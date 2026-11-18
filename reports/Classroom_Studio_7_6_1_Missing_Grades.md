# Classroom Studio 7.6.1 — missing grades count as zero

- Missing gradebook entries automatically display, calculate, and export as zero. This applies to existing blanks, new assignments, and newly added students. Weighted category totals and assignment statistics follow the same rule.
- Combine assignments now includes missing work as zero while retaining earned points. An 8/10 plus a missing 20-point assignment produces 8/30. EX remains excluded; missing extra credit adds no penalty; Not for Grading remains excluded from totals.
- To repair an old combined result: open Gradebook → Grade editor, select its original assignments with Ctrl+click, choose Combine, then choose Replace for the existing combined assignment. Review Before/After and apply. Originals remain unchanged. The destination keeps its identity, Canvas link, due date, description, and existing maximum unless changed. Recovery copies and Undo are available.
- Old combined assignments did not store their source selection, so they cannot be reconstructed automatically. Select their originals to recover earned contributions. Original assignments continue to count in totals unless marked Not for Grading.
- The assessment analyzer still excludes randomized items a student never received. A blank incoming grade never overwrites an existing score. Automatic zero entries can receive actual scores on a later import without a false conflict.
- No database format change. Returning to 7.6.0 restores its previous missing-grade policy; repaired numeric combined grades remain saved.

## Cause and scope

The old Combine dialog defaulted to Leave blank. A single missing source entry blanked the entire combined score for that student. Original source assignments were preserved. Ordinary totals also excluded missing assignments, causing a separate inconsistency with a missing-work-equals-zero policy.

Raw absence is retained internally to distinguish an automatic zero from a teacher-recorded zero during safe imports. This is not a database-wide overwrite: gradebook display, calculations, reports, and exports resolve absence to zero. JSON workspace copies retain that distinction and reopen with zero behavior in 7.6.1. Clearing a normal grade therefore displays zero. No one-week deadline is scheduled by this release; the zero policy applies immediately to missing gradebook entries. Curve/bonus tools still modify recorded scores only.

## Additional release regression

A timing-sensitive reimport check exposed an unnecessary class-profile save. An unchanged roster now preserves its modification timestamp; a deterministic regression forces the old timestamp rather than relying on completing within one second. Actual roster additions still save normally.

## Verification

325 unit/integration checks and static checks passed locally and in source CI. All source GUI workflows passed, including seven missing-grade/repair checks, with no callback errors. The dependency audit reported no known vulnerabilities in 27 packages. Fixtures use fictional students only.

Native Windows installation and reinstallation passed all GUI workflows, including the seven missing-grade/repair checks, with no callback errors. Signed rollback to 7.6.0, upgrade after rollback, and uninstall with classroom-data preservation also passed. The downloaded build archive, installer checksum, and signed update manifest were independently verified before publication.

- Application source: `6662e1a33b06a1c930c0c532241802a3e5e6e9a1`
- [Source verification](https://github.com/ZacharyMeador/classroom-studio/actions/runs/44337499696)
- [Windows build and verification](https://github.com/ZacharyMeador/classroom-studio/actions/runs/44337499753)
- Installer SHA-256: `28da70801e1864c99854d71542bcbc10dfcde8aca426f52aa29ac8b7bbe4c13b`
- Signed manifest SHA-256: `ca4fe6809df61f371e46924a57c5bfe4ef21630db45054b06190bcfa3f38c2a1`
- Machine-readable evidence: [verification_7_6_1](verification_7_6_1/).

## Installation and recovery

The private release channel requires a signed-in GitHub download. Close Classroom Studio and install the 7.6.1 Setup over the existing installation. The installed application and classroom database are separate. No teacher records were accessed or modified while developing this fix.

For an application rollback, use the previous release's Setup and matching signed update.json with Settings → Updates & about → Install an earlier version. A database restore is a separate operation and would remove work saved after that backup. Repairing an existing combination first creates a local before_recombine recovery copy; immediate Undo restores the previous destination values.
