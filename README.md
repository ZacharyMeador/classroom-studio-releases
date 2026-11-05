# Classroom Studio

A Windows workspace for class rosters, seating plans, attendance, hall passes, grades and classroom follow-up.

## Download and install

While signed in to GitHub, open [the latest release](https://github.com/ZacharyMeador/classroom-studio-releases/releases/latest) and download **ClassroomStudio-Setup-7.2.1.exe**. Close any older copy, run Setup, then open **Classroom Studio** from Start. Python and build tools are not required.

If you previously pinned a portable copy to the taskbar, unpin that shortcut and pin the installed app once. Future updates use the same installation path.

## Updates

This repository is currently private. In-app update checks cannot access the private feed; use the installer above for manual updates. When the release repository is public, open **Settings → Updates & about** in the app. The installed version can check for releases, download a verified update, and install it when you close the app. It saves pending edits and creates a recovery copy first. Automatic daily checking is optional.

## Your data

A fresh workspace has no preloaded classes, rooms, students or seating layouts. Existing records remain in `%LOCALAPPDATA%\ClassroomStudio`; Setup installs the program separately in `%LOCALAPPDATA%\Programs\ClassroomStudio`. Updating or uninstalling the program does not remove the classroom data folder.

Update checks download release information and installers. They do not upload classroom records. This repository contains installers and signed update information; application source is maintained separately.

The update feed is digitally signed with the key trusted by the app. The Windows installer does not yet have an Authenticode publisher certificate.
