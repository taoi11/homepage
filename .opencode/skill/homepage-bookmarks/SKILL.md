---
name: homepage-bookmarks
description: Configure bookmarks.yaml for Homepage dashboard - quick-access links with icons and categories
license: MIT
compatibility: opencode
metadata:
  project: homepage
  type: yaml-config
---

# Homepage bookmarks.yaml Configuration

Reference for quick-access bookmarks.

## Structure

```yaml
---
- CategoryName:
    - ServiceName:
        - abbr: AB
          href: https://url.com
```

## Properties

| Property      | Type   | Required | Description           |
| ------------- | ------ | -------- | --------------------- |
| `abbr`        | string | No       | 2-letter abbreviation |
| `href`        | string | **Yes**  | Link URL              |
| `icon`        | string | No       | Icon (overrides abbr) |
| `description` | string | No       | Custom description    |

## Basic Example

```yaml
---
- Developer:
    - Github:
        - abbr: GH
          href: https://github.com/

- Social:
    - Reddit:
        - abbr: RD
          href: https://reddit.com/
```

## With Icons

```yaml
---
- Developer:
    - Github:
        - icon: si-github
          href: https://github.com/
    - GitLab:
        - icon: si-gitlab
          href: https://gitlab.com/

- Social:
    - YouTube:
        - icon: si-youtube
          href: https://youtube.com/
    - Reddit:
        - icon: si-reddit
          href: https://reddit.com/
```

## With Descriptions

```yaml
---
- Infrastructure:
    - Tailscale:
        - abbr: TS
          href: https://login.tailscale.com/admin/machines
          description: VPN Management

    - Cloudflare:
        - icon: si-cloudflare
          href: https://dash.cloudflare.com/
          description: DNS and CDN
```

## Icon Sources

Same as services:

```yaml
icon: github.png           # Dashboard Icons
icon: si-github            # Simple Icons
icon: mdi-github           # Material Design Icons
icon: sh-github            # selfh.st icons
icon: https://example.com/icon.png  # Remote URL
```

## Layout Options

In settings.yaml, control bookmark appearance:

```yaml
layout:
  Developer:
    style: row
    columns: 4
    iconsOnly: true # Show only icons
```

## Complete Example

```yaml
---
- Infrastructure:
    - Tailscale:
        - abbr: TS
          href: https://login.tailscale.com/admin/machines
    - Unraid:
        - abbr: UNR
          href: http://unraid.local
    - iLO:
        - abbr: iLO
          href: https://10.1.11.11/

- Developer:
    - GitHub:
        - icon: si-github
          href: https://github.com/
    - GitLab:
        - icon: si-gitlab
          href: https://gitlab.com/
    - Stack Overflow:
        - icon: si-stackoverflow
          href: https://stackoverflow.com/

- Entertainment:
    - YouTube:
        - icon: si-youtube
          href: https://youtube.com/
    - Netflix:
        - icon: si-netflix
          href: https://netflix.com/
    - Spotify:
        - icon: si-spotify
          href: https://open.spotify.com/
```
