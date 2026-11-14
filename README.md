# No Bloat Dotfiles
My minimalistic and lightweight Hyprland config for Arch with NVIDIA support(incl. 580 devices if needed), in Catppuccin Mocha.
Config is in hyprland.lua, includes runtime hardware detection (display outputs, GPU driver, undervolt support)
instead of hardcoded values, so the same dotfiles port across different machines.
Laptop battery life is priority, so power tooling (tlp, power-profiles-daemon, intel-undervolt) is included

### Requirements:
- (Minimal profile) Arch Linux
- Internet connection

This should preferably run after a clean arch install

### Quickstart:
```
curl -fsSL https://raw.githubusercontent.com/agustux/dots/main/install.sh | bash -s -- <flags here>
```
Flags:
- `--hypr`      Install Hyprland (default when neither `--gnome` nor `--sway` is given)
- `--sway`      Install Sway; add `--hypr` to also install Hyprland
- `--gnome`     Install GNOME and switch the display manager from ly to GDM; add `--hypr`/`--sway` for a WM

- `--nvidia`    Install NVIDIA drivers/config (auto-detected otherwise)
- `--graphics`  Install Mesa/Vulkan + lib32 graphics stack (included in `--bloat`)
- `--foot`      Install foot instead of Ghostty as the terminal
- `--print`     Install CUPS printing and Avahi/mDNS discovery (not included in `--bloat`)
- `--bloat`     EVERYTHING: `--gnome --sway --hypr --graphics`, NVIDIA, all-vendor GPU/microcode, and extra tools

- `--noswap`    Skip creating the 4GB swapfile, for really storage constrained systems
- `--update`    Only update dotfiles (for existing installs)

The installer may modify your system configuration and will install
packages. Review install.sh before running it if you want to see exactly
what will be changed.

## Hyprland

The default session. Both WMs can be installed side by side (`--hypr --sway`); pick one at the display manager.

- Per-machine overrides (e.g. terminal) go in the untracked `~/.config/hypr/local.lua`, created by the installer.
- Only Hyprland has pseudotiling.

## Sway

Kept at parity with Hyprland where Sway allows it. Both configs are always deployed, even if only one WM is installed.

- Per-machine overrides (e.g. terminal) go in the untracked `~/.config/sway/local.conf`, created by the installer.
- `/usr/local/bin/sway` wraps the stock binary so ly's "Sway" entry gets the same GPU, VA-API, cursor and Qt env as Hyprland. `--update` only refreshes it if `--sway` is passed.
- Sway has no native mirroring, so `sway-outputs.sh` caps the mode like Hyprland and mirrors extra displays with `wl-mirror`.
- Screen capture goes through the wlr portal.
- Reload the config with `Super + Shift + R`.

## Keybinds

`Super` is the main modifier.

### Apps

| Keys | Action |
|---|---|
| `Super + Q` | Terminal (Ghostty, or foot if used `--foot`) |
| `Super + E` | Fil**e** manager (Nautilus) |
| `Super + B` | **B**rowser (**B**rave Origin) |
| `Super + R` | Launche**r** (**r**ofi) |
| `Super + W` | Toggle **W**aybar |
| `Super + Shift + Q` | Lock session |
| `Super + M` | Exit Hyprland |
| `Super + Shift + R` | Reload config (Sway only; Hyprland reloads on save) |

### Screenshots

| Keys | Action |
|---|---|
| `Print` | Region |
| `Alt + Print` | Window |
| `Super + Print` | Primary output |
| `Super + Shift + P` | Region |
| `Super + Alt + P` | Window |
| `Super + Ctrl + P` | Primary output |

### Windows

| Keys | Action |
|---|---|
| `Super + C` | **C**lose |
| `Super + P` | **P**seudotile |
| `Super + T` | **T**oggle split |
| `Super + V` | Toggle floating |
| `Super + F` | Toggle **f**ullscreen |
| `Super + H/J/K/L` | Focus left/down/up/right |
| `Super + Shift + H/J/K/L` | Swap window left/down/up/right |
| `Super + LMB drag` | Move |
| `Super + RMB drag` | Resize |
| `Super + Ctrl + R` | Resize mode: `H`/`L` shrink/grow width, `K`/`J` shrink/grow height, `Esc`/`Enter` exits |

### Workspaces

| Keys | Action |
|---|---|
| `Super + 1–0` | Switch to workspace 1–10 |
| `Super + Shift + 1–0` | Move window to workspace 1–10 |
| `Super + Scroll` | Cycle workspaces |
| 3-finger swipe | Switch workspace |
| `Super + S` | Toggle **s**cratchpad |
| `Super + Shift + S` | Move window to **s**cratchpad |

![Example of my rice](https://github.com/agustux/dots/blob/main/assets/2026-09-11-142304_hyprshot.png)
