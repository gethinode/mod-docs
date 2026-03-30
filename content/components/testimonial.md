---
author: Mark Dumay
title: Testimonial
date: 2026-03-30
description: Use the testimonial shortcode to display a quote with attribution.
type: docs
tags: component
weight: 335
---

## Overview

Use the `testimonial` shortcode to display a quote with attribution. The testimonial supports a contact name, role, avatar image, logo, or icon. You can optionally link the contact name to a URL and add a call-to-action link.

### Basic testimonial

Provide inner content as the quote.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* testimonial */>}}
  Hinode has transformed the way we publish documentation. It is fast, flexible,
  and a joy to use.
{{</* /testimonial */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

### Testimonial with avatar

Add `image` to display a circular avatar next to the contact name.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* testimonial contact="Jane Smith" role="CEO, Acme Corp"
    image="/img/placeholder.png" */>}}
  Hinode has transformed the way we publish documentation. It is fast, flexible,
  and a joy to use.
{{</* /testimonial */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

### Testimonial with logo

Use `logo` to display a company or brand logo above the quote.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* testimonial contact="Jane Smith" role="CEO, Acme Corp"
    image="/img/placeholder.png" logo="/img/placeholder.png" */>}}
  Hinode has transformed the way we publish documentation. It is fast, flexible,
  and a joy to use.
{{</* /testimonial */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

### Testimonial with icon

Use `icon` instead of `logo` to display a Font Awesome icon above the quote. Use `icon-style` to adjust the icon size.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* testimonial contact="Jane Smith" role="CEO, Acme Corp"
    icon="fas quote-left" icon-style="fa-3x" */>}}
  Hinode has transformed the way we publish documentation. It is fast, flexible,
  and a joy to use.
{{</* /testimonial */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

### Horizontal orientation

Set `orientation` to `horizontal` to display the avatar in a column to the left of the quote instead of inline below it.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* testimonial contact="Jane Smith" role="CEO, Acme Corp"
    image="/img/placeholder.png" orientation="horizontal" */>}}
  Hinode has transformed the way we publish documentation. It is fast, flexible,
  and a joy to use.
{{</* /testimonial */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

### Colored testimonial

Use `color` to apply a Bootstrap theme color as the background.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* testimonial contact="Jane Smith" role="CEO, Acme Corp"
    image="/img/placeholder.png" color="primary" padding="4" */>}}
  Hinode has transformed the way we publish documentation. It is fast, flexible,
  and a joy to use.
{{</* /testimonial */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

### Testimonial with case study

Use `link` to add a call-to-action button pointing to a case study.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* testimonial 
    image="/img/placeholder.png"
    link="https://example.com/case-study" */>}}
  Hinode has transformed the way we publish documentation. It is fast, flexible,
  and a joy to use.
{{</* /testimonial */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

## Styling

The file `assets/scss/components/_testimonial.scss` defines the Hinode-specific styling of the `testimonial` shortcode.

{{< file file="assets/scss/components/_testimonial.scss" show="false" >}}

## Arguments

The shortcode supports the following arguments:

{{< args structure="testimonial" group="shortcode" >}}
