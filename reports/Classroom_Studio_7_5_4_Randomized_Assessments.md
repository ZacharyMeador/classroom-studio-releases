# Classroom Studio 7.5.4 — randomized Canvas assessments

## Problem and change

Canvas New Quizzes exports contain the union of bank items seen across students. The previous importer skipped blank scores but ignored item status: percentages could be correct while completion and practice readiness compared each student with the entire bank. The score editor also offered items the student never received. Item metadata imports ignored PossiblePoints.

The new importer records assignment status separately from scores, keyed by student and Canvas ItemID. Repeated titles and reordered columns do not merge questions. Metadata confirms the actual per-item maximum and preserves scores. Completion, section counts, FRQ counts, publish previews and AP practice checks use the student's assigned items. Question charts display graded-response counts; standards/skill charts show assessed-student counts. Exports include these counts and item IDs.

## Status handling

| Canvas status | App behavior |
|---|---|
| Graded | Import numeric points, including zero and partial credit. Blank points preserve prior scores and otherwise remain pending, with a warning. |
| Not Attempted | Question was not included. Exclude from grading, completion and denominators. |
| No Answer | Assigned but unanswered. Count as zero. |
| Not Graded | Assigned and pending; preserve any existing teacher-entered score. |
| Not Supported / N.A. | Assigned; warn that results need review. Do not invent a grade. |
| Unknown or contradictory status/points | Reject the entire import. |

Reference: [Instructure — New Quizzes reports](https://community.instructure.com/en/kb/articles/661090-how-do-i-view-reports-for-a-quiz-in-new-quizzes).

## Validation against the supplied exports

Only aggregate verification results are stored here. Student names, IDs, responses, scores and original CSVs are not committed.

| Part | Students | Distinct items represented | Questions per student | Graded responses | Not included |
|---|---:|---:|---:|---:|---:|
| Non-calculator | 17 | 30 | 12 | 204 | 306 |
| Calculator | 17 | 27 | 4 | 68 | 391 |
| Combined | 17 | 57 | 16 | 272 | 697 |

Both files contain the same student IDs and disjoint question IDs. Every individual percentage matches Canvas OverallScore / PointsPossible. All students are Complete. All 57 metadata records match, maxima are confirmed at one point, tags import without warnings, and repeated imports preserve scores. Combined earned-point percentages match the sum of both parts divided by 16.

## Use

1. Create or select an assessment and import its Student Analysis report through Import scores.
2. Choose **More tools → Import item tags** and select the matching Quiz and Item Analysis report (this now imports points as well as tags). This supplies maximum points and topic/skill tags without typing them individually.
3. Repeat for the other part if combining these supplied files. Review results, then preview any transfer to the gradebook.

Different attempts cannot be merged into existing student/item records. Choose one attempt per student in the export, and put retakes in a separate assessment. An assigned question set that changes on reimport requires a separate assessment. This avoids combining answers from different random forms. Missing status in older exports preserves the previous manual/legacy behavior; those imports cannot identify unassigned bank items. Items without an explicit status record retain the legacy expectation that they apply to the roster; students omitted from an export stay pending. Use a complete Student Analysis export for exact per-student assignment counts.

Random forms are not statistically equated for difficulty. Per-question averages use only graded responses; standards percentages describe observed evidence, not complete coverage or an official mastery certification. No new official AP-score prediction is supplied.

## Revert and data protection

The first randomized import through the main app creates `recovery/before_randomized_assessments_<timestamp>.sqlite3` beside the workspace database, before changing roster or assessment data. Classic and individual interface preferences remain available.

Core schema 8 and suite schema 7 remain unchanged; the new eligibility table is additive. Older apps ignore it, so the updater blocks rollback below 7.5.4 when randomized assignments exist. A separate compatible pre-import backup can be restored for rollback, but excludes work done after that backup. Ordinary workspaces without randomized assignments retain the previously verified rollback path. Directly installing an old executable against newer randomized data is not a supported downgrade.

## Verification status

- Local static checks passed; 277 unit/integration tests passed with SQLite-handle cleanup enforcement.
- All supplied real exports passed local import/reimport and percentage reconciliation checks.
- Source CI passed all 277 tests, the full GUI workflow, static checks and the dependency audit (no known vulnerabilities reported). All seven new randomized-assessment GUI checks passed with no callback errors.
- Local GUI execution is unavailable because this session has no display server; GUI validation runs on CI. Native Windows verification passed: all 277 tests, installation and reinstallation with all seven randomized-assessment checks and zero callback errors, signed rollback to 7.4.2 on a compatible workspace, upgrade back, uninstall, and saved-database preservation. Randomized workspaces correctly block unsafe downgrade; their pre-import recovery copies are compatible.
- [Source verification](https://github.com/ZacharyMeador/classroom-studio/actions/runs/43915063479) · [Windows verification](https://github.com/ZacharyMeador/classroom-studio/actions/runs/43915063428).
- Application source commit: `6fdd16cc09b56e9fe6d3863b5b3aecf095c8aca6`.

## Release assets

The installer and signed update manifest were independently checked against the existing trusted public key.

- `ClassroomStudio-Setup-7.5.4.exe` — 63,262,242 bytes; SHA-256 `757c6350315b9c23d1512be95104a0b1788152b680029432ea99b7be0fe1f904`.
- `update.json` — 20,878 bytes; SHA-256 `7e675f7f9d90e6056b93feefe4de6fc2b28f2b83c87144bf39ea0c212231f60f`.

Verification evidence is in [`verification_7_5_4`](verification_7_5_4). The supplied-export checks contain aggregate counts only.
