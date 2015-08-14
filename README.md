# vdr

Script for placement of windows on virtual desktops.

## Summary

At the time of this writing, I am using a Debian Jessie stable system and the corresponding Iceweasel (i.e. Firefox) package.  My laptop has been a bit unstable lately due to a hardware fault and I find myself recovering my Iceweasel session every day or so.  When I do, it restores the all of the windows I had opened to their correct URLs and sizes, but it does not place them on the correct virtual desktop.  This is a [known bug](https://bugzilla.mozilla.org/show_bug.cgi?id=372650) that hasn't gotten much attention since it was reported many years ago, in part because it's a bit tricky to solve in a cross-platform manner.

This script is a makeshift, platform-specific solution to that problem.  It stores a JSON database of mappings from application names (e.g. `/usr/lib/iceweasel/iceweasel`) to window data dictionaries.  Upon execution, it can either (1) examine a running application and add to this database or (2) use the database to move an application's windows to different virtual desktops (which it does by window title).

I wrote this application to solve my short-term problem with Iceweasel, but it is not Iceweasel-specific.  Feedback and suggestions are, of course, welcome.

## Requirements

This script relies upon the ability to call `wmctrl` as a subprocess.  That binary can be found in the `wmctrl` Debian package.

## Example Usage

* Store window data for an application with PID 9876: `vdr --save 9876`
* Use window data to set virtual desktops of an appication with that PID: `vdr --load 9876`
* Store window data for the application using a fixed name (rather than `/proc/self/exe`): `vdr --save --name "Iceweasel Default Profile" 9876`
