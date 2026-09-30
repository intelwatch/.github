# Changelog

All notable changes to IntelWatch are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.1.0] — 2026-09-30

### Added
- AI layer: `/ai ask [prompt]` with OpenRouter tool-calling, 25 LLM-callable tools, 6-step tool loops, live progress.
- Monitoring: `/monitor add|list|remove|run` with 60s scheduler, hash-diff detection, change-only alerts.
- Threat intel (keyless): InternetDB, GreyNoise Community, Hudson Rock Cavalier, XposedOrNot, EmailRep, ThreatFox, URLhaus, OSV.
- Output: `/graph [id]` (PNG/SVG), `/report [id]` (Markdown), `/changelog`.
- Ping flow: mention the bot to start a guided request wizard with multi-select and modal.
- Entity extraction: auto-pull IPs, emails, hashes, URLs, BTC/ETH wallets from every scan.
- Backups: daily rotation, last 30 kept, `/backup` to force.
- Proxy pool: health-tracked, opt-in via `PROXY_POOL`.
- Per-guild isolation for requests and monitors.

### Changed
- `/scan` now parallel + target-classified and covers more sources.
- 30-minute response cache.
- Per-user cooldowns (8s scan, 15s AI).
- Global scan semaphore (max 3 concurrent).
- `/pull` now paginated.

### Fixed
- `/osintsearch` no longer crashes on non-string result values.
- Error handler now correctly handles deferred interactions.
- Graph rendering works with any `@viz-js/viz` version and falls back to SVG if `sharp` is unavailable.

### Internal
- Migrated to `MessageFlags.Ephemeral` (discord.js v14).
- Enabled Message Content Intent.
- Added production scaffolding (Docker, systemd, CI).

## [2.0.0] — 2026-09-29

### Added
- Initial IntelWatch release: `/scan`, `/osint`, `/breach`, `/whois`, `/crypto`, `/username`, `/github`, `/reddit`, `/gravatar`, `/discord`, `/ghunt`, `/dnstwist`, `/subdomains`, `/crt`, `/ssl`, `/headers`, `/dns`, `/ip`, `/wayback`, `/urlscan`, `/phone`.

[2.1.0]: https://github.com/your-org/intelwatch/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/your-org/intelwatch/releases/tag/v2.0.0