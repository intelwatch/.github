# Security Policy

## Reporting a Vulnerability

Email **intelwatch@badopsec.lol** with:
- Description and impact
- Steps to reproduce
- Affected version / commit
- Any suggested fix

You'll get a response within 72 hours. We'll coordinate disclosure.

## Scope

In scope: the bot process, its state files, and the Discord command surface.
Out of scope: third-party APIs the bot queries, the Python tools it invokes.

## Hardening

- Never commit `.env` — it's gitignored.
- Rotate `DISCORD_TOKEN` and `OPENROUTER_API_KEY` immediately if leaked.
- Run the bot as an unprivileged user (`intelwatch`), not root.
- Use the provided systemd unit, which enables `NoNewPrivileges`, `PrivateTmp`, and `ProtectSystem`.