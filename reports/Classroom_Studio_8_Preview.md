# Classroom Studio 8 — Preview 1

**Historical development report.** Delivery is superseded by [the regular 8.0.0 update](Classroom_Studio_8_Update.md). Use the standard Setup installer and existing workspace.

November 24, 2026.

This is a separate Windows preview of the course workspace redesign. It keeps the stable application available and copies its database into an isolated preview workspace. The classroom blueprint builder and seating geometry remain unchanged.

## Download and run

[Download the Windows preview](https://github.com/ZacharyMeador/classroom-studio/actions/runs/45433835267/artifacts/14941331315)

GitHub sign-in with access to the app source repository is required. This Actions download is retained until December 24, 2026; the downloaded app itself does not expire.

Extract the entire ZIP, then open **ClassroomStudio8Preview.exe**. Keep the `_internal` folder beside the executable. This preview does not replace your existing shortcut or automatically install over the stable app.

## Included

- Today / Courses / Insights navigation, with Classic navigation available after restart.
- Canvas connection before assessment creation; course/module browsing and reviewed roster/result collection.
- Class standards defaults, assessment overrides and revision-specific question mappings.
- Private GitHub question-library access, inspected QTI packages and recorded Canvas draft transfers.
- Optional question-only AI review.
- Bug reports, private GitHub diagnostic issues and optional automatic reporting on close.
- Warning-protected local history cleanup and full preview reset.

## Send a testing report to GitHub

Open **Settings → Help, bug reports & local data**.

1. Choose your private app repository.
2. Enter a fine-grained GitHub token restricted to that repository with **Issues: read and write**. Select OS-vault storage if it should be remembered.
3. Use the app normally. Choose **Run checks and send**, or enable **Automatically send diagnostics when I close the app**.
4. Use **Send written bug report** to include your own description of a visual problem or incorrect result.

The report includes app/build version, read-only integrity/dependency/catalog checks, visited screens and coded errors. It does not automatically include student records, grades, credentials, screenshots or raw exception messages. Check results do not prove that every workflow or live service is correct. Review anything you type before sharing it.

Reports become private GitHub issues. Ask the connected chat to review the latest diagnostic issues when testing is finished; sending a report does not automatically start a new AI analysis. Unconfirmed uploads remain saved locally and are checked before retrying.

## Clear history or start empty

| Action | Effect | Confirmation |
|---|---|---|
| Clear activity history | Removes audit/cache/report history and Undo/Redo; keeps classroom records, scoring evidence and blueprints | `CLEAR HISTORY` |
| Reset all local data | Closes the preview and removes all of its workspace records, settings, drafts and saved credentials | `RESET ALL LOCAL DATA` |

Both show a warning and offer backup export. Automatic recovery copies can be included. Neither action deletes the stable app's database, remote Canvas/GitHub records or separately exported files. Reset starts empty on the next launch.

## Validation

Verified code commit: `f1ba34ffccc7eb6a30e1208c6f4b7845c214e19f`.

- **403 unit/regression tests passed** locally and on Windows.
- Native and packaged Windows checks passed with **zero captured callback errors**, including shutdown.
- Checked light/dark appearance at 100/125/150% scaling, course/module navigation, question mapping, private-report delivery with a simulated service, automatic-close dispatch, cancellation of cleanup, Classic restart, and unchanged stable data/blueprint.
- Source checks and dependency audit passed. Live credentials, district imports and account eligibility were not exercised by these mocked checks.
- [Windows build and evidence](https://github.com/ZacharyMeador/classroom-studio/actions/runs/45433835267)
- [Source checks and audit](https://github.com/ZacharyMeador/classroom-studio/actions/runs/45433854950)
- Windows ZIP SHA-256: `4fb96a155f2aa54fd080a60950a759f1da9db3b72c428a7c787b0c0ec7975625`.

## Remaining live checks

Canvas district permissions, QTI conversion/media/scoring, private-repository credentials and AI account access still need account-level testing. New Quizzes randomized bank draws retain a **Finish in Canvas** step. GitHub teaching-library access is read-only; local corrections do not rewrite the source repository. Automatic standards discovery for every jurisdiction is not included in this preview.

Preview edits stay in the preview workspace. Back them up before returning to the stable app.
