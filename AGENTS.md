# Command layout

- Expose each action as `bin/peace-<action>`; symlink shared implementations from `lib/`.
- Keep `bin/peace-theme` as a dispatcher to those same entries, with working `--help` in both forms; reserve `peace` for the Omapeace plugin.
- Keep the dispatcher help and README examples current when actions change.
- The installer discovers executable `bin/peace-*` entries; the uninstaller removes only links resolving to this theme.
