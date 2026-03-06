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
  icon_style: fa-4x text-secondary
  carousel: true
  testimonials:
    - icon: linkedin
      content: First testimonial.
      link: #!
    - icon: google
      content: Second testimonial.
      link: #!
    - icon: github
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
  icon_style: fa-2x text-secondary
  carousel: false
  testimonials:
    - icon: linkedin
      content: First testimonial.
    - icon: google
      content: Second testimonial.
    - icon: github
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
    icon_style: fa-2xl text-secondary
    align: center
    responsive: false
    testimonials:
      - icon: github
      - icon: google
      - icon: linkedin
      - icon: facebook
      - icon: pinterest
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->


## Arguments

The content block supports the following arguments:

{{< args bookshop-testimonials >}}
