# Classroom Studio 8.0.0 — full desktop update

November 24, 2026. The connected course workspace is now the regular installed application.

Close Classroom Studio, run **ClassroomStudio-Setup-8.0.0.exe** over the existing installation, and reopen the usual Classroom Studio shortcut. It opens the existing `%LOCALAPPDATA%\ClassroomStudio\seating_studio.sqlite3` workspace. A validated recovery snapshot is saved before the first version 8 startup can modify it. Setup and uninstall keep classroom data separate from program files.

## Working features

- Today / Courses / Insights navigation with course workspaces, existing gradebook, assessment editor, student profiles, attendance, passes and reports.
- Existing classroom blueprint builder and seating engine, reached from the course overview.
- Canvas connection without an assessment; teacher course list, module order, assignment search, course/section roster review, selected-assignment tracking, question-content preview, and collection history.
- New Quizzes question-first report import and total-score evidence for ordinary assignments. Background refresh stages new source snapshots; applying them remains reviewed. Local score edits and curves are protected. Failed collection never clears earlier results.
- Course-level standards editions inherited by new assessments, explicit assessment overrides, and confirmed source-content/framework mappings. Historical assessments keep their edition snapshots.
- Reviewed source-to-imported-Canvas-item links, reusable local question corrections, and saved balanced draw plans with a distinct-family feasibility check. Combined calculator/non-calculator parts continue the existing numbering through the question-first importer; repeated ItemIDs across distinct assignments are rejected instead of conflated.
- Private GitHub catalog browsing, immutable commit selection, checksum-verified QTI retrieval, bounded package inspection, exact source-ID question lookup, and offline cache of inspected resources. Repository visibility is not changed.
- Deliberate Canvas QTI migration with no manual ZIP handling. The app records transfer intent/migration IDs and checks progress. It does not auto-publish a quiz. Source versions stay separate from deployed copies.
- Optional selected-question AI review using a local model server, an online API, or experimental ChatGPT plan sign-in. The Question Studio adapter is reused from `hhs_math` commit `1371ae0ef0e34ef0375602b6ca542048a0eb7bd2`. No student records are sent to AI by this feature.
- Light/dark/system appearance, accent, typography, density, preferred startup page, and last course restoration. Familiar navigation is available under Settings → Startup & recovery, after restart.
- Settings → Help, bug reports & local data: create, preview, save, copy, export or send a bug report to a private GitHub repository. Run read-only app checks and send diagnostics on demand, or opt into automatic diagnostic reports on app close. Diagnostics contain version, platform, view/appearance, check outcomes and coded runtime events, excluding classroom data and credentials.
- Two explicit cleanup choices: clear activity/cache history while preserving classroom records, or reset all data in this workspace. Both require a warning and typed confirmation. Automatic recovery copies can be included; Canvas/GitHub records and exports elsewhere are outside their scope.

## Connect and use

1. Open Courses → Canvas. Enter the Canvas site and personal access token locally. This version uses the same personal-token approach already tested by Zach; district-managed OAuth is not configured.
2. Choose the course and module. Import/review the roster, choosing the section for the correct period. Existing manual names are preserved; people missing from Canvas are retained for manual review.
3. Set the course's standards default on its overview. Select an assignment and choose Track results, then Collect now and Review collection.
4. Open Question library. Enter `owner/repository` and a fine-grained GitHub token restricted to that repository with Contents read access. This app's connection is separate from ChatGPT's GitHub connector. No developer secret is embedded.
5. Inspect a package before reviewing its questions or choosing Canvas draft. A chosen Canvas course and linked local class are required for transfer.
6. AI is optional. Choose a provider and model in Settings → Connections & AI. Ask AI sends only the selected question and relevant standards, and its response is a suggestion.

Credentials use the OS vault only when supported and explicitly saved. Otherwise they stay in memory. Application backups contain source caches, drafts and classroom data but no provider tokens.

## Report a bug or clear local data

Choose **Report a bug** in the sidebar, or **Settings → Help, bug reports & local data**. Enter a title, the steps, what you expected and what happened. Preview the report, then save it locally, copy it or export a Markdown file. **Open GitHub issues** opens the issue form; it does not send your report. Review anything you type for student information before sharing it.

For in-app delivery, select the private app repository (`ZacharyMeador/classroom-studio` by default) and enter a fine-grained GitHub token restricted to that repository with **Issues: read and write**. This is separate from the teaching-library token. Select OS-vault storage if you want it available on later launches. **Run checks and send** creates a GitHub issue containing database integrity/reference checks, dependency/catalog checks and coded session errors. **Send written bug report** sends the form you reviewed. A report link appears after confirmed delivery, and reports remain available under **Saved reports**.

Optionally enable **Automatically send diagnostics when I close the app**. This sends the diagnostic summary for your testing session; it does not silently attach your written bug description. If sending fails, the app stays open with the failure and keeps the report locally. Disable the option to close without sending. An ambiguous delivery is checked against its report ID before any retry, preventing a blind duplicate issue. Resetting the workspace bypasses automatic reporting. The app refuses to send reports to a public repository.

These checks do not execute every feature or prove live integrations are correct. Exercise your workflows normally, then add notes for visual problems or incorrect results that did not raise an error. Once a report is sent, share the issue link or ask this chat to review the newest diagnostic reports; the app does not start a new ChatGPT analysis automatically.

The same settings page has two separate deletion choices:

| Choice | What is removed | What stays | Required confirmation |
|---|---|---|---|
| Clear activity history | Import and grade-change audit logs, cached packages/content, AI reviews, bug reports and Undo/Redo | Students, grades, attendance, passes, assessments, raw scoring evidence, source baselines and room blueprints | `CLEAR HISTORY` |
| Reset all local data | The entire current workspace, including classes, grades, blueprints, settings, drafts, caches and saved connection credentials | Remote Canvas/GitHub records, and separately exported files | `RESET ALL LOCAL DATA` |

Both actions show a warning before asking for the exact phrase. Cancel leaves the data in place. The recovery-copy checkbox controls whether this workspace's automatic recovery copies are also removed; it starts checked. **Export a backup first** is available on the same page. Reset closes the app and the next launch starts empty. No actual classroom workspace was deleted while implementing or testing these controls.

## Classic navigation and application rollback

- Choose Classic under Settings → Startup & recovery, then restart. The same workspace stays open.
- To install 7.6.2, download its Setup and matching signed update.json from version history. Choose Settings → Updates & about → Install an earlier version. The app checks both the signature and the current data format and requires a recovery copy before applying the rollback after closing.
- Saved numeric grades, attendance and room blueprints remain. Version 8 integration records remain stored but are unavailable in 7.6.2; upgrading again restores access. Restoring an older database backup is a separate operation and replaces work saved since that backup.
- The existing Windows application ID, installation directory, shortcuts, trusted signing key and stable update feed are retained. The new interface opens by default after installation.
- Reset all local data closes the app, removes its saved credentials, then deletes only the active workspace database, its SQLite sidecars and optionally recovery copies. Pending app installation is cancelled for reset. The next launch starts empty.

## Boundaries that still require live validation

- Canvas district permissions, QTI→New Quizzes conversion, actual math/image rendering, item-ID correspondence, and FRQ rubric installation require a real course test. A completed content migration is not proof of a correct administered quiz.
- New Quizzes randomized bank-draw creation is not exposed as a general write operation by the documented item API. Configure and verify bank draws in Canvas; the app never substitutes one static random sample for per-student randomization.
- The private GitHub integration is read-only. Local corrections are separate drafts; they do not rewrite the maintained repository or already administered assessments.
- ChatGPT account/client eligibility and live sign-in/inference have not been established by mocked tests. The local/API alternatives remain explicit choices.
- Image bytes are not yet attached to AI review. The AI is instructed not to claim it inspected unavailable diagrams. Open the actual Canvas question to verify interactive/media content.
- Automated standards discovery from all jurisdictions, a registered multi-user GitHub/Canvas OAuth deployment, and automatic live bank assembly are not represented as completed features.

## Validation

- 410 unit/regression tests passed locally and in the source-validation workflow, including explicit SQLite handle cleanup.
- Source GUI workflow checks passed with no captured callback errors.
- Dependency audit: 41 dependencies, zero known vulnerabilities reported.
- The new Windows interface passed from both source and the packaged executable: navigation, Light/Dark at 100/125/150% scaling, Canvas browsing with a simulated service, question mapping, private diagnostic delivery, cancellation of cleanup, Classic restart, and shutdown. No callback errors were captured.
- Native installation and reinstallation passed the complete legacy workflow checks with no captured callback errors. The installed version 8 app opened the existing fictional workspace, preserved its blueprints, grades and attendance, created its recovery copy, and enabled the regular updater.
- The first rollback stress-test run stopped with a native access violation inside the unchanged 7.6.2 executable while exercising a temporary test database. The upgraded workspace had already passed preservation checks. A clean installation of the same published 7.6.2 binary reached its final curve-dialog checks and failed a dialog assertion instead; it did not reproduce that native crash. This control run establishes an independent old-version stress-test failure, not the cause of the first crash. The unchanged code passed the full native repeat: installation, reinstallation, in-place upgrade, signed rollback to 7.6.2, the old executable's complete stress checks, forward upgrade to 8.0.0, and uninstall/data preservation. This passing repeat is not a root-cause fix for the earlier failures. The unresolved old-executable failures are tracked in [source issue #3](https://github.com/ZacharyMeador/classroom-studio/issues/3). Classic navigation within version 8 avoids needing an executable downgrade.

The classroom builder comparison changes only `SeatingStudioApp.__init__` and `_make_ui` for navigation injection. The room editing and seating methods are unchanged. Core and suite schema versions remain 8 and 7; integration storage is additive.

## Published build identity and evidence

- Tested source commit: `207509f97c103cdf99a9faa8fc01f6f368c754f8`. Subsequent report and diagnostic-workflow commits do not change application code.
- [Successful Windows build and verification, attempt 2](https://github.com/ZacharyMeador/classroom-studio/actions/runs/45438473114/attempts/2).
- [Source validation and dependency audit](https://github.com/ZacharyMeador/classroom-studio/actions/runs/45438492569).
- Installer: `ClassroomStudio-Setup-8.0.0.exe`; 66,201,866 bytes.
- SHA-256: `932dbbc0442db568816b3c95b17410be6b9d1660d223432c55931a84553921af`.
- The signed `update.json` was verified against the existing trusted public key, then its size/checksum were checked against this exact installer. Channel: `stable`; platform: `windows-x64`.
- [Machine-readable verification results](verification_8_0_0/) include the successful native lifecycle, source/packaged UI results, dependency audit, and both earlier old-version failures. All workflow fixtures are fictional.

The installer does not yet carry an Authenticode publisher certificate. Manifest signing and Authenticode are separate mechanisms. For familiar navigation, prefer Classic within 8.0.0; the 7.6.2 rollback passed the full repeated run, but its earlier stress-test failures remain open in issue #3.
