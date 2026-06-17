# open

Smart file opener — dispatches files and directories to different programs based on type.

## Features

- **Type-aware dispatching**: Opens video, audio, image, and text files each with their own configured program.
- **Special keywords**: `music` launches your music player, `wifi` opens your WiFi manager.
- **Configurable**: Edit `~/.config/open/open.toml` to set your preferred programs for each type.
- **Sensible defaults**: Works out of the box with common terminal tools (termusic, mpv, nvim, yazi, etc.).

## Installation

```bash
# Make it executable
chmod +x open

# Copy to somewhere in your PATH
cp open ~/.local/bin/open
```

## Usage

```bash
open <music|wifi|path>
```

### Special keywords

| Keyword | Action              | Default    |
| ------- | ------------------- | ---------- |
| `music` | Launch music player | `termusic` |
| `wifi`  | WiFi manager        | `nmtui`    |

### File types

| Type      | Handler              |
| --------- | -------------------- |
| Directory | `yazi`               |
| Video     | `mpv`                |
| Audio     | `mpv`                |
| Image     | `kitty +kitten icat` |
| Text      | `nvim`               |
| Default   | `xdg-open`           |

## Configuration

On first run, a config file is created at `~/.config/open/open.toml` with the defaults shown above. Edit it to use your preferred programs:

```toml
# ~/.config/open/open.toml

# Special keywords
music = "spotify-tui"
wifi = "iwgtk"

# Directory handler
directory = "lf"

# MIME-type handlers
video = "vlc"
audio = "audacious"
image = "nsxiv"
text = "helix"

# Fallback for unknown file types
default = "xdg-open"
```

Handlers can include arguments (e.g., `kitty +kitten icat`).

## Examples

```bash
open ~/music/playlist/     # Opens in yazi (file manager)
open video.mp4             # Opens in mpv
open photo.png             # Opens in kitty image viewer
open document.md           # Opens in nvim
open music                 # Launches termusic
open wifi                  # Opens nmtui
```

## Dependencies

| Program                          | Used for               |
| -------------------------------- | ---------------------- |
| Python 3.11+ (for `tomllib`)     | Runtime                |
| `termusic` / `mpv` / `nvim` / `yazi` | Default handlers (configurable) |

## License

Public domain / do whatever you want.
