---
_schema: default
title: Contact form
description: Use the contact form content block to display a contact form with server-side forms integration.
type: docs
tags: block
---

## Overview

The `contact-form` content block renders a contact form powered by a form provider of your choice. Provide a render hook and action to link your custom form and callback action to the content block.

### Netlify Contact Form

[Netlify Forms](https://www.netlify.com/products/forms/) provides serverless form handling, allowing you to manage forms without extra API calls or additional JavaScript. You can enable form detection by including a `data-netlify` or `netlify` attribute.

The following render hook uses automatic form detection by Netlify. The form itself includes fields for name, email address, and a message. It uses a honeypot field and reCAPTCHA v2 to reduce spam submissions.

{{< file file="./layouts/_partials/assets/netlify-contact-form-hook.html" show=false >}}

> [!IMPORTANT]
> The render hook example sets `data-netlify="false"` to reduce noise on the current website. Set it to `true` to enable automatic form detection by Netlify.

Assign the render hook and callback action using the `hook` and `action` arguments. For a live form, replace the demo action `#!` with the path to your confirmation page, such as `/thank-you/` or `/nl/bedankt/`. Use a path starting with `/` to avoid resolving it relative to the contact page.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: contact-form
  heading:
    preheading: Get in touch
    title: Contact Us
    content: We'd love to hear from you. Send us a message and we'll respond as soon as possible.
  hook: assets/netlify-contact-form-hook.html
  action: #!
  background:
    color: body-tertiary
    subtle: false
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

#### Allowing reCAPTCHA in the Content Security Policy

Hinode's default Content Security Policy (CSP) does not allow all resources required by reCAPTCHA. Add the following policy to your site's `config/_default/params.toml`:

```toml
[modules.recaptcha.csp]
    script-src = ["www.google.com", "www.gstatic.com"]
    frame-src = ["www.google.com", "recaptcha.google.com"]
    connect-src = ["www.google.com"]
```

These sources allow the scripts, frames, and connections required by [Google's reCAPTCHA CSP guidance](https://developers.google.com/recaptcha/docs/faq#im-using-content-security-policy-csp-on-my-website-how-can-i-configure-it-to-work-with-recaptcha). Use hostnames in this configuration; the CSP module does not support source values containing URL paths.

Regenerate the development and production server headers:

```sh
pnpm run build:headers
```

This updates `config/_default/server.toml` and `netlify.toml`. Commit the policy and generated headers, restart the local server if running, and deploy the changes to Netlify. See [Server headers](https://gethinode.com/docs/advanced-settings/server-headers/) for the header-generation setup.

If the CAPTCHA does not appear, check the browser console for CSP violations. Netlify rejects submissions without a valid CAPTCHA response. A nonce added by a plugin does not bypass an enforced CSP that blocks the script; a report-only policy does not relax the enforced policy.

### Illustrated Contact Form

You can render an illustrated contact form by assigning a value to `illustration`:

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: contact-form
  heading:
    preheading: Get in touch
    title: Contact Us
    content: We'd love to hear from you. Send us a message and we'll respond as soon as possible.
  illustration:
    image: /img/placeholder.png
    class: d-none d-md-block
  hook: assets/netlify-contact-form-hook.html
  action: #!
  background:
    color: body-tertiary
    subtle: false
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

## Arguments

The content block supports the following arguments:

{{< args bookshop-contact-form >}}
