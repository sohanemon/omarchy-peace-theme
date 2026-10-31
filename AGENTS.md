# Command layout

- Expose this theme's lifecycle and timer actions as `bin/peace-<action>`; symlink shared implementations from `lib/`.
- Keep `bin/peace-theme` as a dispatcher to those same entries; reserve `peace` wallpaper and playback commands for the Omapeace plugin.
- Keep dispatcher help and README examples current when theme actions change.
- The installer discovers executable `bin/peace-*` entries; the uninstaller removes only links resolving to this theme.
