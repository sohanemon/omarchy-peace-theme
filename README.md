# Peace Omarchy Theme

![Peace theme preview showing an ayah rendered in Amiri](assets/ayah-1.png)
![Neovim](assets/nvim.png)

![Lazygit](assets/lazygit.png)

## Backgrounds

Peace rotates the ayah wallpaper periodically while Peace is the active Omarchy theme: it runs one minute after login, then every three hours and one minute. The installer also generates the first wallpaper immediately. Each refresh needs an internet connection to fetch the verse from [AlQuran Cloud](https://api.alquran.cloud).

The Arabic Uthmani text is served by AlQuran Cloud as `quran-uthmani`; AlQuran Cloud says its text sources include [Tanzil](https://tanzil.net/) and [Quran Academy](https://quranacademy.io/). The English translation is Saheeh International (`en.sahih`), as identified in [AlQuran Cloud's API client documentation](https://alquran.cloud/api-clients).

The theme also includes these static backgrounds:

| Pattern | Glow | Minimal |
| --- | --- | --- |
| ![Dark green geometric pattern background](backgrounds/01-pattern.png) | ![Dark background with a soft gold glow](backgrounds/02-glow.png) | ![Minimal dark background](backgrounds/03-minimal.png) |

## Wallpaper controls

Choose a random ayah, or move to the next or previous ayah from a terminal:

```bash
peace random
peace next
peace prev
```

Run `peace --help` to see all commands. `peace wallpaper --help` shows renderer options such as `--pool`, `--ref`, and `--out`. Use `peace status` to inspect listening playback and `peace logs` to inspect wallpaper rotation. Run `peace enable` or `peace disable` to control its timer.

Each action is also available as a standalone command: `peace-listen`, `peace-pause`, `peace-stop`, `peace-status`, `peace-random`, `peace-next`, `peace-prev`, `peace-wallpaper`, `peace-init`, `peace-uninstall`, `peace-logs`, `peace-enable`, and `peace-disable`. Each standalone command has its own `--help` output.

To use `Super + Alt + P` and `Super + Alt + N` in Hyprland, add an optional user binding file at `~/.config/hypr/bindings/peace-wallpaper.lua`:

```lua
o.bind("SUPER + ALT + P", "Previous ayah", "peace prev")
o.bind("SUPER + ALT + N", "Next ayah", "peace next")
```

Omarchy loads Lua files from this user bindings directory. It removes Lua files from third-party theme installs for safety, so add these bindings to your own Hyprland config. The installer creates the initial ayah state, after which next and previous are available.

## Listening

Play a surah, one ayah, or an ayah range in order:

```bash
peace listen 55
peace listen 55:5
peace listen 55:5-10
peace listen 55:5-
peace listen 55 --follow
peace listen
peace listen 55:1-20 --follow --buffer 6
peace listen 112 --reciter ar.husary
PEACE_RECITER=ar.alafasy peace listen 1
peace pause
peace stop
peace status
peace wallpaper next
peace help
```

Listening requires `mpv`, `socat` for pause/status/follow, and internet access to AlQuran Cloud. `--reciter ID` overrides `PEACE_RECITER` (default `ar.alafasy`). `--follow` pre-renders ayah wallpapers in the background and switches to the current ayah without delaying audio. `--buffer N` sets the number of upcoming ayat to prepare (1–20, default 10).

## Install

Install the theme and wallpaper rotation on a new Omarchy device with one command:

```bash
omarchy theme install https://github.com/sohanemon/omarchy-peace-theme.git && "$HOME/.config/omarchy/themes/peace/bin/peace" init
```

Omarchy installs and activates the theme under `~/.config/omarchy/themes/peace`. `peace init` checks wallpaper requirements, installs the bundled Amiri font and available `peace-*` commands, then enables the wallpaper timer. Listening additionally requires `mpv`; `socat` enables pause, status, and follow controls.

### Requirements

Wallpaper timer hard requirements checked by the installer:

- `curl` — `omarchy pkg add curl`
- `jq` — `omarchy pkg add jq`
- `awk` — `omarchy pkg add gawk`
- ImageMagick `magick` with the Pango delegate — `omarchy pkg add imagemagick`
- Fontconfig tools (`fc-cache`, `fc-list`, `fc-match`) — `omarchy pkg add fontconfig`
- A working `systemctl --user` session
- `mpv` for listening (`omarchy pkg add mpv`); missing `mpv` does not prevent wallpaper timer setup
- `socat` for listening controls, status, and wallpaper follow (warning only)

Internet access to `api.alquran.cloud` is required each time an ayah is rendered.

DejaVu Serif and DejaVu Sans are optional font warnings; install them with `omarchy pkg add ttf-dejavu`. Amiri is bundled. The renderer uses the system's Amiri Quran family when present and otherwise falls back to Amiri.

To apply the theme again later, run:

```bash
omarchy theme set peace
```

## Uninstall

Switch to another installed theme before removing Peace, then run the master command:

```bash
peace stop
omarchy theme set "Tokyo Night"
peace uninstall
rm -f ~/.local/bin/peace
```

`peace uninstall` disables the timer, removes the installed commands and bundled font, then removes the theme through Omarchy. It leaves `~/.config/omarchy/backgrounds/peace/` intact, preserving personal backgrounds.

## License and text credits

This project's code is MIT licensed; see [LICENSE](LICENSE). The bundled Amiri font is separately licensed under the SIL Open Font License 1.1; its required notice is in [`fonts/OFL-Amiri.txt`](fonts/OFL-Amiri.txt) and is installed alongside the font. Quran text and translation credits are listed above.
