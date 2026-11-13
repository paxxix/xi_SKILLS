---
name: win11-storage-governance
description: Use when investigating Windows 11 disk space or planning cleanup, storage migration, cache relocation, or maintenance on C:, D:, E:, other local volumes, or removable drives; including AppData, Windows Installer, WinSxS, WindowsApps/UWP, winget, Scoop, developer caches, browser profiles, NVIDIA caches, and recurring cleanup.
---

# Windows Storage Governance

Help free space while preserving user data. A drive letter or the label “data drive” does not prove that a volume is safe to clean. D: and E: may contain projects, libraries, backups, application data, or mounted/system-managed folders.

## Workflow

1. Establish scope: template only, read-only audit, or local cleanup. For local work, use only the drives the user named; never infer that “non-core” means disposable.
2. Read `references/safety-model.md` before deletion, migration, junctions, package-manager changes, or environment-variable changes.
3. Read `references/runbook.md` for a local audit or cleanup plan, and `references/device-profile-template.md` for reusable device profiles.
4. Inventory first. Report the target drive, volume label/type, free space, top-level space use, likely categories, confidence, and proposed actions before changing files.
5. Prefer supported Windows or application cleanup controls. Before any deletion, show one consolidated preview with exact categories/paths and estimated recovery, then wait for explicit approval of those categories. A general request to “clean the drive” authorizes the audit, not deletion; silence is not approval.
6. Verify reclaimed space and application behavior; provide rollback guidance for moves or configuration changes.

## Privacy and scope

- Do not inspect user profiles, AppData, registry, shell history, package-manager state, or project contents unless the user explicitly requests a local audit or cleanup.
- During an authorized audit, inspect only the named volume and only as deeply as needed. Avoid opening file contents; use metadata and folder sizes first.
- Begin with a root listing and volume totals. Bound enumeration (for example, 500 entries or 30 seconds); do not recursively scan a whole volume by default. Expand only into named candidates, skip reparse points and protected/system-managed folders, and label unmeasured sizes as unknown and interrupted scans as partial.
- Use neutral placeholders in reusable examples. Do not copy personal paths, names, logs, or file lists into templates.
- Do not create recurring or unattended deletion rules unless the user explicitly requests automation and approves a narrow allowlist, retention threshold, and recovery plan.

## Output contract

Classify findings as: safe clean, official-tool clean, migrate/configure, investigate, or do-not-touch. For each proposed action include the exact path/category, estimated space, reason, confidence, method, and recovery status. Distinguish measured results from estimates. See the referenced safety model and runbook.
