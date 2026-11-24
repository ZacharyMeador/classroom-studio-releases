# Classroom Studio

A Windows teacher workspace for Canvas courses, private question libraries, class rosters, seating plans, assessments, grades and classroom follow-up.

## Download and install

Open [the latest release](https://github.com/ZacharyMeador/classroom-studio-releases/releases/latest) and download the **ClassroomStudio-Setup** installer listed under Assets. Close any older copy, run Setup, then open **Classroom Studio** from Start. Python and build tools are not required.

If you previously pinned a portable copy to the taskbar, unpin that shortcut and pin the installed app once. Future updates use the same installation path. Starting with 7.5.2, the window title shows the installed version so you can confirm which copy is open.

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

## New features and reverting

In 8.0.0, choose **Settings → Startup & recovery → Classic** and restart for familiar navigation in the same workspace. You can return to Courses navigation at any time. Version 8 can also revert to the verified **7.6.2** installer using **Settings → Updates & about → Install an earlier version…** and that release's matching signed `update.json`. Saved numeric grades, attendance and blueprints remain; version 8 integration records stay stored and become accessible again after upgrading.

Earlier 7.x releases also retain their feature controls. After installing 7.5.2, the newer interface features turn on automatically. In **Settings → Experience & features**, you can choose **Use Classic**, **Revert last interface update**, or individual feature switches. Classic and Revert disable automatic feature adoption and remain in effect after restarting. **Use latest experience** turns it back on. Your classroom records and appearance choices stay in place.

The public release channel supports the app's signed update checks. Settings → Updates & about offers Download update and Install when I close the app. New interface features activate after installation; individual appearance and feature choices remain available.

**Settings → Updates & about** contains **Open version history** and **Install an earlier version…**. Download both the earlier Setup installer and its matching `update.json` from the same release. The app verifies the signature and record-format compatibility, then creates a recovery copy before installing. Version 7.6.2 can revert to the verified 7.6.1 return point; saved curves remain unless you undo them or restore a recovery copy. Version 7.6.1 can revert to the verified 7.6.0 return point. This restores the previous missing-grade policy while preserving repaired numeric combined scores. Version 7.6.0 can revert to the verified 7.5.5 return point. Imported district/tracker evidence stays on disk but its new analysis views require 7.6.0; upgrade again to view them. Earlier targets are blocked when district evidence exists. **Assessment overview first** in Experience settings can be turned off to start Canvas/manual results in the familiar scoring charts. Workspaces containing randomized question assignments cannot be opened safely by versions below 7.5.4; the app blocks that downgrade. Use a separate pre-import recovery copy if an older version is required, understanding that later work is absent from that copy.

## Your data

A fresh workspace has no preloaded classes, rooms, students or seating layouts. Existing records remain in `%LOCALAPPDATA%\ClassroomStudio`; Setup installs the program separately in `%LOCALAPPDATA%\Programs\ClassroomStudio`. Updating or uninstalling the program does not remove the classroom data folder.

Update checks download release information and installers. They do not upload classroom records. This repository contains installers and signed update information; application source is maintained separately.

The update feed is digitally signed with the key trusted by the app. The Windows installer does not yet have an Authenticode publisher certificate.

## Reports

See the [reports folder](reports/) for release verification and links to the original audit and source evidence.
