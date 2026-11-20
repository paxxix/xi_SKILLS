# Safety model for Windows storage

## Risk classes

- **Safe clean:** narrowly identified, reproducible temporary output with no user state; use the owning application's cleanup control where available.
- **Official-tool clean:** Windows components, Store apps, Visual Studio, drivers, or package-manager data that must be handled through their supported maintenance tools.
- **Migrate/configure:** user-selected libraries or regenerable caches that can be moved using application settings and verified afterward.
- **Investigate:** large or old files, unknown folders, installers, archives, downloads, project trees, backups, databases, media libraries, and application data.
- **Do-not-touch:** Windows servicing stores and protected/system-managed directories, including `C:\Windows\Installer`, `C:\Windows\WinSxS`, `C:\Program Files\WindowsApps`, `System Volume Information`, and active application or backup stores. Do not manually delete or junction these.

## Rules

1. Never treat D:, E:, a volume label, age, file extension, or size as proof that content is disposable.
2. Never recursively clear a drive, whole user folder, whole `AppData`, `ProgramData`, `Downloads`, application cache root, package cache, or recycle bin as a shortcut.
3. Never delete unknown files, personal documents, source trees, virtual machines, databases, backups, restore points, or application data without identifying the owner and purpose.
4. Before any deletion, show a consolidated preview list and expected space recovery, then wait for explicit approval of the listed categories/paths. A general request to clean a drive authorizes an audit, not deletion; silence is not approval. For ambiguous or personal files, obtain the user's selection.
5. Use quarantine or Recycle Bin only when it is supported for that file type and volume. For large or cross-volume moves, verify the destination and copy before removing the source.
6. Treat content as clearly regenerable only when its owning application or Windows maintenance tool identifies it as disposable, or when it is verified transient output with no user state. Examples may include an app's explicit “clear cache” action or a known build output that can be recreated from source. Age, `.tmp` extension, or a folder named `cache` is not sufficient evidence. Junction only a clearly regenerable cache after the application is closed, with a backup, tested path, and rollback steps. Do not redirect system-managed or user-state directories.
7. Do not use broad commands such as recursive force-delete against a drive root or an unverified variable. Keep commands constrained to a reviewed exact path.

## Recovery and verification

Record what was changed and how much space was freed. Verify the owning app, the target volume, and any migrated path. State whether recovery is available through Recycle Bin, backup, or application regeneration; if not, do not perform an ambiguous deletion.
