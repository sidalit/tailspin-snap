<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="snap/gui/tailspin-dark.png" />
  <img src="snap/gui/tailspin.png" alt="tailspin logo" width="128" />
</picture>

# tailspin

**Read logs with automatic highlighting.**

[![tailspin](https://snapcraft.io/tailspin/badge.svg)](https://snapcraft.io/tailspin)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [tailspin](https://github.com/bensadeh/tailspin), a log viewer that highlights timestamps, addresses and other patterns automatically.

</div>

---

## Getting Started

<a href="https://snapcraft.io/tailspin"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install tailspin
tspin ./application.log
```

## Configure

There are no `snap set` options.

| Setting | Value / default |
|---|---|
| Theme file | `~/snap/tailspin/current/.config/tailspin/theme.toml` |
| Alternative theme | `--theme <path>` to a readable TOML file |
| Pager | `--pager` or `TAILSPIN_PAGER`; defaults to `less` |

Generate a starting theme in a visible home folder with `tspin --generate-default-theme > ~/tailspin-theme.toml`, then select it with `--theme ~/tailspin-theme.toml`.

Optional file access:

```bash
sudo snap connect tailspin:removable-media  # /media and /mnt
sudo snap connect tailspin:log-observe      # /var/log
```

## Limitations

- Reading `/var/log` also requires normal file permissions, commonly root or membership in `adm`. Alternatively, pipe logs from the host: `journalctl -f | tspin`.
- `--exec` and custom pagers run inside the snap. Host-only commands such as `kubectl` or `docker` are unavailable; pipe their output instead. The default `less` works.
- Hidden host configuration directories such as `~/.config` are inaccessible. Use the snap's theme path or a visible file in your home folder.

## Build

```bash
git clone https://github.com/sidalit/tailspin-snap.git
cd tailspin-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/tailspin-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/bensadeh/tailspin/issues).

## License

Snap packaging: [MIT](https://github.com/sidalit/tailspin-snap/blob/main/LICENSE).
