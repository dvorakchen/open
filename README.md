# open

Smart file opener — dispatches files and directories to different programs based on type.

## Features

- **Type-aware dispatching**: Opens video, audio, image, and text files each with their own configured program.
- **Special keywords**: `music`, `wifi`, `mail`, `im`, `cb` — launch apps or run pipelines with a single word.
- **Configurable**: Edit `~/.config/open/open.toml` to set your preferred programs for each type.
- **Sensible defaults**: Works out of the box with common terminal tools (termusic, mpv, nvim, yazi, etc.).

## Installation

```bash
# Make it executable
chmod +x open

# Copy to somewhere in your PATH
cp open ~/.local/bin/open
```

Requires Python 3.11+ (for `tomllib`).

## Usage

```bash
open <music|wifi|mail|im|cb|path>
```

### Special keywords

| Keyword | Action                | Default                                    |
| ------- | --------------------- | ------------------------------------------ |
| `music` | Launch music player   | `termusic`                                 |
| `wifi`  | WiFi manager          | `nmtui`                                    |
| `mail`  | Email client          | `aerc`                                     |
| `im`    | Instant messaging     | `iamb` (Matrix client)                     |
| `cb`    | Clipboard manager     | `cliphist list \| fzf \| cliphist decode \| copy` |

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
mail = "mutt"
im = "weechat"
clipboard = "cliphist list | fzf | cliphist decode | wl-copy"

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

Handlers can include arguments (e.g., `kitty +kitten icat`) or shell pipelines (e.g., `cliphist list | fzf | ...`). Pipeline commands are run through the shell; everything else is split with `shlex` and passed to `subprocess.run`.

## Examples

```bash
open ~/music/playlist/     # Opens in yazi (file manager)
open video.mp4              # Opens in mpv
open photo.png              # Opens in kitty image viewer
open document.md            # Opens in nvim
open music                  # Launches termusic
open wifi                   # Opens nmtui
open mail                   # Opens aerc
open im                     # Opens iamb (Matrix)
open cb                     # Opens clipboard manager (fzf pick → decode → copy)
```

## Dependencies

| Program                                   | Used for                        |
| ----------------------------------------- | ------------------------------- |
| Python 3.11+ (for `tomllib`)              | Runtime                         |
| `termusic` / `mpv` / `nvim` / `yazi`      | Default handlers (configurable)   |
| `aerc` / `iamb` / `cliphist` / `nmtui`    | Default keyword handlers         |

## License

[Apache License 2.0](LICENSE)
