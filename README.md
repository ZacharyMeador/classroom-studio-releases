# Classroom Studio

A Windows teacher workspace for Canvas courses, private question libraries, class rosters, seating plans, assessments, grades and classroom follow-up.

## Download and install

Open [the latest release](https://github.com/ZacharyMeador/classroom-studio-releases/releases/latest) and download the **ClassroomStudio-Setup** installer listed under Assets. Close any older copy, run Setup, then open **Classroom Studio** from Start. Python and build tools are not required.

If you previously pinned a portable copy to the taskbar, unpin that shortcut and pin the installed app once. Future updates use the same installation path. Starting with 7.5.2, the window title shows the installed version so you can confirm which copy is open.

## Classroom Studio 8.0.1

This maintenance update fixes closing blocked by automatic diagnostic delivery and makes Canvas default to current courses. Filter by term or search by course code/section; switch to All courses when you deliberately want historical classes.

In-app version rollback has been removed. Older installers stay archived on GitHub. Newer updates download automatically and install after you close the app, with Postpone available. Workspace backups and appearance preferences remain.

See the [8.0.1 changes and verification](reports/Classroom_Studio_8_0_1_Shutdown_Canvas.md).

## Classroom Studio 8.0.0

Version 8 is the regular installed update. It opens your existing classroom workspace, creates a validated recovery snapshot on its first launch, and keeps the same installed application and shortcuts. The classroom blueprint builder is preserved.

The new Today, Courses, Insights and Settings layout brings Canvas connection, module browsing, roster review, assignment collection, class standards defaults, private GitHub question libraries and optional question review into one workspace. Manual and offline workflows remain available. Canvas transfers stay unpublished for teacher review.

Use **Report a bug** or **Settings → Help, bug reports & local data** to save a report, run app checks, or send a diagnostic issue to a private repository. Automatic diagnostic delivery on close is optional and excludes student records and credentials. Clearing history and resetting the workspace are separate controls with warnings and typed confirmation.

See the [full 8.0.0 guide, verification and integration limits](reports/Classroom_Studio_8_Update.md).

## Grade-column menus and curves

Version 7.6.2 adds a menu when you click a grade-column title. Edit, analyze, combine, duplicate, export, move, include/exclude, clear, or delete that column. **Curve / add points** offers seven methods with per-student Before/After review, explicit zero handling, recovery copies, and Undo. Flat-point bonuses can include every non-excused cell, including missing-work zeros.

See the [7.6.2 column menu and curve guide](reports/Classroom_Studio_7_6_2_Column_Menus.md).

## Missing gradebook work counts as zero

Version 7.6.1 automatically counts missing gradebook entries as zero in the grid, combined assignments, course totals, reports, and exports. Excused work remains excluded. Randomized questions a student never received stay excluded in the assessment analyzer.

To repair an existing combined grade, open **Gradebook → Grade editor**, select the original assignments, choose **Combine**, and select **Replace** for the old combined assignment. Review Before/After and apply. A recovery copy and Undo protect the previous result. Originals remain unchanged and still count in course totals unless marked Not for Grading.

See the [7.6.1 fix and verification report](reports/Classroom_Studio_7_6_1_Missing_Grades.md).

## Assessment imports and Geometry analysis

In 7.6.0, **Assessments → Import assessment data** accepts Canvas question/student reports, district assessment exports, and tracking workbooks through one entry point. Review class/form assignments, student identity proposals, and conflicting fields before the batch is saved. Geometry is the default district preset; subject, edition, course level, and thresholds are editable.

**Overview, Standards, Progress, and Compare** keep reported totals, individual item evidence, and source-wide statistics distinct. The district benchmark defaults to 75%. PDF summaries include editable Strength and Grow. Totals-only benchmark exports do not create individual student standards estimates.

Canvas retains metadata-first processing, continuous bank-item numbering, and each student's randomized ItemID assignments. Canvas and district files use separate reviewed batches through the same entry point.

See the [7.6.0 report](reports/Classroom_Studio_7_6_0_Assessment_Evidence.md) and [import guide with the supplied-file pairings](reports/Assessment_Import_Guide.md).

## Updates and appearance

**Settings → Updates & about** checks the signed public release feed. Starting with 8.0.1, newer versions download automatically and install on close; teachers can postpone or turn off automatic installation. Pending edits are saved and a recovery copy is required before updating. The app and updater do not install older versions.

Historical releases remain in [GitHub Releases](https://github.com/ZacharyMeador/classroom-studio-releases/releases). They are an archive, not an in-app rollback option. Historical release notes describe features of those older versions.

Navigation, colors, text size, spacing and individual feature choices remain available in Settings. These are appearance preferences within the current app. They do not replace it with an older version.

## Your data

A fresh workspace has no preloaded classes, rooms, students or seating layouts. Existing records remain in `%LOCALAPPDATA%\ClassroomStudio`; Setup installs the program separately in `%LOCALAPPDATA%\Programs\ClassroomStudio`. Updating or uninstalling the program does not remove the classroom data folder.

Update checks download release information and installers. They do not upload classroom records. This repository contains installers and signed update information; application source is maintained separately.

The update feed is digitally signed with the key trusted by the app. The Windows installer does not yet have an Authenticode publisher certificate.

## Reports

See the [reports folder](reports/) for release verification and links to the original audit and source evidence.

