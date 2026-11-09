# Classroom Studio

A Windows workspace for class rosters, seating plans, attendance, hall passes, grades and classroom follow-up.

## Download and install

While signed in to GitHub, open [the latest release](https://github.com/ZacharyMeador/classroom-studio-releases/releases/latest) and download the **ClassroomStudio-Setup** installer listed under Assets. Close any older copy, run Setup, then open **Classroom Studio** from Start. Python and build tools are not required.

If you previously pinned a portable copy to the taskbar, unpin that shortcut and pin the installed app once. Future updates use the same installation path. Starting with 7.5.2, the window title shows the installed version and active experience so you can confirm which copy is open.

## New features and reverting

After installing 7.5.2, the newer interface features turn on automatically. In **Settings → Experience & features**, you can choose **Use Classic**, **Revert last interface update**, or individual feature switches. Classic and Revert disable automatic feature adoption and remain in effect after restarting. **Use latest experience** turns it back on. Your classroom records and appearance choices stay in place.

Interface selection is separate from downloading the application. This repository is private, and the app cannot authenticate to the private update feed. Download new installers from the signed-in release page above; automatic software downloading and installation are not enabled for this private channel.

**Settings → Updates & about** contains **Open version history** and **Install an earlier version…**. Download both the earlier Setup installer and its matching `update.json` from the same release. The app verifies the signature and record-format compatibility, then creates a recovery copy before installing. Version 7.5.2 supports return points 7.5.1, 7.5.0 and 7.4.2.

## Your data

A fresh workspace has no preloaded classes, rooms, students or seating layouts. Existing records remain in `%LOCALAPPDATA%\ClassroomStudio`; Setup installs the program separately in `%LOCALAPPDATA%\Programs\ClassroomStudio`. Updating or uninstalling the program does not remove the classroom data folder.

Update checks download release information and installers. They do not upload classroom records. This repository contains installers and signed update information; application source is maintained separately.

The update feed is digitally signed with the key trusted by the app. The Windows installer does not yet have an Authenticode publisher certificate.

## Reports

See the [reports folder](reports/) for release verification and links to the original audit and source evidence.
