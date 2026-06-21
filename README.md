# ansible-i3-gaps

[![CICD](https://github.com/jahrik/ansible-i3-gaps/actions/workflows/cicd.yml/badge.svg)](https://github.com/jahrik/ansible-i3-gaps/actions/workflows/cicd.yml)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-jahrik.i3__gaps-blue?logo=ansible)](https://galaxy.ansible.com/ui/standalone/roles/jahrik/i3_gaps/)

Installs [i3](https://i3wm.org/) — a tiling X11 window manager ([GitHub](https://github.com/i3/i3)) — with a full desktop stack (conky, dunst, feh, dmenu, scrot, xorg tools). Deploys templated config files to `~/.config/i3/`. Note: i3-gaps was merged into mainline i3 at v4.20 (2022); this role now installs mainline i3 on all platforms.

Gaps are enabled by default in the deployed config (`gaps inner 10`, `gaps outer 5`, `smart_gaps on`) with a full keybinding mode for adjusting gaps at runtime (`$mod+Shift+g`).

## OS Support

| Platform | Install method |
|---|---|
| Arch Linux | `pacman` (i3, i3lock, i3status, conky, dmenu, dunst, feh, scrot, xcalib, xorg tools) |
| Debian / Ubuntu | `apt` (i3, i3lock, i3status, conky-all, dmenu, dunst, feh, rxvt-unicode, scrot, fonts-dejavu, udiskie) |

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

## Author Information

jahrik@gmail.com
