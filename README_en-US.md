# Cat Cursor (Linux)

English | [中文](./README.md)

## About

- **Original Author**: [Bilibili @HappyCadogt](https://space.bilibili.com/406949928)
- **Contributors**: [@Tseshongfeeshur (Ryan)](https://github.com/Tseshongfeeshur/cat-cursors) (initial Linux port), this project (V1.4 update + multi-resolution build)

Based on Ryan's [cat-cursors](https://github.com/Tseshongfeeshur/cat-cursors) initial port. Synced with the original author's V1.4 update and extended to support 12 resolution sizes (8–64 px).

## Contents

- Designed by [**HappyCadogt**](https://space.bilibili.com/406949928)
- Source version: **V1.4** (Windows `.ani`/`.cur` files)
- **All** cursors are animated
- Supports **8 / 12 / 16 / 20 / 24 / 28 / 32 / 36 / 40 / 48 / 56 / 64** pixel sizes

## Supported Platforms

- All [GNU](https://www.gnu.org/)/[Linux](https://kernel.org/) desktop environments supporting [XDG cursor themes](https://specifications.freedesktop.org/icon-theme/latest/)
- Tested and working on [Hyprland](https://hyprland.org/) and KDE Plasma

## Installation

### Per-user

```bash
git clone https://github.com/<your-repo>/catcursor_linux.git
mkdir -p ~/.local/share/icons/
cp -r catcursor_linux/猫标 ~/.local/share/icons/
```

Or directly into `~/.icons/`:

```bash
git clone https://github.com/<your-repo>/catcursor_linux.git
mkdir -p ~/.icons/
cp -r catcursor_linux/猫标 ~/.icons/
```

### System-wide (requires root)

```bash
sudo mkdir -p /usr/share/icons/
sudo cp -r 猫标 /usr/share/icons/
```

## Applying

### Hyprland

```bash
hyprctl setcursor "猫标" 24
```

Or in `~/.config/hypr/hyprland.conf`:

```conf
exec-once = hyprctl setcursor "猫标" 24
```

### GNOME

```bash
gsettings set org.gnome.desktop.interface cursor-theme "猫标"
gsettings set org.gnome.desktop.interface cursor-size 24
```

### KDE Plasma

Navigate to **System Settings → Appearance → Cursors**, select "猫标".

### Other Environments

Set `XCURSOR_THEME` and `XCURSOR_SIZE` environment variables:

```bash
export XCURSOR_THEME="猫标"
export XCURSOR_SIZE=24
```

Add to `~/.profile` or `~/.xprofile` for persistence.

---

## Replacement Parts

The original V1.4 package includes **alternative "link click" cursor animations** (`hand2`). When the default style feels stale, swap it out.

### Available Replacements

| File | Frames | Description |
|---|---|---|
| `Link（1）.ani` | 94 frames | Catfish-themed click animation |
| `Link（2）.ani` | 60 frames | Alternative click animation (current default) |

Replacement source files are in the `替换件/` directory.

### Usage (Linux)

Install dependencies:
```bash
pip install win2xcur Pillow
# System packages (Arch): sudo pacman -S xcur2png xcursorgen
```

Example using Link（1）:

```bash
# 1. Convert .ani to XCursor
win2xcur 替换件/Link（1）.ani -o /tmp/replace/

# 2. Extract frames and rebuild at 12 sizes (8–64 px)
python3 build-multi-cursor.py --single /tmp/replace/Link（1） --output hand2

# 3. Overwrite hand2 in the theme
cp hand2 ~/.local/share/icons/猫标/cursors/hand2

# 4. Reload
hyprctl setcursor "猫标" 24
```

Switch back to default Link（2）:
```bash
git checkout 猫标/cursors/hand2
hyprctl setcursor "猫标" 24
```

---

## Building from Source

To build the Linux version from Windows source files (`.ani`/`.cur`):

```bash
pip install win2xcur Pillow
```

See `build-multi-cursor.py` for the full pipeline:

1. `win2xcur` converts `.ani`/`.cur` to single-size XCursor
2. `xcur2png` extracts frames
3. PIL resizes to target sizes
4. `xcursorgen` builds multi-size XCursor
5. Create alias symlinks + `cursor.theme` / `index.theme`

Project source files are in `工程文件/` — PNG frames for all cursor variants, suitable for derivative works.

---

## File Structure

```
猫标/
├── cursor.theme
├── index.theme
└── cursors/
    ├── left_ptr          # Default arrow
    ├── left_ptr_watch    # Working in background
    ├── wait              # Busy
    ├── cross             # Precision select
    ├── xterm             # Text select
    ├── pencil            # Handwriting
    ├── circle            # Unavailable
    ├── hand2             # Link select
    ├── question_arrow    # Help
    ├── bottom_side       # Vertical resize
    ├── left_side         # Horizontal resize
    ├── bottom_left_corner
    ├── bottom_right_corner
    ├── move              # Move
    ├── dotbox            # Alternate
    └── right_ptr / ...   # Symlink aliases
```

## Credits

- **Original author** [**HappyCadogt**](https://space.bilibili.com/406949928) — without their work, this project would not exist
- [@Tseshongfeeshur](https://github.com/Tseshongfeeshur) — initial Linux port
- `win2xcur` + `xcursorgen` — cursor conversion and multi-resolution building
- `xcur2png` — frame extraction and debugging
