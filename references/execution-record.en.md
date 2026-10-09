# Execution and Records

[简体中文](execution-record.md) | English

## States and logging

Use stable candidate IDs. Distinguish at least: awaiting review, approved, retained, absent before execution, cleaned, partially cleaned, and deferred. Approval applies to a specific candidate version and scope. If a path is reused, content is unknown, its purpose changes, or backup arrangements change, record the discrepancy; do not transfer old approval to new content.

Execution records should include:

| Field | Purpose |
|---|---|
| Time, timezone, batch/candidate ID | Connect the timeline and distinguish stages involving similarly named items |
| Exact target and identity | Path, snapshot name, application/version, or a conditional file-selection rule |
| Authorization and retention boundaries | The user's actual decision and applicable candidate version; historical permissions do not grant new approval |
| Before-state | Existence, size/units/method, identity, active use, and before df measurement |
| Backup and verification | Whether a backup was required, its location, verification strength, source changes, and current recoverability |
| Action and per-item results | Method, exit status, exceptions, and actual subpaths touched; exclude passwords and credentials |
| After-state/verification | Target and retained-path checks, failures and unknowns, and after df measurement |
| Recovery and effects | Reinstallation, downloads, rebuild conditions, and content that cannot be restored from this batch |

Persist the plan and before-state first, then action and after-state item by item. Save logs in exception and finally paths as well. Do not keep all successful results only in memory until the batch finishes. Automation failures, partial removals, and fallback methods that change the original approach must leave factual records and evidence gaps.

Directory existence does not verify all retained content; a SHA-256 manifest is not a content backup. When the user requires a saved copy before removal, verify the file set, content or suitable integrity conditions, and that the source has not changed, then remove the source. For items without a backup, describe how content could be obtained again. When a backup is later deleted, retain its historical verification but mark its current availability as unavailable.

## Common false completion claims

- A dry-run did not execute the operation; a UI click only reached an intermediate screen; a failed command produced some success messages. Target and retention checks must support the claimed outcome.
- A directory removal stopped midway. Record removed subitems and residuals, continue other independent approved items, and do not claim the whole directory is gone.
- Applications regenerated caches. Distinguish removed old caches, newly generated caches, and data never removed; do not repeatedly chase active caches.
- Deleted audio-driver files may remain loaded in memory. Separate restart-dependent device changes from the immediate file-removal result; do not force a restart of audio services just to unload them.
- NAS/SMB reports a nonempty directory, or lists a file that unlink cannot find. Inspect actual residuals, open handles, and server behavior. Use bounded diagnosis/retries only for identified metadata inside the approved directory. Do not change global NAS settings or report partial success as complete deletion.
- Available space may not increase immediately. Snapshots, background writes, and shared blocks can retain space; do not repeat removals of already processed content based on this observation.

## Maintenance archives

Use a dated directory at the user's chosen location, organized with an overview, itemized records/evidence, troubleshooting leads, and a checksum manifest. Combine files when the record is small. Leave existing backups in place and add an index. Without a specified location, use an already authorized local workspace and report the actual path; do not choose an external cloud service without authorization.

Preserve the timeline: before cleanup, each batch, later backup deletion, and final verification. Do not overwrite historical evidence. Remove processed items from current candidate totals; list retained and deferred items separately. Read records back after saving to a NAS and accurately describe whether verification covered sizes, file sets, or content hashes.

Organize troubleshooting leads as symptom → actual related change → first checks → recovery conditions. Distinguish possible associations from confirmed failures. The next operator should capture the error text, version, reproduction steps, and restart/update timing before making a narrow repair. Record repair actions separately.

Share only general rules, synthetic examples, and necessary tools in a public skill. Personal maintenance reports, hardware identifiers, reading lists, accounts, NAS addresses, private paths, and historical deletion scripts are not published by default. A user's retention choices apply to their conversation, not as mandatory preferences for everyone.
