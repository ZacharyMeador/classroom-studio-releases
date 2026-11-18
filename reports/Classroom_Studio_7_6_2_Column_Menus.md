# Classroom Studio 7.6.2 — column menus and reviewed curves

## What changes

Click or right-click an assignment title in the gradebook grid. The popup operates
on that column, including after filtering or horizontal scrolling. It contains
assignment settings (name, category, grading type, points, description, due date),
score editing, analysis, a curve submenu, bulk score entry, clear, combine,
duplicate, include/exclude, move left/right, export, Undo/Redo, and delete.
Unavailable actions are disabled. Shift+F10 opens the menu from the grid; a focused
header also supports arrow navigation and Enter/Space.

Combining explicitly asks which additional assignments to include before using the
existing combine/repair preview. A duplicate gets a fresh identity and no Canvas
assignment link, while retaining its scores. Original assignments remain intact.
Deletion and clearing are reviewed and recoverable. Clearing keeps EX excused;
ordinary missing entries continue to count as zero.

## Curve choices

Here, x is the old point score and M is the assignment maximum.

| Option | Calculation before caps/protection | Example on a 20-point quiz |
| --- | --- | --- |
| Add points to every score | x + b | 12 + 2 = 14 |
| Add percentage points | x + M × b / 100 | 12 + 20 × 5 / 100 = 13 |
| Multiply scores | x × factor | 12 × 1.1 = 13.2 |
| Scale highest score to target | x × (M × target% / 100) / highest eligible score | Highest 16; target 100%; 12 becomes 15 |
| Shift average to target | x + (M × target% / 100 − eligible mean) | Mean 12; target 75%; add 3 |
| Square-root curve | M × sqrt(x / M) | 5 becomes 10 |
| Custom linear curve | x × factor + b | 12 × 1.1 + 2 = 15.2 |

Header curves default to **All students**, ignoring search filters and previous
student selections. **Visible students** and **Selected students** are explicit
alternatives. Former students are included only when the gradebook's Include former
students option is on. The selected group and count appear in the configuration
and preview. Statistics for target curves use only eligible students in that group.

EX is always excluded. Flat and percentage bonuses initially **include zeros and
missing work**, so a bonus can apply to every non-excused cell. Other methods initially
**keep zeros at zero**. The teacher can change this choice. A missing entry is treated
as zero when included; an unchanged missing zero retains its import-safe distinction.
No randomized assessment item records are changed.

The default cap is the assignment maximum. **Keep higher scores** is also on by
default, so previously earned extra credit is retained even when above the cap.
Turn off that protection only when intentionally lowering grades. Scores cannot
become negative. Extra-credit columns offer raw points, multiplier, and custom
linear adjustments; percentage/statistical curves are disabled. Excluded assignments
must be included before curving. Assignment maxima and grading metadata never change.

Caps, zero protection, and keeping higher scores can prevent an exact target mean
or maximum. The Before/After preview is the actual result. Calculations round only
the final saved score to six decimal places. Applying another curve compounds the
result; Undo first to compare different methods against the original grades.

## Persistence and recovery

Curve changes are prepared on a copy. Cancel changes nothing. Applying creates a
`before_column_change` recovery copy and saves the complete draft before changing
the visible workspace or Undo history. Save/backup failures leave grades unchanged.
Undo/Redo persist through the existing gradebook workflow. Recovery copies remain
available after restart; Undo history is session-local.

No database format changes. Install 7.6.2 over the existing copy while the app is
closed. The private GitHub release requires a signed-in download. Settings → Updates
& about → Install an earlier version accepts the 7.6.1 Setup and matching signed
update.json. Reverting the app keeps saved curved scores; undo the curve first if
you want its original scores too. Database restoration is separate and replaces
work saved after the backup.

## Verification

341 unit/integration checks and static checks passed locally and in source CI. All
12 new source GUI checks passed with no callback errors. The dependency audit found
no known vulnerabilities in 27 packages. Native Windows installation, reinstallation,
and rollback checks are pending. New regressions
cover curve mathematics, percentage-vs-raw-points behavior, zero/EX policy, scopes,
invalid/overflow inputs, menu routing, filter independence, backup, cancellation,
failed saves, Undo/Redo, column actions, and dialogs at 100%, 125%, and 150% scaling.
All fixtures use fictional students. No classroom records were accessed or changed.

- Application source: `3b2092fa2c4960981aa88d5b516838d39904e127`
- [Source checks](https://github.com/ZacharyMeador/classroom-studio/actions/runs/44355252550)
- [Windows build](https://github.com/ZacharyMeador/classroom-studio/actions/runs/44355252429)
- [Machine-readable evidence](verification_7_6_2/).
