---
_schema: default
title: Testimonials
description: Use the testimonials content block to display one or more client testimonials.
type: docs
tags: block
---

## Overview

The `testimonials` content block renders one or more client testimonials. You can render them as a carousel or as columns.

### Carousel

Set `carousel` to `true` to render a carousel of multiple testimonials.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: testimonials
  card:
    color: body-tertiary
    subtle: false
  cols: 1
  icon_style: fa-4x
  carousel: true
  testimonials:
    - icon: fab linkedin
      content: First testimonial.
      link: #!
    - icon: fab google
      content: Second testimonial.
      link: #!
    - icon: fab github
      content: Third testimonial.
      link: #!
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Columns

Set `cols` to `3` to render three testimonials as columns.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: testimonials
  card:
    color: body-tertiary
    subtle: false
  cols: 3
  icon_style: fa-2x
  carousel: false
  testimonials:
    - icon: fab linkedin
      content: First testimonial.
    - icon: fab google
      content: Second testimonial.
    - icon: fab github
      content: Third testimonial.
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Minimal

Set `responsive` to `false` and omit any content to render a minimal, horizontal stack of icons.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
  - _bookshop_name: testimonials
    cols: 5
    background:
      color: body-tertiary
    icon_style: fa-fluid text-secondary
    align: center
    responsive: false
    testimonials:
      - icon: fab github
      - icon: fab node
      - icon: fab unsplash
      - icon: fab font-awesome
      - icon: fab sass
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->


## Arguments

The content block supports the following arguments:

{{< args bookshop-testimonials >}}
