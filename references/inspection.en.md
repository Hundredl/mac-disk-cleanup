# Inspection Notes

[简体中文](inspection.md) | English

Choose methods that fit the current scope; a full-disk scan is not required every time. Use verified paths and quote command arguments correctly so a filename cannot become shell code.

## Space and performance measurements

- `df -k /System/Volumes/Data` reports the data volume's currently available space. Record the raw output, time, and units. System Settings may include purgeable space in its available-space figure; do not mix these measurements.
- `du -sk <exact-directory>` measures allocated blocks. Check its exit status and stderr. When part of the directory is unreadable, label the measurement incomplete rather than presenting it as an exact total.
- For cloud storage, iCloud, NAS volumes, and sparse files, use locally allocated blocks and file state. Do not read placeholder contents just to verify size and trigger bulk downloads. APFS clones, snapshots, compression, and hard links also affect reclamation.
- For a slowdown, consider `sysctl vm.swapusage`, `sysctl kern.memorystatus_vm_pressure_level`, `uptime`, and brief process samples. Commands or fields may be unavailable on some systems. Accumulated swap, a CPU snapshot, basic SMART status, or one memory-pressure reading cannot alone prove a sustained performance or hardware problem.

## Large items that file-size searches miss

Start with application directories, user and system caches, Application Support, containers, Downloads, identified development workspaces, and Trash. CacheStorage, WebStorage, updater payloads, old program versions, and build artifacts can contain many small files. Searching for large individual files does not replace directory measurements.

For a broad investigation, inspect metadata in stages to limit the investigation's own disk and memory pressure. Prefer rg to find records or configuration for identified projects. Do not follow symlinks onto other volumes or read unrelated personal content.

## Evidence needed for different candidate types

| Type | Verify | Do not assume |
|---|---|---|
| Uninstall leftovers | Application removal, bundle ID, related services, and the path's purpose | A missing app permits deleting all shared directories from its vendor |
| Browser/Electron caches | Cache boundaries versus account databases, required offline content, relevant processes | CacheStorage cannot contain wanted offline content; browser cleanup includes its account Profile |
| Old extensions/program packages | Obsolete markers, version inventory, current entry points, running executables | An older version is unused; a historical candidate still exists |
| Development caches/artifacts | Lockfiles, source location, running builds, manual edits inside dependencies, offline needs | Every node_modules, target, registry, or pkgs directory can be wiped |
| Conda | Current clean dry-run, registered environments, links into caches, signs of custom environments | A clean preview permits deleting the entire pkgs directory or using force-pkgs-dirs; registered environments cover every custom environment |
| Model caches | Model files versus tokens/configuration, tool dependencies, redownload conditions | Everything under a cache path is a downloadable model |
| Games | Actual title, app ID, install directory, saves and Steam userdata | The folder name identifies the game; uninstalling includes deleting saves |
| Ebooks/personal files | Corresponding copies, file sets, content verification, source changes | Matching names, titles, or similar sizes prove a complete archive |
| Trash | Current contents and whether they match the reviewed batch | It is acceptable to empty all user or administrator Trash |
| Time Machine/APFS | Snapshot type, exact identifier, rollback purpose, native management method | System update snapshots are Time Machine snapshots; snapshot size and purgeable space can be added together |
| System icons/voices/models/indexes | Current system mechanism, native controls, active use, protection state | A historical rm command is universally safe; unreadable data can be deleted |

## Tools and permissions

Prefer local tools and an application's own controls. For unfamiliar behavior, check current official documentation or local help/man pages. Forum posts can suggest leads, but they do not establish a safe scope. System and application cleanup interfaces can change between versions.

Without Full Disk Access or administrator rights, report completed coverage and specific blocked paths; request access through the current environment when needed. After access is granted, revisit those paths rather than continuing to report historical access errors as current unknowns. If normal authorized deletion is rejected by the system, do not modify SIP or protected flags to reach a space target.
