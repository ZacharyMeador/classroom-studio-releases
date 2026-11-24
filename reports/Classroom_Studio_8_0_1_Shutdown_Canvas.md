# Classroom Studio 8.0.1: closing and Canvas course selection

## Report and confirmed defects

The teacher reported a responsive app whose close button did not close it, and a
Canvas picker containing past-year classes and apparently duplicate names.

The 8.0.0 close path waits for automatic GitHub diagnostic delivery to call its
success callback. Missing credentials, a rejected/failed delivery, or an active
background operation can return without invoking that callback. The window stays
open. This is a confirmed code defect matching the symptom; no diagnostic log from
the teacher's particular incident was available to prove its exact trigger.

The Canvas picker requested all teacher enrollments without an active-enrollment
filter, and displayed only a name and numeric ID. It did not request term or
conclusion metadata. Those omissions account for the ambiguous historical list.

## Changes

- Bound optional diagnostic sending on close to five seconds. A second close
  request stops waiting immediately. Missing credentials, failed delivery and
  busy operations cannot prevent the ordinary save-and-close path.
- Keep normal pending-edit validation and saving. A genuine invalid edit or
  failed workspace save still requires attention; shutdown must not discard it.
- Save checks locally when closing without a report token. A prepared report
  remains local if sending is interrupted. An interrupted send is not proof that
  GitHub did or did not receive it; existing delivery identities prevent blind
  duplicate retries. Reports remain free of student data and credentials.
- Stop processing queued UI callbacks after widget destruction.
- Default Canvas browsing to `enrollment_state=active`, requesting `term`,
  `sections` and `concluded`. Exclude explicitly concluded courses from this view.
- Provide All courses, term selection and course/code/term/section search. Display
  name, course code, term and stable Canvas ID; show section details on selection.
- Deduplicate repeated course IDs, never distinct courses merely sharing a name.
- Clear stale course context on reconnection and cancel a pending connection on
  disconnect or window destruction.

Canvas documents that its active-enrollment query respects section, course and
term date overrides: [Courses API](https://developerdocs.instructure.com/services/canvas/resources/courses).
The app does not infer the academic year from a course title. Districts can leave
old courses/enrollments active; the term filter provides an explicit correction.
Missing term metadata is labeled as unavailable rather than invented.

## Update policy

At the teacher’s request, version rollback is removed from the app, update helper,
and release workflow. Historical releases remain on GitHub unchanged. New versions
download automatically and install on close by default, with Postpone and a
preference to disable automatic installation. Workspace backups and interface
preferences remain separate. The helper rejects older signed installers.

## Validation

Regression coverage includes missing credentials, failed/stalled reporting,
concurrent operations, repeated close clicks, late callbacks and save-veto retry;
active-query parameters, concluded/deleted classes, duplicate IDs, same-name
distinct IDs, missing metadata, search and term identity. The GUI check exercises
the actual window-close protocol, plus normal and Classic navigation.

The Windows release workflow tests native install, reinstall, preservation of the
existing workspace, and data-preserving uninstall. Rollback is no longer a product
feature or a release check. Previous stress-test evidence remains historical.


Validation completed for app commit `76b4f391fa3da15ab96c7c7e5e47cf8f3e818692`:

- 417 strict unit/integration tests and static checks passed.
- Source GUI workflows passed with zero callback errors.
- Dependency audit: 41 packages, zero known vulnerabilities reported.
- Windows source and packaged Studio checks passed, including real close-button
  handling, missing/failed/busy/stalled diagnostics, current-course filtering,
  removal of downgrade controls, automatic-update default and Classic navigation.
- Native installation, reinstallation, existing-workspace startup, classroom-data
  preservation and data-preserving uninstall passed. The blueprint fixture was
  unchanged.
- The installer checksum and signed manifest were independently verified with the
  existing trusted update key.

[Source checks](https://github.com/ZacharyMeador/classroom-studio/actions/runs/45466778195)
and [Windows release build](https://github.com/ZacharyMeador/classroom-studio/actions/runs/45466778257).
Machine-readable evidence is in `reports/verification_8_0_1/` in the source repository.
The earlier build was cancelled after the requested removal of version rollback;
its installer is not the released artifact.

Installer: `ClassroomStudio-Setup-8.0.1.exe` (65,281,368 bytes).
SHA-256: `9225c8334d9d685afa24c8466aa69b7a424a9be1434d81785dbd7e014965dfef`.
Manifest SHA-256: `84cde7420b0b8f0087f245ae87cfbef6da4700f292f31bd01ecaaa35abd167d2`.

These tests use fictional data and simulated provider responses. They do not
certify a live NNPS account or establish the exact trigger of the teacher's incident.
The update manifest is digitally signed; the installer has no Authenticode publisher certificate.

## Scope

Normal full application update, version 8.0.1. No database schema, grade policy,
assessment import, room blueprint builder or saved room geometry changes.
