# Importing assessment evidence in Classroom Studio 7.6.0

## First import

1. Create or select a class, then open **Assessments → Import assessment data → Add reports**. You can select several CSV/XLSX reports together. For the tracker workbook, choose the student worksheet, not the cut-score reference/image sheet.
2. District files open **Review assessment data**. Each source class and populated tracker assessment gets a row. Select one or several compatible rows and choose **Assign selected**.
3. Choose **New assessment / form** for a new destination, or explicitly choose an existing/prepared destination. Enter the assessment name and form (for example, Unit 2 / Regular), choose the class, and confirm subject and standards edition. Geometry defaults to the built-in **2023 SOL** reference. Course level is independent of period number.
4. Pair the question analysis with its matching assessment/form. If the same question report covers multiple prepared classes, choose **All prepared classes with this assessment/form**. **Duplicate destination** lets a source report be assigned to an additional destination when needed.
5. Assign or skip every row. Choose **Review import**. Read the class assignments, student identity proposals, and conflict list. IDs take precedence; exact names within a class are proposals. No fuzzy matches are applied. If a student link is wrong, cancel and correct/link the roster identity before retrying.
6. **Review conflicts** lets you select individual fields and choose Keep existing or Use incoming. Keeping export precision is normally appropriate when the tracker contains rounded values. Blank values never erase scores. Choose **Import reviewed data** only after reviewing the mappings. A recovery copy is created before saving the batch.

Question reports can be imported before student results. Add the student results later through the same button and explicitly select the existing imported assessment. Reimporting into that destination preserves the question/form identity. Choosing New intentionally creates a separate assessment.

## Pairing the supplied Geometry workbooks

The following pairings are supported by the contents and tracker comparisons. The exports do not carry a reliable assessment title, so confirm the intended titles/forms in the review rather than relying on the generic filenames.

| File | Contents | Suggested destination |
|---|---|---|
| `grid_data(1).xlsx` | 52 student rows, 25 item percentages | Unit 2 / Regular; map Period 1 and Period 3 separately |
| `grid_data (2)(1).xlsx` | 25 question statistics and standards | Unit 2 / Regular; both prepared classes |
| `grid_data (4)(1).xlsx` | 23 student rows, 25 item percentages | Unit 2 / Honors; Period 4 |
| `grid_data (5)(1).xlsx` | 25 question statistics and standards | Unit 2 / Honors |
| `grid_data (6)(1).xlsx` | 23 student totals, no individual item scores | MP 1 Benchmark / Honors; Period 4 |
| `grid_data (7)(1).xlsx` | 30 question statistics and standards | MP 1 Benchmark / Honors |
| `grid_data (8)(1).xlsx` | 52 student rows, totals/status only | MP 1 Benchmark / Regular; map Period 1 and Period 3 separately |
| `grid_data (9)(1).xlsx` | 25 question statistics and standards | MP 1 Benchmark / Regular; both prepared classes |
| `Geometry Data Tracking 26-27.xlsx` | 79 actual students; Unit 1, Unit 2, MP 1 Benchmark populated | Map classes `1`, `3`, `4`; create Unit 1 destinations and select the prepared/existing Unit 2 and benchmark destinations |

The tracker contains names without permanent IDs. Eight tracker names and four export names have no exact counterpart across the supplied files. Do not assume those are twelve additional people or accept guessed matches. Review them against the roster. Importing all unmatched rows as new records produces 83 local identities in the validation workspace; that count is not a claim about the number of unique real students.

## Reading the results

- **Overview:** reported/course total, completion status, mean, median, missing counts, threshold counts, and available item evidence.
- **Standards:** Class summary or a selected student. Student mean uses individual evidence. Source item mean is the question report's cohort-wide statistic and can include multiple classes. The benchmark files above support the latter, not individual student standards results.
- **Progress:** choose an earlier assessment. Only matched identities with scores on both sides contribute to the overall paired change. Repeated-standard changes require compatible course/edition and individual item evidence. Set assessment dates or order in Report settings; workbook column order does not determine latest.
- **Compare:** compare the same named assessment across classes/forms, or optional subgroup fields. Unknown classifications remain separate. Differences are descriptive and are not adjusted for test difficulty.
- **Report settings:** configure thresholds, the district/course benchmark (75% default), date/order, course level, Strength, Grow, and next instruction.
- **Export summary:** summary PDF by default; optional student-detail CSV. CSV details contain names/IDs and are intended for local use. Small subgroup breakdowns are omitted from the PDF.
- **Publish grades:** previews reported overall percentages against a selected gradebook assignment. Item percentages are not converted into fabricated point maxima; unfinished/missing totals do not overwrite a manual grade.

## Existing Canvas workflow

Use the same Import assessment data button. Select Canvas question and student reports together, or load question reports first and return with student results later. Reorder question reports to control numbering. Distinct new bank ItemIDs continue after the highest Q label; existing ItemIDs keep their labels. A bank item's label is not a student's shuffled question position. Canvas and district files use separate batches through this same entry point.

## Returning to a familiar view or version

- **Settings → Experience & features → Assessment overview first:** turn this off to start Canvas/manual results in Scoring charts. All views remain available. District percentage reports use the new evidence views because old point charts cannot represent them correctly.
- **Settings → Updates & about → Install an earlier version:** use the 7.5.5 installer and its own matching signed `update.json`. New district/tracker records are retained but their analysis is hidden until you return to 7.6.0. A recovery backup precedes installation. Earlier versions are blocked when district evidence is present.
- Restoring a pre-import backup replaces the workspace with that earlier snapshot and excludes subsequent work; it is different from changing the app version.
