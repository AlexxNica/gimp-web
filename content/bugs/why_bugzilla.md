Title: Why Do We Use Bugzilla for Reports?
Date: 2015-08-17T11:09:31-05:00
Modified: 2015-08-17T11:09:40-05:00
Authors: Pat David
Status: hidden



From time to time, we get questions about why we are [using Bugzilla](/bugs/) for tracking bug reports related to GIMP or to this web site. Some users would prefer to send us a simple e-mail describing the problem or to fill in a web form without having to register and create a Bugzilla account.

Besides the fact that the [same instance of Bugzilla](http://bugzilla.gnome.org/) is already used for tracking bugs related to GTK+ (GIMP ToolKit) and GNOME, here are some reasons why we ask bug reporters to take the time to create a Bugzilla account:

### Most bug reports need additional information from the reporter

In most cases, it is necessary for the developers to ask for additional information. This can be because some general information such as the GIMP version number or the operating system was not specified, or because the problem is not easy to reproduce and the developers need a step-by-step description of the process that leads to unexpected results. If the report is a request for enhancements, it is often necessary to discuss some details and to clarify what the reporter wants and how it is best implemented.

Requesting the creation of a Bugzilla account ensures that all comments added by developers or other contributors will reach the original reporter. This is also useful for informing the reporter about any changes in the status of the bug report, such as when a patch is supplied or when the bug is fixed.

The owner of a Bugzilla account can switch to a different e-mail address easily and can also configure the types of notifications that are sent via e-mail. Being able to change e-mail addresses is important if some bug reports or proposals for enhancements remain open for a long time.

### Several developers can provide feedback and work on the bug report

Although the requests for additional information could also be handled via e-mail, Bugzilla provides some important features that allow several people to cooperate and to handle bugs in a better way. Anybody can view the status of the bugs or add comments at any time. It is also possible for interested parties to add their own address to the CC list of a bug report in order to be notified whenever something changes. Allowing more people to participate increases the chances that someone will be able to fix the bug or at least provide a timely response. This applies to the GIMP application and its various components as well as to this web site.

In addition, Bugzilla allows us to keep track of the status of all bug reports and ensure that no bug is forgotten. Although most bugs can be fixed rather quickly, a few remain open for a long time because they depend on other bugs or because nobody has been able to work on them yet. Bugzilla never forgets them, while it would be easy to forget about some e-mail discussion that took place several weeks earlier, especially if the bug is eventually fixed by someone else than the original developer.

### Other features of Bugzilla

Bugzilla provides a convenient way to handle duplicate bug reports: when a bug is marked as being a duplicate of another, the reporter can easily see the status of the original bug report and can read all comments attached to it. The reporter is also added to the CC list of the original bug report in order to be notified of any updates.

Note that we have used other bug tracking systems in the past such as the Debian bug tracker, which is mostly e-mail based. But the set of features currently provided by Bugzilla is what allows GIMP developers to work in the best way.
