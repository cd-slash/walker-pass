# walker-pass

A [Walker](https://github.com/abenz1267/walker)-based frontend for [pass](https://www.passwordstore.org/) (the standard Unix password manager).

Designed for [Omarchy](https://github.com/basecamp/omarchy) and other Wayland desktops using Walker as the application launcher.

![walker-pass demo](https://github.com/cd-slash/walker-pass/assets/demo.gif)

## Features

- Fuzzy search through all your pass secrets
- Copy password to clipboard with auto-clear (default 45 seconds)
- Optionally pick which field to copy (password, username, url, etc.)
- Type password directly using wtype
- Native Walker dmenu integration — looks and feels like your other Walker menus

## Dependencies

- [pass](https://www.passwordstore.org/) - the password manager
- [Walker](https://github.com/abenz1267/walker) - the application launcher
- `wl-copy` / `wl-paste` (from `wl-clipboard`) - Wayland clipboard utilities
- `wtype` - for the `--type` option
- `notify-send` (from `libnotify`) - for notifications

On Arch/Omarchy:
```bash
sudo pacman -S pass wl-clipboard wtype libnotify
```

## Installation

```bash
# Clone the repo
git clone https://github.com/cd-slash/walker-pass.git

# Copy to your local bin
cp walker-pass/walker-pass ~/.local/bin/
chmod +x ~/.local/bin/walker-pass
```

## Setup pass

If you haven't already set up pass:

```bash
# Generate a GPG key (if you don't have one)
gpg --full-generate-key

# Initialize pass with your GPG key
pass init your-email@example.com

# Add some secrets
pass insert api/openai
pass insert api/anthropic
pass insert services/github
```

## Usage

```bash
# Pick a secret and copy password to clipboard
walker-pass

# Pick a secret, then pick which field to copy
walker-pass --show

# Pick a secret and type the password (useful for terminals)
walker-pass --type
```

## Keybinding

Add to your Hyprland config (e.g., `~/.config/hypr/bindings/utilities.conf`):

```bash
bind = $mainMod SHIFT, P, exec, walker-pass
bind = $mainMod SHIFT ALT, P, exec, walker-pass --show
```

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `PASSWORD_STORE_DIR` | `~/.password-store` | Location of your pass store |
| `PASSWORD_STORE_CLIP_TIME` | `45` | Seconds before clipboard auto-clears |

## Pass Entry Format

walker-pass expects the standard pass format:

```
mysecretpassword
user: myusername
url: https://example.com
email: me@example.com
```

The first line is always the password. Additional fields use `key: value` format.

## License

MIT
