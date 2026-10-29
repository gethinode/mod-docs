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

The `preview` content block renders a live URL preview in an iframe with device switcher controls. By default it uses `activation: load`, offers desktop, tablet, and mobile views, enables controls, and uses the legacy `frame: none` layout. Those defaults preserve the existing load behavior when the new options are omitted; the markup gains `data-src`, `data-devices`, and `data-load-timeout` attributes and a hidden unavailable block.

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

When Hugo's build-time checks find that a target's response policy refuses framing, or this site's published `frame-src` policy excludes the target, the block renders its fallback. For `X-Frame-Options: SAMEORIGIN`, the target is allowed when it shares this site's origin; `frame-ancestors` takes precedence when present. Provide an `image` argument to display a representative screenshot in place of the blocked iframe. The warning alert with a direct link is still shown below the image.

Set `show_fallback: true` in Bookshop content (or `show-fallback: true` when calling the Hugo partial) to force the fallback explicitly — useful when the build cannot verify a target URL, or when you know it cannot be embedded on your site.

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

When the build checks a remote preview URL, it tries HEAD first and retries with GET only when the HEAD request returns an error, such as Hugo rejecting that method. Hugo's default security policy only allows `GET` and `POST` methods, so allowing HEAD avoids the retry. Add the following to your site's `config/_default/hugo.toml`:

```toml
[security]
  [security.http]
    methods = ['(?i)GET|POST|HEAD']
    urls = ['.*']
```

[Embedding restrictions](#embedding-restrictions) describes how the build handles a request that fails. Use `show_fallback: true` to force the fallback explicitly — it is not affected by this setting.

### Embedding restrictions

Many websites prevent iframe embedding using `X-Frame-Options` or `Content-Security-Policy` response headers. When this site's base URL has a host and the block has not already selected its fallback, Hugo checks each target URL. For URLs with a host, it requests response headers, trying HEAD and then GET when HEAD returns an error, and compares the target's framing policy with this site's configured origin. Site-relative URLs are resolved against the base URL and skip the remote header request. After a successful header check, or a warning when the request fails, Hugo checks the URL against this site's published `frame-src` policy, when one exists. The block shows its fallback when either policy refuses framing. The table describes target response headers when they are available:

| Response header | Build-time action |
| --- | --- |
| `X-Frame-Options: SAMEORIGIN` | Fallback rendered only when the target and this site have different origins |
| `X-Frame-Options` with another value | Fallback rendered |
| `Content-Security-Policy: frame-ancestors` excluding this site's configured origin | Fallback rendered |
| `Content-Security-Policy: frame-ancestors` allowing this site's configured origin | No fallback from the target policy |
| No relevant target headers | No fallback from the target policy; this site's `frame-src` is still checked |

When the target's CSP declares `frame-ancestors`, Hugo ignores its `X-Frame-Options` header.

When the header request fails, Hugo warns that it could not verify embedding restrictions and continues to the `frame-src` check; that check may still select the fallback. A HEAD answer of 404 Not Found is not an error to Hugo, so the build does not retry with GET; it warns that the request failed with `<nil>`. In either case the build cannot see the target's headers: unless the `frame-src` check selects the fallback, the block renders live, and only the runtime `load_timeout` and `ready_message` handling remains. Use `show_fallback: true` when you know embedding will fail.

**Best practices:**

- Use the preview component for sites you control or that explicitly allow embedding
- Test URLs in development before deploying
- Set `image` to a representative screenshot so users see meaningful content when embedding is blocked
- Use `show_fallback: true` when the build cannot verify a URL or you know the target cannot be embedded on your site
- Use embeddable alternatives (e.g., youtube-nocookie.com instead of youtube.com)

## Device dimensions

Device dimensions use **logical pixels** (CSS pixels), which is what browsers and responsive design tools use for layout. Physical pixels depend on the device pixel ratio (DPR) of the hardware display.

| Device | Logical resolution | Aspect ratio | DPR reference |
| -------- | ------------------- | -------------- | --------------- |
| Desktop | 1440 × 900px | 16:10 | @1× (MacBook / laptop) |
| Tablet | 820 × 1180px | ~9:13 | @2× (iPad 10th gen / iPad Air M2) |
| Mobile | 402 × 874px | 9:19.5 | @3× (iPhone 17 Pro, 460 ppi) |

A website loaded inside the iframe sees a viewport matching these logical pixel dimensions, so breakpoints and responsive layouts behave exactly as they would on the real device.

### Auto-scaling

JavaScript scales each device on page load and on every browser resize. Tablet and mobile always use a **contain fit** — the largest scale where neither dimension is clipped:

```text
scale = min(containerWidth / deviceWidth, containerHeight / deviceHeight, 1)
```

Desktop scaling depends on the `desktop_responsive` argument:

| Mode                 | `desktop_responsive`   | Behaviour                                                                                                                                                           |
| -------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Responsive (default) | `true`                 | Scales to fill the full container width; iframe height is adjusted dynamically so the container height is also filled. The site inside sees a 1440px-wide viewport. |
| Strict aspect ratio  | `false`                | Contain fit — the full 1440 × 900px frame is always visible; symmetric gaps may appear above and below on wide containers.                                          |

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
sandbox="allow-scripts allow-same-origin allow-forms allow-popups allow-storage-access-by-user-activation"
```

This restricts iframe capabilities while allowing:

- JavaScript execution (`allow-scripts`)
- Access to same-origin resources (`allow-same-origin`)
- Form submissions (`allow-forms`)
- Opening popups/new windows (`allow-popups`)
- Letting an embedded page request storage access after user activation (`allow-storage-access-by-user-activation`)

### Choose device views

Set `devices` to the subset of device views to offer, in the order their controls appear. The default is desktop, tablet, and mobile. Set `controls: false` to hide the switcher; the component then selects the largest offered view that fits the viewport and switches as the viewport crosses a device breakpoint. A `device` that is not in `devices` falls back to the first offered view.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: preview
  url: "https://en.wikipedia.org/wiki/Hugo_(software)"
  devices: [desktop, mobile]
  controls: false
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Load on click

Set `activation: click` to show a poster and defer navigation until a visitor activates the preview. The active view loads on activation; other views load the first time they are shown. A view without its own poster uses the desktop poster. Set `mode: true` to use light and dark posters: Hinode then requests both the `-light` and the `-dark` variant of each poster file and never falls back to the unsuffixed file, so both variants must exist.

### Load when visible

Set `activation: visible` to start navigation for the shown device view when the preview actually enters the viewport. It first waits for the parent page to finish loading, then gives the browser an idle opportunity, with a 600ms timeout. This timeout bounds the wait for idle; it is not a required delay. If the preview leaves the viewport before then, it does not navigate; it waits until the preview enters again and becomes eligible. The observer and idle callback have guarded fallbacks when those browser APIs are unavailable. This delays navigation; it does not preload the page or promise zero cost. It also does not monitor the page after its initial navigation.

```yml
url: /example/
activation: visible
```

### Keep narrow screens static

Set `mobile_static: true` (default `false`) to keep the preview static below 1024px. At those widths the page renders a poster image, falling back to the `image` argument when no poster is supplied, or a neutral background when neither is. The component makes no embedded-page navigation request there, including after scrolling, resizing, or waiting. Returning to desktop follows the configured `activation` mode; `click` still requires a new click. This option does not add a tablet layout.

```yml
url: /example/
activation: visible
mobile_static: true
```

### Window frame

Set `frame: window` (default `none`) to contain the desktop page in its native 1440×900 (16:10) viewport, with title-bar chrome. After measuring navigation and title-bar height, the window fits the available width and height with 24px above and below when space allows. In tighter but feasible spaces, decorative chrome compacts first to preserve the top-right open action, and margins shrink as needed. If navigation plus the minimum accessible chrome and native viewport cannot fit, a scroll fallback retains the available native viewport and reachable open action; resizing back to a feasible space restores the fitted layout. The viewport is never cropped. The window stays centered in the existing full-width section. Its usual appearance and native device ratios remain unchanged; no minimum supported height is implied. `frame_title` (default empty) supplies the optional title and, for a single URL, the iframe's accessible title. The title bar is outside the 1440×900 page viewport. Tablet and mobile keep their native 820×1180 and 402×874 viewports.

With `open_link: true`, the window has one open action in its top-right title bar, including while static or showing a fallback. For a single URL, `open_url` (default empty) takes priority over `url`. Items require a `url`; the shown item's `open_url` takes priority over its own `url`. Item titles remain the titles of their own frames.

```yml
url: /preview-demo/ready/
frame: window
frame_title: Example workspace
open_link: true
controls: false
devices: [desktop]
activation: visible
mobile_static: true
ready_message: example:ready
mode: true
poster:
  desktop: img/poster-desktop.png
```

See the [window preview example](https://github.com/gethinode/mod-blocks/blob/v2.13.0/exampleSite/content/components/preview-window.md) for the complete runnable source. It uses a local child page and stays static below 1024px.

### Window states and appearance

The window title bar shows `Preview` before its current view is admitted, `Loading` while it waits (a re-proof of a ready view keeps `Live`, see below), `Live` after the current view passes its configured readiness check, and `Unavailable` when a wait times out. Without `ready_message`, the iframe load event ends the wait; with it, the current frame must post that exact message. Theme synchronization adds a matching current-theme acknowledgement before `Live`. In a compact title bar, a shorter visible state such as `Wait` or `Error` sits beside the open action; the full accessible status remains available.

While a view is loading or has failed, a 30% black scrim sits over its poster, with the status and spinner painted above the scrim. A ready view removes the poster and scrim, and from mod-blocks v2.13.1 a ready view that re-proves a new document or theme keeps them removed. A static phone view stays in `Preview` without a loading spinner or scrim because it makes no embedded-page request.

The window open action uses the theme's existing `externalLink` icon mapping, whose default is a generic external-link glyph. The window's CSS custom property `--preview-window-border-radius` overrides the Sass fallback `$preview-window-border-radius` (default `0.375rem`) without changing other theme corners. A site can set the custom property, for example to `0`, to choose square window corners.

The block forwards the existing section `padding` option. Leave it unset to retain the section's default spacing, or set `padding: 0` to remove the content's padding on both axes. Without `fluid: true`, the outer container keeps the site's horizontal padding, so the section's edge still lines up with other sections.

### Readiness with a local child page

`ready_message` can wait for an exact reply from a page that you control. The [readiness example](https://github.com/gethinode/mod-blocks/blob/v2.13.0/exampleSite/content/components/preview-ready.md) uses `example:ready` and also sets `theme_message: example:theme`: its Ready child announces after the DOM is ready and answers requests only from its own parent, while its Silent child never announces. The example demonstrates the matching request/reply protocol without treating readiness as an ongoing health check.

### Synchronize an embedded page's theme

Set `theme_message` to opt a cooperating child page into synchronization with the outer page's resolved light or dark theme. The argument defaults to empty and requires a nonempty `ready_message`; omitting it preserves ordinary readiness behavior. Use distinct tokens for readiness and theme requests. When calling the Hugo partial directly, use `theme-message`. This code-only Bookshop configuration uses the public example tokens and the producer example site's local Ready page:

```yml
url: /preview-demo/ready/
frame: window
activation: visible
mobile_static: true
ready_message: example:ready
theme_message: example:theme
```

When adapting the snippet to your own site, use a child page your site serves instead of `/preview-demo/ready/`.

After the current child sends its readiness message, the parent requests the resolved theme with a unique positive safe-integer request ID, for example `{type: "example:theme", theme: "dark", requestId: 1}`. The parent sends only to that frame's captured nonopaque HTTP(S) origin. The child validates the message from its actual parent and exact parent origin, applies the requested theme, then replies with the same fields and `applied: true`. For the first reveal of an activation, the parent reveals the view only after an acknowledgement from the current frame window at its captured origin matches the request ID and theme. A new child document or theme request needs a fresh matching acknowledgement; an old or out-of-order reply cannot reveal the view. A view that was already ready re-proves in place instead, as described below. The parent resolves `auto` to light or dark before sending the request.

For full-document navigation, the bridge carries transient theme intent in a `window.name` seed beginning `hinode-preview-theme:` followed by `{type, theme, requestId, parentOrigin}` JSON. The initial seed uses request ID `0`; theme requests use positive safe integers. Keep the complete seed within 512 JavaScript string code units and use a canonical HTTP(S) parent origin. A participating child reads the seed as early theme context and mirrors each validated request into its own `window.name` before acknowledging; the seed alone is not readiness or proof that the theme was applied. This context is not a cookie or stored preference.

On `pagehide` and early startup of a newly navigated document, a participating child sends a matching `applied: false` invalidation. The parent also invalidates the current theme proof on the iframe's load event. A current invalidation requires a fresh readiness message, theme request, and `applied: true` acknowledgement before the view counts as ready again. From mod-blocks v2.13.1, a view that was already ready in its current activation re-proves in place: its frame stays shown and not inert, its poster stays hidden, the pane is busy, and a window's title bar keeps its ready state (`Live`) without a new status announcement until the acknowledgement arrives. A new outer theme re-proves the same way. The first wait of an activation, and any wait after a failure, still returns the frame to its poster and makes it inert, and the deadline still fails a re-proof with the poster and alert and an inert, hidden frame. A late acknowledgement from the current frame still recovers. Earlier releases show the poster again on every such invalidation and theme change. Signals from an older document or superseded request cannot invalidate newer proof.

Hinode also exposes the synchronous, cancelable document event `hinode:color-mode:before-change` (Hinode v3.45.0 or later). Its `detail.theme` is the requested preference (`auto`, `light`, or `dark`); invalid values normalize to `auto`. When not canceled, `auto` resolves to system appearance after dispatch. Calling `preventDefault()` skips that setter's preference storage, root theme attributes, and selector updates, but does not undo earlier preference reads/writes or native control changes. Without cancellation, normal theme behavior remains. Hinode provides only this event; it does not manage a framed child's theme selector. A cooperating child page managed by its preview parent may cancel this event to intercept local setter updates while managed, then apply the parent's resolved theme without persisting it. The child may also hide its own duplicate theme selector while managed so the outer page remains authoritative, and keep its normal selector behavior when standalone or unmanaged.

### Guarded loading and browser policy

`activation: visible`, `mobile_static: true`, and a nonempty `theme_message` use a guarded loading path. Their iframe begins with a literally empty, script-free `srcdoc` in the same browsing context. The resulting `about:srcdoc` load only releases the guard; it is never treated as the child page's readiness and never starts or resets its load deadline. The actual URL is opened with `Location.replace` only after the blank document has completed and the current iframe, owner document, controller generation, and activation mode still admit navigation. Unconfigured legacy `load` and `click` previews keep their existing behavior.

These enhanced modes require native custom-element lifecycle callbacks (`customElements.define`/`get` and `HTMLElement`) so removal or adoption can release ownership synchronously. They also require an HTTP(S) parent and target, the preview iframe's `no-referrer-when-downgrade` policy, and a sandbox that permits same-origin access. An opaque sandbox or a different, stricter element referrer policy is incompatible, and an HTTPS page will not load an HTTP child. If a capability or policy check fails, the child is not requested; the preview stays in its static `Preview` state with its poster or neutral background and any configured open action. The guard keeps the page's existing `Referrer-Policy` and iframe policy; it does not widen either policy to enable navigation. The standard Hinode `strict-origin` document policy with the preview's compiled `no-referrer-when-downgrade` iframe policy is supported. These are enhanced-mode requirements, not a general guarantee for every third-party theme or browser.

### Window with item-specific links

When a window contains `items`, its title-bar action follows the shown item. Each item requires a `url`; its own `open_url` wins over that URL. Legacy previews without `frame: window` keep the open link below the frame.

### Keep the existing defaults

Omitting the new options keeps the existing load behavior and legacy frame. `activation` defaults to `load`; `frame_title` and `open_url` default to empty, and `mobile_static` defaults to `false`. All three device views and the controls remain enabled by default. `activation: load` can still put the selected URL in the initial HTML; that initial navigation has no `load_timeout` deadline when `ready_message` is empty. Navigations started later by the script use the deadline.

```yml
url: https://example.org/
```

This keeps the current load activation, all three device views, controls, and legacy frame. The six focused producer pages cover:

- [Basic preview](https://github.com/gethinode/mod-blocks/blob/v2.13.0/exampleSite/content/components/preview.md)
- [Click activation](https://github.com/gethinode/mod-blocks/blob/v2.13.0/exampleSite/content/components/preview-click.md)
- [Device selection](https://github.com/gethinode/mod-blocks/blob/v2.13.0/exampleSite/content/components/preview-devices.md)
- [Items](https://github.com/gethinode/mod-blocks/blob/v2.13.0/exampleSite/content/components/preview-items.md)
- [Readiness](https://github.com/gethinode/mod-blocks/blob/v2.13.0/exampleSite/content/components/preview-ready.md)
- [Window, visible activation, and static narrow view](https://github.com/gethinode/mod-blocks/blob/v2.13.0/exampleSite/content/components/preview-window.md)

These examples use local child pages in the producer's example site rather than remote framing targets. The basic page becomes live; click activation waits for the poster button; device and item examples change the offered view; readiness contrasts a replying Ready page with a Silent page that reaches its timeout; and the window example combines visible activation with a static narrow-screen view. The light/dark posters match their child page and device.

### Switch between items

Set `items` to an ordered list of views. Every item needs a `title` and `url`; optional `open_url`, `poster`, and `heading` values customize its open link, poster, and heading. Items replace `url` (when both are set, the first item URL is used). Switching items keeps the selected device, and only the shown item's URL is loaded in the shown device. Item posters fall back from the selected device to that item's desktop poster, then to the block poster.

> **Item headings.** An item heading appears with its tab. If an item has no heading, the block heading is used. A build-time fallback has no item tabs and displays the first item's heading, when supplied.

### Runtime loading, fallback, and readiness

The active view loads by default; views load when first shown. `activation: click` adds an explicit visitor action before any view loads. `load_timeout` sets the per-navigation deadline in seconds (default 15), starting when a waiting view enters the viewport. On timeout, the frame shows an alert; a supplied poster remains behind the alert. With the default `frame: none`, the alert includes a link to open the target. With `frame: window`, the alert has no link; only the title-bar open action, shown with `open_link: true`, opens the target. Without a poster, the alert appears against the frame background. With an empty `ready_message`, the initial frame whose `src` is in the markup has no deadline because it may load before the script starts; navigations started later by the script are timed. A page-relative URL is resolved on this site.

The iframe `load` event does not prove the target is healthy: browsers can fire it for an HTTP 503 response or a refused connection. With the default empty `ready_message`, load ends the wait. To wait for positive readiness, set `ready_message` to a token shared with a cooperating framed page. For example, the self-contained [readiness example](https://github.com/gethinode/mod-blocks/blob/v2.13.0/exampleSite/content/components/preview-ready.md) uses `example:ready`. A child page can announce readiness after its DOM is ready and answer only requests from its own parent that contain the matching token. The preview requests a reply when the frame loads, so an early announcement can be recovered. The example's Ready page replies; its Silent page does not.

When a live view loads in readiness mode, it stays busy behind its poster and its frame cannot take focus until the current frame acknowledges the exact token. If the deadline expires first, the frame is hidden and stays inert, so it still cannot take focus. With click activation, before the poster button is pressed, item changes update the selected poster and item heading, when supplied, without requesting a frame or starting a wait. After activation, each item or device navigation gets its own wait. A late acknowledgement from the current frame can recover the view. Messages from another frame, a previous navigation, or with a different token do not count. This is a one-time navigation check, not ongoing health monitoring; without `theme_message`, behavior after the framed app navigates internally belongs to that app. With `theme_message` (mod-blocks v2.13.1 or later), each new document of a ready view re-proves as described under [Synchronize an embedded page's theme](#synchronize-an-embedded-pages-theme). Keep the token non-sensitive: messages must not carry visitor data, privileged actions, URLs, or HTML.

The build-time fallback remains distinct from runtime failure: a block that shows its fallback has no waiting or failed runtime state. [Embedding restrictions](#embedding-restrictions) describes when the build-time checks run and how a failed request is handled.

### Open link and buttons

Set `open_link: true` to show an open link. With the default `frame: none`, it appears under the frame and opens the current item's `open_url`, or its `url`; without items it opens the block `open_url`, or its `url`. With `frame: window`, it appears in the title bar. Links open in a new tab with `noopener`. Set `links` to render additional buttons under the frame, each with a `title` and `url`. A window's title-bar action remains available with a static poster or build-time fallback; runtime failure feedback does not add a duplicate action. Legacy previews keep their existing below-frame link and load behavior.

## Arguments

The content block supports the following arguments:

{{< args bookshop-preview >}}
