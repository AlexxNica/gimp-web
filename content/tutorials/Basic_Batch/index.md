Title: GIMP Batch Mode
Date: 2015-08-18T12:24:32-05:00
Modified: 2015-08-18T12:24:36-05:00
Author: Pat David


## Introduction

GIMP comes with a so-called batch mode that allows you to do image processing from the command line. It also makes it easy to apply the same set of operations to a number of images. We have got a lot of questions on the mailing-lists on how to use the batch mode and this small page tries to explain the basics to you.

GIMP can be started with a number of command-line options. Let's have a closer look at the output of `gimp --help`:

    :::bash
    GIMP version 2.4.1

    Usage: gimp [option ... ] [file ... ]

    Options:
      -?, --help              Show help options
      -v, --version           Show version information and exit
      --verbose               Be more verbose
      -d, --no-data           Do not load brushes, gradients, palettes, patterns, ...
      -f, --no-fonts          Do not load any fonts
      -i, --no-interface      Run without a user interface
      --batch-interpreter=<procedure>
                              The procedure to process batch commands with
      -b, --batch=<commands>  Batch command to run (can be used multiple times)
      ...

In order to do image processing from the command-line, you usually use the Script-Fu batch interpreter. This is the default, which makes things simple. To give you an impression of what can be done, try the interactive console mode:

    gimp -b -

This will tell GIMP to start in batch mode and accept commands on the command-line. This is essentially the same as using the Script-Fu console. It would however be tedious to enter the commands here, so instead we will create a simple script and show you how to run that:


## A simple example

    (define (simple-unsharp-mask filename
                                  radius
                      amount
                      threshold)
       (let* ((image (car (gimp-file-load RUN-NONINTERACTIVE filename filename)))
              (drawable (car (gimp-image-get-active-layer image))))
         (plug-in-unsharp-mask RUN-NONINTERACTIVE
                           image drawable radius amount threshold)
         (gimp-file-save RUN-NONINTERACTIVE image drawable filename filename)
         (gimp-image-delete image)))

This simple script takes a filename and some numeric parameters. It opens the respective file, applies the Unsharp Mask filter and saves the image again (be careful, for the sake of simplicity this script overwrites the original image). It does all this w/o any user interaction, so we can run it without any user interface. In order to do that, save the script with the .scm extension in the **~/.gimp-2.4/scripts** directory. Then run it like this:

    gimp -i -b '(simple-unsharp-mask "foo.png" 5.0 0.5 0)' -b '(gimp-quit 0)'


There is a catch here: Some plugins or Script-Fu scripts create new layers and then flatten the image again. This changes the drawable ID. If this is the case insert the following line to get the current drawable ID just before saving the image:

    (set! drawable (car (gimp-image-get-active-layer image)))



## Processing several files

You might want to apply an effect to a number of files, typically to a set of files in the same directory. GIMP 2.2 added a very useful function for this purpose, the **file-glob** plug-in. This turns GIMP into a versatile batch processor. In order to use it, we will need to do some modifications to our script:

      (define (batch-unsharp-mask pattern
                                  radius
                                  amount
                                  threshold)
      (let* ((filelist (cadr (file-glob pattern 1))))
        (while (not (null? filelist))
               (let* ((filename (car filelist))
                      (image (car (gimp-file-load RUN-NONINTERACTIVE
                                                  filename filename)))
                      (drawable (car (gimp-image-get-active-layer image))))
                 (plug-in-unsharp-mask RUN-NONINTERACTIVE
                                       image drawable radius amount threshold)
                 (gimp-file-save RUN-NONINTERACTIVE
                                 image drawable filename filename)
                 (gimp-image-delete image))
               (set! filelist (cdr filelist)))))

This version of the script takes a glob pattern instead of a filename and will apply the Unsharp Mask filter to all files matching this pattern. In order to sharpen all PNG images in the current directory, you would run the following command:

    gimp -i -b '(batch-unsharp-mask "*.png" 5.0 0.5 0)' -b '(gimp-quit 0)'

## Further information

If you want to write your own scripts for batch processing, we suggest you use the **Procedure Browser** as found in the **Help** menu. It gives you a detailed list of all commands.

