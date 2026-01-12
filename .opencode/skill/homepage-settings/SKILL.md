---
name: homepage-settings
description: Configure settings.yaml for Homepage dashboard - theme, layout, providers, quick launch, and global options
license: MIT
compatibility: opencode
metadata:
  project: homepage
  type: yaml-config
---

# Homepage settings.yaml Configuration

Reference for application-level settings.

## Structure

```yaml
---
title: My Homepage
theme: dark
layout:
  GroupName:
    style: row
    columns: 4
```

## Title & Branding

| Property      | Type   | Description            |
| ------------- | ------ | ---------------------- |
| `title`       | string | Page title             |
| `description` | string | Meta description       |
| `favicon`     | string | URL or path to favicon |
| `startUrl`    | string | PWA URL (default "/")  |

## Theme & Appearance

| Property      | Values                                                                                                                                                                                             |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `theme`       | `dark`, `light`                                                                                                                                                                                    |
| `color`       | `slate`, `gray`, `zinc`, `neutral`, `stone`, `amber`, `yellow`, `lime`, `green`, `emerald`, `teal`, `cyan`, `sky`, `blue`, `indigo`, `violet`, `purple`, `fuchsia`, `pink`, `rose`, `red`, `white` |
| `cardBlur`    | `xs`, `sm`, `md`, `xl`                                                                                                                                                                             |
| `headerStyle` | `underlined`, `boxed`, `clean`, `boxedWidgets`                                                                                                                                                     |
| `iconStyle`   | `gradient`, `theme`                                                                                                                                                                                |

## Background

```yaml
background:
  image: /images/background.png
  blur: sm
  saturate: 50
  brightness: 50
  opacity: 50
```

Note: Restart container when adding new images.

## Layout

```yaml
layout:
  Media:
    style: row
    columns: 4
    header: false
    initiallyCollapsed: true
    useEqualHeights: true
    icon: jellyfin.png
```

| Property             | Type    | Description         |
| -------------------- | ------- | ------------------- |
| `style`              | string  | `row` or `column`   |
| `columns`            | number  | 1-8                 |
| `header`             | boolean | Show section header |
| `initiallyCollapsed` | boolean | Start collapsed     |
| `useEqualHeights`    | boolean | Equal height cards  |
| `icon`               | string  | Section icon        |

## Tabs

```yaml
layout:
  Media:
    tab: First
    style: row
    columns: 4
  Downloads:
    tab: First
  Monitoring:
    tab: Second
  Always Visible:
    style: row # No tab = all tabs
```

## Layout Behavior

| Property                   | Type    | Description                   |
| -------------------------- | ------- | ----------------------------- |
| `fullWidth`                | boolean | Use full window width         |
| `maxGroupColumns`          | number  | Max group columns (default 4) |
| `disableCollapse`          | boolean | Disable collapsing            |
| `groupsInitiallyCollapsed` | boolean | Collapse all                  |

## Providers

Define shared API credentials:

```yaml
providers:
  openweathermap: your-api-key
  longhorn:
    url: https://longhorn.example.com
    username: admin
    password: LonghornPassword
```

Use in widgets:

```yaml
- openweathermap:
    provider: openweathermap # Instead of apiKey
    latitude: 50.449684
    longitude: 30.525026
```

## Quick Launch

```yaml
quicklaunch:
  searchDescriptions: true
  hideInternetSearch: false
  showSearchSuggestions: true
  provider: google # duckduckgo, bing, baidu, brave, custom
```

Custom provider:

```yaml
quicklaunch:
  provider: custom
  url: https://www.ecosia.org/search?q=
  suggestionUrl: https://ac.ecosia.org/autocomplete?type=list&q=
```

## Global Options

| Property          | Type    | Description                            |
| ----------------- | ------- | -------------------------------------- |
| `target`          | string  | Default link target: `_blank`, `_self` |
| `language`        | string  | Locale: `en`, `fr`, `de`, etc.         |
| `hideVersion`     | boolean | Hide version number                    |
| `showStats`       | boolean | Show all Docker stats                  |
| `statusStyle`     | string  | Global: `dot`, `basic`                 |
| `hideErrors`      | boolean | Hide widget errors                     |
| `disableIndexing` | boolean | Block search engines                   |

## Complete Example

```yaml
---
title: My Dashboard
theme: dark
color: slate
headerStyle: boxed
useEqualHeights: true

layout:
  Media:
    style: row
    columns: 4
    icon: jellyfin.png
  Monitoring:
    style: row
    columns: 3
    initiallyCollapsed: true

providers:
  openweathermap: { { HOMEPAGE_VAR_WEATHER_KEY } }

quicklaunch:
  searchDescriptions: true
  provider: duckduckgo

target: _blank
showStats: true
statusStyle: dot
```
