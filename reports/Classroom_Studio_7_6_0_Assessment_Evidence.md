# Classroom Studio 7.6.0 — assessment evidence integration

[Import guide and supplied-file pairings](Assessment_Import_Guide.md).

## Behavior

Assessments has one Import assessment data entry. Canvas question/student reports retain the existing metadata-first, stable-ItemID workflow. District student reports, district question analyses, and a tracking workbook enter a shared batch review. A batch can cover multiple classes and assessment columns. Assign or explicitly skip every source row; existing/prepared destinations are explicit choices, never guessed from a filename. Question reports can be applied to every prepared class using the same assessment/form. Review lists roster proposals and conflicting values before Import commits the batch.

The destination is a class plus assessment plus form. Regular, Honors, calculator/non-calculator, or other distinct forms are never joined merely because they contain Q1. Permanent IDs drive identity; same-class exact names are reviewable proposals. Unmatched names remain separate, and contradictory IDs block importing. No fuzzy matching or hardcoded student lists are used.

Percent scores and source-reported totals are stored independently of the Canvas point model. No synthetic 100-point questions are created. Publishing explicitly previews the reported totals against the gradebook destination. Missing totals preserve manual gradebook values. Partial item evidence does not replace an official reported total with an average of the nonblank cells.

## Analysis and reporting

- Overview: reported/course percentages, mean, median, missing counts, status, score bands, configurable thresholds (60/70/75 by default), and individual item-evidence coverage.
- Standards: exact imported lettered codes and edition; individual student evidence and source-wide item statistics are separately labeled. District response summaries use equal item percentage weight; Canvas summaries use actual points. Multi-tagged item weight is divided across tags.
- Progress: pairs the same identities with scores on both assessments, reports percentage-point changes and paired evidence counts. Standards comparisons require the same course and edition. Latest is determined only by entered dates or order, never import order or worksheet column position.
- Compare: same-named assessments across classes/forms, course levels, and optional SWD, ELL, SOL Tester, grade/year, or source-section groups. Unknown is a separate category. Classifications remain local, optional, and assessment-specific.
- PDF summary: editable Strength, Grow, and next instruction; spiral-review warm-ups are the default next-step text. Student-detail CSV is optional. A subgroup breakdown is omitted entirely if any scored group has fewer than 5 students, avoiding subtraction from a visible total.

These are descriptive results. Different tests and randomized forms are not equated for difficulty; no official SOL/AP prediction is introduced. Source-wide question statistics may cover more than one class. A totals-only benchmark cannot support individual student standards estimates until detailed student-item evidence is supplied.

## Actual-file validation

The nine supplied workbooks were tested locally without copying them or any student records into either repository. The tracker has 79 actual students and 3 populated assessment columns. The eight exports comprise two detailed student-result reports, two totals-only reports, and four question-analysis reports.

The review identified 22 conflicting fields: 14 rounded benchmark scores, 6 SWD flags, and 2 ELL flags across the assessment destinations. Keeping existing export values preserves all nonblank source scores exactly, including genuine zeroes and fractional precision. Eight tracker-only names and four export-only names remain unresolved separate records; they are not guessed into a match. The validation workspace therefore has 83 reviewed identities across its three classes, not an asserted 83 unique real people. A teacher must review these first-time links before applying an import to a real workspace.

Completed district records with missing item cells are flagged. Question P-values stay source-wide aggregate percentages. The benchmark reports produce no invented student standards estimates. All input files remained unchanged. Aggregate evidence: [geometry-import-validation-7.6.0.json](geometry-import-validation-7.6.0.json).

## Recovery and return path

Each district/tracker commit creates a before_assessment_evidence recovery copy. A stale preview or failed file rolls back the entire batch, including roster changes. Blanks cannot erase saved values; nonblank conflicts default to Keep. Reimport into the same explicitly selected destination is idempotent.

Core/suite schema remains 8/7. New data lives in additive evidence/reporting tables. The verified return target for a workspace containing district evidence is 7.5.5; earlier targets are blocked. Version 7.5.5 retains this data but does not expose its analysis screens. Returning to 7.6.0 makes those screens available again. Restoring a pre-import backup is a different operation and excludes subsequent work.

Settings → Experience & features → Assessment overview first can be disabled to open Canvas/manual results in the familiar scoring charts. All analysis views remain available. Existing Classic/individual feature choices remain persistent.

## Additional regression findings

An explicitly blank source section now imports only that group, rather than all sections. Shared distributions include extra-credit totals in the 95+ band. Table text/spacing changes update table styles without retheming and rescaling all CustomTkinter canvases; selecting an already active native theme no longer resets it. This narrows an unnecessary redraw path found while investigating a native Windows access violation in a candidate build. The native smoke test records GUI resource counts by stage and checks the actual table font sizes.

## Verification status

- 317 unit/integration tests pass locally, including 27 new evidence regressions and strict SQLite-handle cleanup.
- Static fatal-error checks pass.
- Actual-workbook validation passes with aggregate evidence only.
- [Source verification](https://github.com/ZacharyMeador/classroom-studio/actions/runs/44132574210) passed: all 317 checks, full GUI workflows including the 9 new evidence checks, and dependency audit (27 packages; no known vulnerabilities found). [Saved evidence](verification_7_6_0/source-verification.json).
- [Native Windows verification](https://github.com/ZacharyMeador/classroom-studio/actions/runs/44132574358) passed: install and reinstall each ran the full GUI checks with no callback errors; signed rollback to 7.5.5, old-version reads of new records, upgrade after rollback, and data-preserving uninstall passed. The final candidate completed the appearance/scaling round trips without the earlier native crash. [Saved native evidence](verification_7_6_0/windows-verification.json).
- Downloaded release ZIP integrity, signed update manifest, installer hash/size, and portable-package privacy checks pass. [Asset verification and exact hashes](verification_7_6_0/asset-verification.json).
- Application code: `f267695a6b6777d6ae9e91f10c16677d50f930b0`. Report-only commits may follow this tested revision.

These checks cover the supplied imports and exercised workflows; they are not a guarantee that every future export format or classroom configuration is bug-free.
