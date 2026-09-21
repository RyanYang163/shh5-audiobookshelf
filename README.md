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
| User: non-root `1000:1000` | Isolated non-root container execution |

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
- Runs as a non-root user (`user: "1000:1000"`); no privileged mode, no host network
- **Vulnerability scan**: `trivy-report.txt` and `trivy-summary.txt` are attached to every Release

### About the container image vulnerabilities (review item T1 / S10)

The upstream image `advplyr/audiobookshelf:2.36.1` bundles third-party npm dependencies
that carry known HIGH/CRITICAL advisories (`axios`, `tar`, `nodemailer`, `path-to-regexp`,
`socket.io`, `ws`, `form-data`, `sequelize`, …). **Essentially all findings live inside the
upstream-published image**, not in this packaging repository: this repo ships no image
layers, only `config.ini` / `.lang` / `.svg` / `docker-compose.yml`, so no change here can
remove them. Only a handful originate from the Alpine base layer.

Measured with `trivy 0.74.0` (DB 2026-09-21): **72 HIGH/CRITICAL total, 71 with an upstream
fix available**. The release workflow therefore enforces a *regression* gate (the count may
not exceed the declared baseline) instead of a zero-tolerance gate, and publishes the full
report with every Release.

This finding is declared to the platform for the **T1 exemption channel**. Under the
developer review specification V2.3, T1 (“no known high-severity CVEs”) is a *hold +
exemption* item, not a rejection item — rejection is reserved for V4 (malicious code) and
V12 (illegal content).

Upstream tracking: <https://github.com/advplyr/audiobookshelf>

## Changelog

### v1.0.3 (2026-09-21)
- Bumped upstream image `2.33.0` → `2.36.1`
- Fixed the container healthcheck: it previously invoked `curl`, which is not installed in
  this `node:24-alpine` based image; now uses the busybox `wget` present in the image
- Restored the in-package licence declaration header in `docker-compose.yml`
- Rewrote `PRIVACY.md` to describe the actual container-based security measures
  (the previous text described systemd hardening that does not apply to a Docker app)
- Release workflow: trivy gate changed from zero-tolerance to a declared-baseline
  regression gate, with the full report published alongside each Release

### v1.0.2 (2026-09-20)
- Bumped version after the previous submission was held

### v1.0.1 (2026-09-20)
- Compliance update: added LICENSE / NOTICE / PRIVACY materials,
  declared upstream license inside the package, added container healthcheck

### v1.0.0
- Initial release

## License

**GPL-3.0** — this packaging repository is distributed under the same license as the
upstream project. Full text: [`LICENSE`](./LICENSE).
