# AGENTS.md - Homepage Dashboard Configuration

## Project Overview

This repository contains YAML configuration files for a [Homepage](https://github.com/gethomepage/homepage) dashboard instance. Homepage is a modern, self-hosted application dashboard.

**This is NOT a code project** - purely configuration files. No build, test, or lint commands exist.

**For YAML syntax reference**: Use skills `homepage-services`, `homepage-settings`, `homepage-docker`, `homepage-widgets`, `homepage-bookmarks`

---

## Repository Structure

```plaintext
homepage/
├── config/
│   ├── services.yaml    # Service definitions with widgets
│   ├── settings.yaml    # UI/layout configuration
│   ├── docker.yaml      # Docker socket connections
│   └── bookmarks.yaml   # Quick-access bookmarks
├── docker-compose.yml   # Container orchestration
├── .env.example         # Environment variable template
└── .env                 # Secrets (gitignored)
```

---

## Deployment

Dashboard is deployed on remote host via Tailscale VPN:

```bash
ssh luffy@ionos-1.bun-delta.ts.net "cd /home/luffy/docker/homepage && git pull"
```

- Do not open a persistent shell session.
- The container will auto update to the new configuration.

**Web Access**: `http://ionos-1.bun-delta.ts.net:3000`

---

## Code Style

### Environment Variables

Secrets use `{{HOMEPAGE_VAR_*}}` syntax:

```yaml
key: {{HOMEPAGE_VAR_JELLYFIN_API_KEY}}
```

**Never hardcode secrets in YAML files.**

---

## Anti-Patterns

| Avoid                       | Do Instead                |
| --------------------------- | ------------------------- |
| Hardcoding API keys         | Use `{{HOMEPAGE_VAR_*}}`  |
| Inconsistent indentation    | Always 4 spaces           |
| Missing `server:` for stats | Match docker.yaml entry   |
| Committing .env             | Use .env.example template |

---

## Git Workflow

```bash
# Commit message format
OpenCode: ...

# Examples
OpenCode: Added Service: Jellyfin service to Media stack
OpenCode: Updated Service: Grafana URL to new host
```

---

## Resources

- [Homepage Docs](https://gethomepage.dev/)
- [Widget Reference](https://gethomepage.dev/widgets/)
- [Service Config](https://gethomepage.dev/configs/services/)
- **Skills**: `homepage-services`, `homepage-settings`, `homepage-docker`, `homepage-widgets`, `homepage-bookmarks`
