# Classroom Studio 7.5.2: automatic interface features and persistent revert

## Cause and resulting behavior

Versions 7.5.0 and 7.5.1 defaulted to Classic, leaving the four newer workflow
views disabled unless the teacher opted in. This made an installed update look
largely unchanged. Version 7.5.2 adopts the new interface on first launch,
including existing installations, and displays the installed version and active
experience in the window title and Experience settings.

The guided home, simpler gradebook, focused assessment editor and student summary
cards turn on automatically. The prior feature selection is saved before that
change. **Revert last interface update** restores it; **Use Classic** turns all
four off. Both actions disable future automatic feature adoption and persist
across restarts and subsequent releases. **Use latest experience** enables all
current features and automatic adoption. Individual switches preserve the
teacher's choice; a later update only enables newly introduced feature keys.

Pending grades are validated before changing features. Preferences, prior
selection and automatic-adoption tracking are committed atomically during
startup adoption. Classroom records and appearance choices are unchanged.
Backup restoration uses the same policy for the restored preferences.

## Scope of automatic behavior

This release automatically activates interface features **after installation**.
It does not claim to download or install new software automatically. The private
GitHub release feed requires authentication that the current app does not have;
repository visibility, credentials and the trusted signing key are unchanged.
The Updates screen explains this distinction and retains version history.

Core schema 8 and suite schema 7 are unchanged. Signed compatible rollback to
7.5.1, 7.5.0 and 7.4.2 is allowed, with the existing format verification and
mandatory recovery copy. Native CI continues to exercise the 7.4.2 return point.

## Verification

New regressions cover first-launch defaults, restoration of an existing Custom
selection, persistent Classic, persistent individual switches, future feature
adoption, an existing opt-out and transaction failure. Real GUI checks cover
visible default views, version/mode labels, one-click revert, individual choices,
Use latest experience, Classic and Undo. Existing attendance, grade, AP,
standards, backup and installer checks remain required.

The first Windows validation run (42626638786) passed all six new feature checks, then exposed a timing assumption in the existing import-review smoke check: its fixed 150 ms callback ran before the Apply control was mapped. The diagnostic screenshot also showed the scaled dialog cascading partly off-screen. The dialog now opens within the screen margins; the test waits up to five seconds for the real control to map, checks that the footer is on-screen, and closes the modal even when an assertion fails. The failed build was not published.

The next Windows run (42629764633) passed the complete installed-app workflow, including the import-dialog correction. Reinstallation exposed a delayed callback from a closed preview window. CustomTkinter 5.2.2 schedules Windows titlebar/icon work but does not cancel pending timers in its window destructor. A stale timer can encounter a reused Tcl command name. Classroom dialogs now cancel callbacks owned by that window and its children before destruction, while preserving timers owned by the rest of the app. The grade-entry focus timer is now owned by its dialog. Deterministic Tcl regressions cover command reuse and independent-window work; native GUI verification also requires timer cleanup. This build was also held from publication.

Upstream code reviewed: [CustomTkinter 5.2.2 window implementation](https://raw.githubusercontent.com/TomSchimansky/CustomTkinter/v5.2.2/customtkinter/windows/ctk_toplevel.py). Failure records are retained in [pre_release_runs](https://github.com/ZacharyMeador/classroom-studio/tree/main/reports/verification_7_5_2/pre_release_runs/).

A further native Windows run (42633907593) exited with access-violation code 3221225477 during rapid modal checks at 150% scaling. The shared dialog class now applies the Windows titlebar color directly through DWM without CustomTkinter's withdraw/update/deiconify sequence, which could run input callbacks while a dialog was still being constructed. A real-widget regression requires pending application input callbacks to remain pending throughout construction. Fatal native diagnostics are enabled for the test executable. This run was not published.

Source workflow [42636188128](https://github.com/ZacharyMeador/classroom-studio/actions/runs/42636188128) passed on application commit `5fdef012554d71d77bd9a4beaa05ed8be43bf4bb`:

- 261 unit and integration tests passed, including two real-Tcl callback lifecycle regressions.
- Dialog construction and timer cleanup, all 6 automatic-feature GUI checks, 9 experience checks and 8 attendance/roster checks passed, with zero callback errors.
- Dependency audit reported no known vulnerabilities.
- Downloaded source evidence matched the workflow artifact SHA-256.

Native Windows workflow [42636187828](https://github.com/ZacharyMeador/classroom-studio/actions/runs/42636187828) also passed on the same application commit:

- Install, compiled app launch, reinstall, uninstall and existing database preservation passed.
- Dialog timer cleanup and the 6 automatic-feature, 9 experience and 8 attendance/roster GUI checks passed in both installed and reinstalled builds, with zero callback errors.
- The signed rollback to 7.4.2, recovery copy, old-version reading of newer records and upgrade back to 7.5.2 passed. Native rollback to 7.5.0/7.5.1 was not executed in this workflow; their formats are covered by compatibility tests.
- The downloaded Windows artifact matched GitHub's SHA-256. The manifest signature, installer hash and byte count, portable ZIP integrity and packaged-data exclusions were verified before publication.
- Both files were downloaded again from the published release. Their bytes matched the verified build, and the served manifest signature and installer hash were verified again.

## Published release

[Classroom Studio 7.5.2](https://github.com/ZacharyMeador/classroom-studio-releases/releases/tag/v7.5.2) is the latest published release. Download `ClassroomStudio-Setup-7.5.2.exe` while signed in, close Classroom Studio, then run Setup. This publication does not update an already installed copy by itself.

| Asset | Bytes | SHA-256 |
| --- | ---: | --- |
| Installer | 63247181 | `6b3f2d3cbddf5f1d8d5805545204adf26e82e335f03971c822e1c55f91780283` |
| Signed update manifest | 18749 | `9d46811503cc3938e9a2d3f48950ed0b72e1fca7a287f333cddc2c89870d018d` |

Verification records and screenshots are in [verification_7_5_2](https://github.com/ZacharyMeador/classroom-studio/tree/main/reports/verification_7_5_2/).

[Windows 7.5.2 experience defaults](https://github.com/ZacharyMeador/classroom-studio/blob/main/reports/verification_7_5_2/automatic-features.png)

[Published 7.5.2 release](https://github.com/ZacharyMeador/classroom-studio/blob/main/reports/verification_7_5_2/published-release.jpg)

**Status:** source validation, native Windows verification and publication completed.
