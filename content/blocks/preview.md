---
_schema: default
title: Preview
description: >-
  Display live URL previews with switchable device views (desktop, tablet,
  mobile). Shows websites or web applications in an iframe with device-specific
  dimensions and responsive controls.
type: docs
tags: block
modules: ["preview"]
---

## Overview

> [!IMPORTANT]
> Since {{< release version="v2.8.0" short="true" link-type="link" >}}, the
> `preview` block requires the `preview` JS module for device switching and
> auto-scaling. Add `modules: ["preview"]` to the front matter of any page that
> uses this block. Sites that use `preview` on many pages can set
> `integration = "core"` for the preview module in their `params.toml` to load
> it globally instead.

### Basic preview

The `preview` content block renders a live URL preview in an iframe with device switcher controls. By default, it displays in desktop view.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: preview
  heading:
    title: Hugo on Wikipedia
    content: Live preview of the Hugo static site generator Wikipedia page
  url: "https://en.wikipedia.org/wiki/Hugo_(software)"
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Preview with specific device

Set the `device` argument to specify which device view to display by default. Options are `desktop`, `tablet`, or `mobile`.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: preview
  heading:
    title: Tablet Preview
    content: Opens in tablet view (820×1180 logical pixels)
  url: "https://en.wikipedia.org/wiki/Hugo_(software)"
  device: tablet
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Controls below preview

By default the device switcher appears above the preview. Set `controls_placement: bottom` to move it below the preview area instead.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: preview
  heading:
    title: Controls Below
    content: Device switcher placed beneath the preview
  url: "https://en.wikipedia.org/wiki/Hugo_(software)"
  controls_placement: bottom
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Strict aspect ratio

By default the desktop preview fills the full container width and height (responsive mode). Set `desktop_responsive: false` to use a strict 16:10 contain fit instead — the full 1440 × 900px frame is always visible with no clipping, leaving symmetric gaps above and below when the container is wider than it is tall.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: preview
  heading:
    title: Strict Aspect Ratio
    content: Full 1440×900px frame always visible, no clipping
  url: "https://en.wikipedia.org/wiki/Hugo_(software)"
  device: desktop
  desktop_responsive: false
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Full-width preview

Use `cover: true` and `fluid: true` for a full-width preview layout, ideal for showcasing responsive designs.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: preview
  heading:
    title: Full-Width Preview
    content: Responsive design showcase
  background:
    color: body-tertiary
    subtle: true
  width: 12
  cover: true
  fluid: true
  url: "https://en.wikipedia.org/wiki/Hugo_(software)"
  device: desktop
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Embedded map example

The preview component works well with embeddable content like [OpenStreetMap](https://www.openstreetmap.org/). This example demonstrates a full-width preview with custom background styling.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: preview
  heading:
    title: "Embedded Map"
    content: "OpenStreetMap embed URL - specifically designed for iframes"
  background:
    color: body-tertiary
    subtle: true
  width: 12
  cover: true
  fluid: false
  url: "https://www.openstreetmap.org/export/embed.html?bbox=-0.1,51.5,-0.08,51.52"
  device: desktop
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Blocked URL with fallback image

When the target URL sets `X-Frame-Options` or `Content-Security-Policy: frame-ancestors 'none'`, Hugo detects this at build time via a HEAD request and renders the error overlay server-side. Provide an `image` argument to display a representative screenshot in place of the blocked iframe. The warning alert with a direct link is still shown below the image.

Set `show-fallback: true` to force the error overlay explicitly — useful when the HEAD request cannot reach the target URL (offline or CI environments), or when the URL blocks embedding for your specific domain without using the headers detected above.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: preview
  heading:
    title: Preview unavailable
    content: This URL blocks iframe embedding — a fallback image is shown instead
  url: "https://google.com"
  image: /img/placeholder.png
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Blocked URL without fallback image

Without an `image` argument the component shows only the warning alert when the iframe fails to load, with a link to open the URL directly in a new tab.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: preview
  heading:
    title: Preview unavailable (alert only)
    content: No fallback image — only the warning alert is displayed
  url: "https://google.com"
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

## CSP Configuration

The preview component embeds external URLs in iframes, which requires appropriate Content Security Policy (CSP) configuration.

### Production configuration

For production environments, explicitly allow the domains you want to embed in your `config/production/params.toml`:

```toml
[modules.hinode.csp]
    frame-src = [
        "https:",                        # Allow all HTTPS sources
        "example.com",                   # Specific domain
        "*.yourdomain.com",              # Wildcard subdomain
        "*.googletagmanager.com",
        "player.cloudinary.com",
        "www.youtube-nocookie.com",
        "www.youtube.com",
        "player.vimeo.com"
    ]
```

### Development configuration

For local development, allow HTTP sources in your `config/development/params.toml`:

```toml
[modules.hinode.csp]
    frame-src = [
        "http:",                         # Allow all HTTP for localhost
        "https:",
        "*.googletagmanager.com",
        "player.cloudinary.com",
        "www.youtube-nocookie.com",
        "www.youtube.com",
        "player.vimeo.com"
    ]
```

This allows embedding localhost sites during development while maintaining security in production.

### Hugo security configuration

Build-time embedding detection issues a HEAD request to each preview URL during the build. Hugo's default security policy only allows `GET` and `POST` methods. Add the following to your site's `config/_default/hugo.toml` to enable HEAD requests:

```toml
[security]
  [security.http]
    methods = ['(?i)GET|POST|HEAD']
    urls = ['.*']
```

Without this setting, the HEAD requests are silently blocked and embedding restrictions are not detected. Use `show-fallback: true` to force the fallback explicitly — it is not affected by this setting.

### Embedding restrictions

Many websites prevent iframe embedding using `X-Frame-Options` or `Content-Security-Policy` response headers. Hugo issues a HEAD request to each preview URL at build time and inspects the response headers. Detection coverage:

| Response header | Build-time action |
|---|---|
| `X-Frame-Options` (any value) | Fallback rendered — blocks all cross-origin embedding |
| `Content-Security-Policy: frame-ancestors 'none'` | Fallback rendered — blocks all embedding |
| `Content-Security-Policy: frame-ancestors` with specific domains | No action — domain-specific; whether the iframe loads depends on the deployment domain |
| No relevant headers | No action — embedding allowed by default |

For `frame-ancestors` with specific domains (e.g. `'self' example.com *.example.com`), Hugo cannot determine at build time whether the iframe will load on your site, since the allowed origins depend on the deployment domain. If you know a URL will not embed on your site, use `show-fallback: true` to render the fallback explicitly.

**Best practices:**

- Use the preview component for sites you control or that explicitly allow embedding
- Test URLs in development before deploying
- Set `image` to a representative screenshot so users see meaningful content when embedding is blocked
- Use `show-fallback: true` in offline or CI environments where the HEAD request cannot reach the target URL, or when a URL restricts embedding via domain-specific `frame-ancestors` headers
- Use embeddable alternatives (e.g., youtube-nocookie.com instead of youtube.com)

## Device dimensions

Device dimensions use **logical pixels** (CSS pixels), which is what browsers and responsive design tools use for layout. Physical pixels depend on the device pixel ratio (DPR) of the hardware display.

| Device | Logical resolution | Aspect ratio | DPR reference |
|--------|-------------------|--------------|---------------|
| Desktop | 1440 × 900px | 16:10 | @1× (MacBook / laptop) |
| Tablet | 820 × 1180px | ~9:13 | @2× (iPad 10th gen / iPad Air M2) |
| Mobile | 402 × 874px | 9:19.5 | @3× (iPhone 17 Pro, 460 ppi) |

A website loaded inside the iframe sees a viewport matching these logical pixel dimensions, so breakpoints and responsive layouts behave exactly as they would on the real device.

### Auto-scaling

JavaScript scales each device on page load and on every browser resize. Tablet and mobile always use a **contain fit** — the largest scale where neither dimension is clipped:

```
scale = min(containerWidth / deviceWidth, containerHeight / deviceHeight, 1)
```

Desktop scaling depends on the `desktop_responsive` argument:

| Mode | `desktop_responsive` | Behaviour |
|------|----------------------|-----------|
| Responsive (default) | `true` | Scales to fill the full container width; iframe height is adjusted dynamically so the container height is also filled. The site inside sees a 1440px-wide viewport. |
| Strict aspect ratio | `false` | Contain fit — the full 1440 × 900px frame is always visible; symmetric gaps may appear above and below on wide containers. |

The zoom recalculates on page load and whenever the browser window is resized.

**Container height** adapts to available viewport space and is capped so tall devices
(tablet: 1180px logical) are never rendered beyond the available screen area:

```scss
height: min(calc(100vh - controls - navbar - 4rem),
            calc(var(--max-section-height, 1024px) - controls));
min-height: 400px;
```

### Responsive visibility

The component automatically shows or hides device previews **based on viewport width only**:

- **Small screens (< 640px)**: Mobile preview only
- **Medium screens (640px–1023px)**: Tablet and mobile previews
- **Large screens (≥ 1024px)**: All three previews

Buttons for hidden device views are automatically hidden from the control bar, and the active view automatically switches when a panel becomes unavailable.

### Container constraints

In responsive mode (default), the desktop preview fills whatever container it is placed in. For best results with `desktop_responsive: false` or when using `cover: true`:

- Use `fluid: true` or `width: 12` for full-width layouts
- Use a container at least as wide as the desired desktop zoom level

## Security

The preview component includes iframe sandboxing for security:

```html
sandbox="allow-scripts allow-same-origin allow-forms allow-popups"
```

This restricts iframe capabilities while allowing:

- JavaScript execution (`allow-scripts`)
- Access to same-origin resources (`allow-same-origin`)
- Form submissions (`allow-forms`)
- Opening popups/new windows (`allow-popups`)

## Arguments

The content block supports the following arguments:

{{< args bookshop-preview >}}
