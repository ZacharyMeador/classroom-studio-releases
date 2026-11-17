# Classroom Studio

A Windows workspace for class rosters, seating plans, attendance, hall passes, grades and classroom follow-up.

## Download and install

While signed in to GitHub, open [the latest release](https://github.com/ZacharyMeador/classroom-studio-releases/releases/latest) and download the **ClassroomStudio-Setup** installer listed under Assets. Close any older copy, run Setup, then open **Classroom Studio** from Start. Python and build tools are not required.

If you previously pinned a portable copy to the taskbar, unpin that shortcut and pin the installed app once. Future updates use the same installation path. Starting with 7.5.2, the window title shows the installed version and active experience so you can confirm which copy is open.

## Canvas assessment imports

In 7.5.5, **Assessments → Import Canvas data** accepts question reports, student reports, or both. Load questions first and add results later through the same button. Review and reorder the reports before importing; new bank items continue after the highest existing Q number, while matching ItemIDs keep their labels. Randomized assignments remain specific to each student.

See the [7.5.5 report](reports/Classroom_Studio_7_5_5_Unified_Canvas_Import.md) for numbering examples and verification.

## New features and reverting

After installing 7.5.2, the newer interface features turn on automatically. In **Settings → Experience & features**, you can choose **Use Classic**, **Revert last interface update**, or individual feature switches. Classic and Revert disable automatic feature adoption and remain in effect after restarting. **Use latest experience** turns it back on. Your classroom records and appearance choices stay in place.

Interface selection is separate from downloading the application. This repository is private, and the app cannot authenticate to the private update feed. Download new installers from the signed-in release page above; automatic software downloading and installation are not enabled for this private channel.

**Settings → Updates & about** contains **Open version history** and **Install an earlier version…**. Download both the earlier Setup installer and its matching `update.json` from the same release. The app verifies the signature and record-format compatibility, then creates a recovery copy before installing. Version 7.5.5 can revert to 7.5.4 with the same record format. Workspaces containing randomized question assignments cannot be opened safely by versions below 7.5.4; the app blocks that downgrade. Use a separate pre-import recovery copy if an older version is required, understanding that later work is absent from that copy.

## Your data

A fresh workspace has no preloaded classes, rooms, students or seating layouts. Existing records remain in `%LOCALAPPDATA%\ClassroomStudio`; Setup installs the program separately in `%LOCALAPPDATA%\Programs\ClassroomStudio`. Updating or uninstalling the program does not remove the classroom data folder.

Update checks download release information and installers. They do not upload classroom records. This repository contains installers and signed update information; application source is maintained separately.

The update feed is digitally signed with the key trusted by the app. The Windows installer does not yet have an Authenticode publisher certificate.

## Reports

See the [reports folder](reports/) for release verification and links to the original audit and source evidence.
