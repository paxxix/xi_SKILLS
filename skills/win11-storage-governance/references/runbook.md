# Local drive audit and cleanup runbook

## 1. Confirm the target

Record the user-named drive letters, readiness, volume label, filesystem, total/free capacity, and whether each is fixed, removable, network-backed, or mounted. If system APIs cannot confirm a property, report it as unknown. Never infer drive purpose from D:/E: alone.

## 2. Audit read-only

Start with volume totals and a root-level listing, capped (for example, at 500 entries or 30 seconds). Do not recursively scan a whole volume by default. If size estimates are needed, scan only relevant named folders, skip reparse points, protected/system-managed folders, and other volumes, and use a bounded depth/time or entry limit. Report when a scan is partial and record access errors; never present a partial total as exact. If a folder was not scanned, label its size unknown; if a scan hit its limit, label the result partial. Use metadata before reading file contents. Drill down only into large or ambiguous folders relevant to the request. Avoid opening personal documents.

For each finding record:

| Field | Record |
|---|---|
| Location | Exact drive and folder, with sensitive names minimized in the report |
| Size | Measured, estimated, or unknown |
| Category | Windows, application, cache, project, media, backup, personal, unknown |
| Confidence | High, medium, or low, with the evidence |
| Recommendation | Supported cleanup, migrate/configure, investigate, or leave alone |

## 3. Present a bounded plan

Show likely space recovery as an estimate, separate safe supported cleanup from uncertain candidates, and name the exact tool or path. Prefer Windows Storage settings / Disk Cleanup for eligible system files and the owning application's cache or library settings for app data. Do not promise that old, duplicate-looking, or large files are unnecessary.

## 4. Make changes only within approved scope

The user's request to clean a drive authorizes a scoped audit, not deletion. Present one consolidated preview of exact categories/paths and estimated recovery, then wait for explicit approval before removing anything, including clearly regenerable caches. For ambiguous or personal candidates, ask the user to select the items; silence is not approval. Use a reversible move/quarantine when practical; do not create automation unless separately requested. Never empty a Recycle Bin or remove Windows cleanup categories without including them in the approved preview.

## 5. Verify and report

Recheck free space and the owning application's behavior. Report paths/categories changed, space reclaimed, errors, what was left untouched, and recovery/rollback options. Do not claim success based only on command completion.
