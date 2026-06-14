# ansible-i3-gaps

[![CICD](https://github.com/jahrik/ansible-i3-gaps/actions/workflows/cicd.yml/badge.svg)](https://github.com/jahrik/ansible-i3-gaps/actions/workflows/cicd.yml)

Install and configure i3 with gaps support, along with a full desktop stack (conky, dunst, feh, dmenu, scrot, xorg tools). Deploys templated config files to `~/.config/i3/`. Supports Arch Linux and Debian/Ubuntu.

Gaps are enabled by default in the deployed config (`gaps inner 10`, `gaps outer 5`, `smart_gaps on`) with a full keybinding mode for adjusting gaps at runtime (`$mod+Shift+g`).

**Platform notes:**
- **Arch**: installs `i3-gaps` from the AUR via pacman (the gaps fork).
- **Ubuntu 24.04+**: gaps support was merged into mainline i3 at v4.20, so this role installs the standard `i3` package — which includes full gaps functionality. The separate `i3-gaps` package no longer exists on Ubuntu 24.04.

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `install` | `true` | Set to `false` to uninstall i3 and remove config files |
| `i3.lock` | `true` | Enable i3lock |
| `i3.bar` | `false` | Use i3bar (false = use polybar) |
| `i3.polybar` | `true` | Enable polybar |
| `i3.terminal` | `alacritty` | Default terminal emulator |
| `conky.update_int` | `2` | Conky update interval (seconds) |
| `conky.interface` | `ansible_default_ipv4.interface` | Network interface for conky |

## Example Playbook

```yaml
- hosts: workstations
  roles:
    - role: jahrik.i3_gaps
```

To uninstall:

```yaml
- hosts: workstations
  roles:
    - role: jahrik.i3_gaps
      vars:
        install: false
```

## Testing

```bash
yamllint .
ansible-lint
molecule test
molecule converge
molecule destroy
```

## License

GPLv2
