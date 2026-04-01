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

{{< file file="layouts/_partials/assets/netlify-contact-form-hook.html" >}}

> [!IMPORTANT]
> The render hook example sets `data-netlify="false"` to reduce noise on the current website. Set it to `true` to enable automatic form detection by Netlify.

Assign the render hook and callback action using the `hook` and `action` arguments:

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

## Arguments

The content block supports the following arguments:

{{< args bookshop-contact-form >}}
