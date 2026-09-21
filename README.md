# Audiobookshelf

> TOS 7 application package for **Audiobookshelf** — platform integration only.
> The application itself is provided by the upstream project, unmodified.

## Overview

Self-hosted audiobook and podcast server with metadata scraping and mobile apps.

上游项目 / Upstream: <https://github.com/advplyr/audiobookshelf>
上游许可证 / License: **GPL-3.0**

## Features

- Audiobook library with automatic metadata lookup
- Podcast subscription and download
- Per-user playback progress sync
- Official iOS and Android apps

## Installation

1. Requirements: TOS 7.0+ and Docker Engine (install from the TOS App Center)
2. Install from the TOS App Center
3. Open the app and complete initial configuration

## Usage

1. Access URL: `http://${ip}:18805`
2. Default credentials: see upstream documentation
3. Key settings: see upstream documentation

## Permissions

| Permission | Rationale |
|---|---|
| Network: port 18805 | Web UI access |
| File system: `/Volume*/DockerAppData/shh5-audiobookshelf/` | Application data persistence |
| User: shh5audiobookshelf | Isolated non-root service execution |

## Configuration

See `config.ini` for platform metadata; see `docker-compose.yml` for runtime configuration.

## Ports

| Port | Protocol | Purpose |
|---|---|---|
| 18805 | TCP | Web UI (Audiobookshelf) |

## Support

- Documentation: https://github.com/advplyr/audiobookshelf
- Issue tracker: https://github.com/advplyr/audiobookshelf/issues
- Community: https://github.com/advplyr/audiobookshelf

## Security & Compliance

- **License**: GPL-3.0 — full text in [`LICENSE`](./LICENSE)
- **Attribution**: see [`NOTICE`](./NOTICE)
- **Privacy Policy**: see [`PRIVACY.md`](./PRIVACY.md)
- **Vulnerability scan**: `trivy-report.txt` attached to each Release (HIGH/CRITICAL must be 0)
- Runs as a non-root dedicated user; no privileged mode, no host network

## Changelog

### v1.0.1 (2026-09-20)
- Compliance update: added LICENSE / NOTICE / PRIVACY materials,
  declared upstream license inside the package, added container healthcheck

### v1.0.0
- Initial release

## License

**GPL-3.0** — this packaging repository is distributed under the same license as the
upstream project. Full text: [`LICENSE`](./LICENSE).
