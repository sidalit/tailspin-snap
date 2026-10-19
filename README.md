# tailspin snap

[![tailspin](https://snapcraft.io/tailspin/badge.svg)](https://snapcraft.io/tailspin)

Snap packaging for [tailspin](https://github.com/bensadeh/tailspin), a log viewer that highlights timestamps, addresses and other patterns automatically.

Unofficial build, not affiliated with or endorsed by the tailspin project.

## Build

```bash
snapcraft pack
```

## Install and try

<a href="https://snapcraft.io/tailspin"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install tailspin                   # or a local build: ./tailspin_7.0.0_*.snap --dangerous
sudo snap connect tailspin:removable-media   # optional: /media, /mnt
sudo snap connect tailspin:log-observe       # optional: /var/log
tspin ./application.log
journalctl -f | tspin
```

The command is `tspin`, as upstream. Until the Snap Store grants the `tspin` auto-alias, run it as `tailspin.tspin` or create the alias yourself:

```bash
sudo snap alias tailspin.tspin tspin
```

## Known limitations

### System logs in /var/log

Reading files in `/var/log` needs the `log-observe` interface, which is not connected automatically:

```bash
sudo snap connect tailspin:log-observe
tspin /var/log/syslog
```

Normal file permissions still apply: most logs are readable only by root and members of the `adm` group. Without the interface, pipe the log in instead:

```bash
cat /var/log/syslog | tspin
journalctl -f | tspin
```

### Commands run with --exec

`--exec` runs its command inside the snap, so only basic tools from the snap's base are available. Host programs such as `kubectl` or `docker` are not found. Pipe their output instead:

```bash
kubectl logs -f pod_name | tspin
```

The same applies to a custom pager set with `--pager` or `TAILSPIN_PAGER`: the default `less` works, other pagers installed on the host do not.

### Theme file

The snap reads its theme from `~/snap/tailspin/current/.config/tailspin/theme.toml` instead of `~/.config/tailspin/theme.toml`, and it cannot read hidden folders such as `~/.config`. Create the theme in the snap's folder:

```bash
mkdir -p ~/snap/tailspin/current/.config/tailspin
tspin --generate-default-theme > ~/snap/tailspin/current/.config/tailspin/theme.toml
```

Or keep it in a visible folder and pass it explicitly:

```bash
tspin --theme ~/tailspin-theme.toml ./application.log
```

## Update to a new upstream release

Change `source-tag` in `snap/snapcraft.yaml`, then rebuild.

## Automation

Builds, publishing, and dependency updates use [snap-automation](https://github.com/sidalit/snap-automation).

## License

The packaging is MIT-licensed (see `LICENSE`). tailspin is MIT-licensed; its dependencies carry their own licenses.
