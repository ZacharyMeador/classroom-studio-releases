# Classroom Studio 7.5.3 — Mouse-wheel error fix

Date: November 16, 2026

Application commit: `74836f9f1e3f76afb00c258074d3e896a054c9b4`

## Reported behavior and reproduced cause

The reported problem was a burst of error messages when using the mouse wheel past the last student name. The exact screen and error text were not provided, so this report does not claim the user's individual traceback was confirmed.

Investigation reproduced a shared scrolling defect in CustomTkinter 5.2.2. A native Tk dropdown creates its popup in Tcl rather than as a Python widget. Tkinter consequently supplies that popup's pathname as a string in a wheel event. CustomTkinter's global scrolling handler assumes every event target has a `.master` attribute and raises `AttributeError: 'str' object has no attribute 'master'`.

Every open scrollable panel can receive the same event, explaining how one wheel movement can produce several modal errors. Panels that have been closed also leave global wheel and Shift-key bindings registered in the upstream implementation, allowing unnecessary callbacks to accumulate.

## Changes

- Added the shared `scrolling.ScrollableFrame` subclass. It walks only actual Tk widget parents; native popup pathnames are ignored by unrelated panels so the popup keeps its own normal scrolling.
- Replaced scrollable-panel constructors and subclasses across 15 application modules, including Students, Attendance, Gradebook, assessments, hall passes and dialogs.
- Each panel records its own global binding IDs and removes only those bindings when destroyed. Other panels and independent application handlers remain registered.
- Events already queued for a closing panel are ignored safely.
- Kept native list boundary behavior. Repeated scrolling at the first or last row stops there. The change does not hide general application errors or disable normal scrolling.
- Advanced the application version to 7.5.3 and added it to the compatible rollback table. Core/suite schemas remain 8/7. Existing records, saved scores and interface preferences use the same storage.

## Verification

Local unit/integration checks passed all **264 tests**. Compilation, fatal-error lint checks and whitespace checks passed. The local headless environment could not launch the desktop UI; actual interface validation was performed by GitHub Actions.

[Source verification run](https://github.com/ZacharyMeador/classroom-studio/actions/runs/43905405024) passed on Python 3.13, including all 264 tests, the full application GUI workflow, and the dependency audit. The audit reported no known vulnerabilities among the 27 resolved dependencies at the time of the run.

The new real-event GUI checks exercise 80 fictional students and verify:

| Check | Coverage |
| --- | --- |
| Students | Normal wheel movement and repeated movement beyond both name-list boundaries; selection preserved |
| Attendance | Normal movement and both boundaries; selection preserved |
| Gradebook | Names and scores stay aligned while scrolling either table and at both boundaries |
| Saved grades | Score values remain unchanged after wheel events |
| Native dropdowns | Actual Tcl-created popup events at 100%, 125% and 150% scaling; both boundaries |
| Scrollable panels | Normal wheel movement works and stops at both boundaries |
| Dialog cleanup | Closing panels removes their own callbacks and Tcl commands while preserving an independent handler |
| Error handling | No wheel callback errors, and no callback errors in the complete GUI workflow |

The existing appearance, quick-attendance, alphabetical enrollment, import review, assessment, standards, backup and audit regression workflows also passed in the source build. Tests use fictional data only.

[Native Windows run](https://github.com/ZacharyMeador/classroom-studio/actions/runs/43905404449) passed all 264 tests and the complete installed-app GUI workflow after both installation and reinstallation. All eight scrolling checks passed in both runs, with zero callback errors. Signed rollback to 7.4.2, launching the earlier app, upgrading back, uninstalling, and preservation of the fixture database's SHA-256 all passed. The earlier source also read new-format saved scores, attendance and feature preferences successfully.

The downloaded build artifact matched GitHub's SHA-256. The installer matched its signed manifest, whose Ed25519 signature was verified against the existing trusted public key. Portable archive integrity and the packaging exclusions for personal files passed. The installer and manifest uploaded to the release draft matched those verified files byte-for-byte by GitHub's recorded digest and size.

| Download | Bytes | SHA-256 |
| --- | ---: | --- |
| `ClassroomStudio-Setup-7.5.3.exe` | 63,252,666 | `25c07cfb1136efcc7d978c45b56c6d7f25f9e7571592f9021e2000e9c3c81e18` |
| `update.json` | 19,573 | `bfc788ec29aafaea817318005ce8e6ef97d71428dfc1dcf92b1ad56d36e95d61` |

[Machine-readable verification evidence](https://github.com/ZacharyMeador/classroom-studio/tree/main/reports/verification_7_5_3) includes source and native GUI reports, the dependency audit, download verification and publication verification.

The release was published as the latest **7.5.3**. Both files were downloaded again from the published release and passed signature/checksum verification. [Release page](https://github.com/ZacharyMeador/classroom-studio-releases/releases/tag/v7.5.3).

## Installation and rollback

Close Classroom Studio, download `ClassroomStudio-Setup-7.5.3.exe` from the 7.5.3 release, run it over the current installation, and reopen the application. Confirm **7.5.3** in the window title or Settings. Only the Setup executable is needed for manual installation.

Both GitHub repositories remain private. Downloading requires an authorized GitHub sign-in; anonymous in-app update checks cannot read the private release feed. This release does not change that restriction.

Settings → Updates & about retains the earlier-version installation option. Use the chosen compatible version's installer and its matching signed `update.json`; a recovery copy is required before rollback. Interface feature/revert choices remain available separately.

## Scope

This is a focused fix for the reproduced shared wheel-handler failure and callback cleanup. It is not a claim that every possible scrolling device, operating system or unrelated application defect has been tested. The user's machine has not been remotely updated. If errors remain after installing 7.5.3, the first error message and affected screen will identify whether a different path is involved.
