---
name: homepage-widgets
description: Configure widgets.yaml for Homepage dashboard - information widgets (resources, search, datetime, weather) and service widget types
license: MIT
compatibility: opencode
metadata:
  project: homepage
  type: yaml-config
---

# Homepage widgets.yaml Configuration

Reference for information widgets and service widget types.

## Structure

widgets.yaml displays information widgets at page top:

```yaml
---
- resources:
    cpu: true
    memory: true

- search:
    provider: google
```

## Resources Widget

```yaml
- resources:
    label: System
    cpu: true
    memory: true
    disk: /
    cputemp: true
    tempmin: 0
    tempmax: 100
    uptime: true
    network: true
    refresh: 3000
    expanded: true
    units: metric # or imperial
    diskUnits: bytes # or bbytes
```

### Multiple Disks

```yaml
- resources:
    label: Storage
    disk:
      - /mnt/storage
      - /mnt/backup
      - /mnt/media
```

### Resource Groups

```yaml
- resources:
    label: System
    cpu: true
    memory: true

- resources:
    label: Storage
    disk: /mnt/data
```

## Search Widget

```yaml
- search:
    provider: google # duckduckgo, bing, baidu, brave, custom
    focus: true
    showSearchSuggestions: true
    target: _blank
```

### Custom Provider

```yaml
- search:
    provider: custom
    url: https://www.ecosia.org/search?q=
    suggestionUrl: https://ac.ecosia.org/autocomplete?type=list&q=
    showSearchSuggestions: true
```

### Multiple Providers

```yaml
- search:
    provider: [brave, google, duckduckgo]
```

## DateTime Widget

```yaml
- datetime:
    text_size: xl # 4xl, 3xl, 2xl, xl, md, sm, xs
    locale: en
    format:
      timeStyle: short
      dateStyle: short
      hour12: true
```

### Format Examples

```yaml
# 13:37
format:
    timeStyle: short
    hourCycle: h23

# 1:37 PM
format:
    timeStyle: short
    hour12: true

# 1/23/22, 1:37 PM
format:
    dateStyle: short
    timeStyle: short
    hour12: true
```

## Weather Widgets

### OpenWeatherMap

```yaml
- openweathermap:
    provider: openweathermap # or apiKey directly
    latitude: 36.66
    longitude: -117.51
    cache: 5
```

### Open-Meteo (No API key)

```yaml
- openmeteo:
    label: Weather
    latitude: 36.66
    longitude: -117.51
    cache: 5
```

## Service Widget Types

Common widgets for services.yaml:

### Media

| Type       | Description     | Common Fields           |
| ---------- | --------------- | ----------------------- |
| `plex`     | Plex server     | streams, libraries      |
| `jellyfin` | Jellyfin server | streams, movies, series |
| `emby`     | Emby server     | streams, movies         |
| `tautulli` | Plex stats      | active, bandwidth       |

### Automation

| Type       | Description     | Common Fields          |
| ---------- | --------------- | ---------------------- |
| `sonarr`   | Series manager  | wanted, queued, series |
| `radarr`   | Movie manager   | wanted, queued, movies |
| `lidarr`   | Music manager   | wanted, queued, albums |
| `readarr`  | Book manager    | wanted, queued, books  |
| `prowlarr` | Indexer manager | grabs, queries         |
| `bazarr`   | Subtitles       | wanted, queued         |

### Downloads

| Type           | Description    | Common Fields                 |
| -------------- | -------------- | ----------------------------- |
| `transmission` | Torrent client | leech, seed, download, upload |
| `qbittorrent`  | Torrent client | download, upload, seeds       |
| `deluge`       | Torrent client | download, upload              |
| `sabnzbd`      | Usenet client  | queue, speed                  |

### Requests

| Type         | Description     | Common Fields                |
| ------------ | --------------- | ---------------------------- |
| `jellyseerr` | Request manager | pending, approved, available |
| `overseerr`  | Request manager | pending, approved            |
| `ombi`       | Request manager | pending, approved            |

### Infrastructure

| Type            | Description       | Common Fields      |
| --------------- | ----------------- | ------------------ |
| `portainer`     | Container manager | containers, stacks |
| `proxmox`       | Virtualization    | vms, containers    |
| `pihole`        | DNS blocker       | queries, blocked   |
| `nextdns`       | DNS stats         | queries, blocked   |
| `uptimekuma`    | Uptime monitor    | up, down, pending  |
| `homeassistant` | Home automation   | entities           |

### Monitoring

| Type         | Description       | Common Fields |
| ------------ | ----------------- | ------------- |
| `grafana`    | Metrics dashboard | alerts        |
| `prometheus` | Metrics           | up, alerts    |
| `glances`    | System stats      | cpu, memory   |

### Finance

| Type     | Description   | Common Fields  |
| -------- | ------------- | -------------- |
| `wallos` | Subscriptions | total, monthly |

### Custom

| Type        | Description                                |
| ----------- | ------------------------------------------ |
| `customapi` | Custom API integration with field mappings |

## CustomAPI Widget

```yaml
- MyService:
    widget:
      type: customapi
      url: http://api.service/stats
      headers:
        Authorization: Bearer {{HOMEPAGE_VAR_TOKEN}}
      mappings:
        - field: data.users
          label: Users
          format: number
        - field: data.status
          label: Status
```

## Widget with Fields

Limit displayed fields:

```yaml
- Sonarr:
    widget:
      type: sonarr
      url: http://sonarr.host
      key: { { HOMEPAGE_VAR_SONARR_API_KEY } }
      fields: ["wanted", "queued"]
      enableQueue: true
```

## Complete widgets.yaml Example

```yaml
---
- resources:
    label: System
    cpu: true
    memory: true
    cputemp: true
    uptime: true

- resources:
    label: Storage
    expanded: true
    disk:
      - /
      - /mnt/data

- search:
    provider: duckduckgo
    focus: true

- datetime:
    text_size: xl
    format:
      timeStyle: short
      dateStyle: short

- openmeteo:
    label: Weather
    latitude: 53.5461
    longitude: -113.4938
```
