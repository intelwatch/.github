# IntelWatch

Autonomous OSINT platform for Discord. 55+ keyless data sources, LLM tool-calling, continuous monitoring, and graph/report generation — in one bot.

```
55+ commands   ·   55+ data sources   ·   30+ platforms enumerated   ·   0 API keys required
```

## Features

- **AI copilot** — `/ai ask "search test user up"` runs real OSINT tools via OpenRouter tool-calling and summarizes the results.
- **Parallel scan** — `/scan [target]` classifies the input and fans out to every relevant source at once.
- **Continuous monitoring** — `/monitor add target 24h` re-scans on schedule and only pings you when something changes.
- **Daily briefings** — automatically at `BRIEFING_HOUR` local time.
- **Guided ping flow** — mention the bot → pick data types → fill a modal → request submitted.
- **Graph & report output** — `/graph #id` renders an entity relationship PNG; `/report #id` produces a Markdown briefing.
- **No API keys needed** — every data source is either fully public or has a generous free tier.

## Data Sources

**Network** · RDAP, dns.google, crt.sh, ip-api, internetdb.shodan.io, greynoise.io
**Threat Intel** · threatfox.abuse.ch, urlhaus.abuse.ch, osv.dev, hudsonrock.com
**Identity** · github.com, reddit.com, gravatar.com, discord.com, GHunt, numlookupapi
**Breach** · haveibeenpwned (best-effort), xposedornot.com, emailrep.io
**Local** · sherlock, holehe, dnstwist, sublist3r, nexfil (Python via venv)
**Certificates** · TLS handshake, Certificate Transparency

## Quick Start

```bash
git clone https://github.com/your-org/intelwatch.git
cd intelwatch
cp .env.example .env
# edit .env — set DISCORD_TOKEN, CLIENT_ID, OPENROUTER_API_KEY
npm install
node src/index.js
```

### Docker

```bash
docker compose up -d --build
docker compose logs -f
```

## Environment

| Variable | Required | Description |
| --- | --- | --- |
| `DISCORD_TOKEN` | yes | Bot token from the Discord Developer Portal |
| `CLIENT_ID` | yes | Application ID |
| `GUILD_ID` | no | Test server ID for instant command sync |
| `OPENROUTER_API_KEY` | yes (for `/ai`) | https://openrouter.ai/keys |
| `OPENROUTER_MODEL` | no | Defaults to `openai/gpt-4o-mini` |
| `VENV` | no | Python venv bin dir. Defaults to `/opt/osint-venv/bin` |
| `BRIEFING_HOUR` | no | Hour (0–23) to post the daily briefing. Default 9 |
| `PROXY_POOL` | no | Comma-separated HTTP proxies for scraping modules |

## Bot Setup

1. Create an application at https://discord.com/developers/applications
2. Bot → Reset Token → copy to `DISCORD_TOKEN`
3. Bot → enable **Message Content Intent** (required for the ping flow)
4. OAuth2 → URL Generator → scopes `bot applications.commands` → permissions: Send Messages, Embed Links, Attach Files, Use Slash Commands, Read Message History
5. Paste the URL and invite the bot

## Python Tools (optional)

```bash
python3 -m venv /opt/osint-venv
/opt/osint-venv/bin/pip install sherlock-project holehe dnstwist
# GHunt (needs a browser cookie): https://github.com/mxrch/GHunt
```

If Python tools aren't installed, the corresponding jobs just return `null` and are skipped — everything else keeps working.

## Commands

Run `/help` in Discord. Categories: AI · Threat Intel · Network · Identity · Crypto · Monitoring · Output · Requests · Owner.

## Production

- **State files** live in `data/` — mounted volume in Docker.
- **Backups** rotate daily, keeping the last 30 in `backups/`.
- **Audit log** at `logs/osint-audit.log`.
- **Graceful shutdown** flushes all state on SIGINT / SIGTERM.
- **Per-guild isolation** — users only see their own server's requests unless they're the owner.

## Security

See [SECURITY.md](SECURITY.md). Report vulnerabilities privately.

## License

MIT — see [LICENSE](LICENSE).