---
_schema: default
title: Hero
description: >-
  Shows a hero banner on the top of the page. The section supports a background
  image with an overlay to improve contrast. The hero includes a headline and
  optional breadcrumb for site navigation.
type: docs
tags: block
---

## Overview

### Basic hero

The `hero` content block renders a page hero, typically at the top of the page. Set `cover` to true to display a full-page hero.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: hero
  heading:
    title: Title
    align: start
    content: Hero content
    width: 12
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Illustrated hero

You can include an `illustration` next to the hero heading. Specify `orientation` and `order` to configure the illustration's placement. You can set `cover` to true to display a full-height hero. In horizontal layout, `heading.width` sets how many Bootstrap columns the heading occupies (1–12); the illustration fills the remaining columns. Use `illustration.width` to further constrain the image within its column (1–12).

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: hero
  background:
    color: body-tertiary
    subtle: false
  heading:
    title: Title
    align: start
    content: Hero content
    width: 8
  orientation: horizontal
  order: last
  illustration:
    image: /img/placeholder.png
    ratio: 1x1
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Image sizing

Use `illustration.width` to constrain the image within its column. In the example below,
`heading.width: 8` allocates 8 columns to the heading (leaving 4 for the illustration), and
`illustration.width: 10` renders the image at 10/12 of that 4-column container.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: hero
  heading:
    title: Title
    align: start
    content: Hero content
    width: 8
  orientation: horizontal
  order: last
  illustration:
    image: /img/placeholder.png
    ratio: 3x2
    width: 10
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Hero with breadcrumb

Set `breadcrumb` to `true` to add a breadcrumb to the top of the hero.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: hero
  heading:
    title: Title
    align: start
    content: Hero content
    width: 12
  breadcrumb: true
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Hero with backdrop

Adjust the background of the hero by configuring a `backdrop` that links to an image asset.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: hero
  heading:
    title: Title
    align: start
    content: Hero content
    width: 12
  background:
    backdrop: /assets/img/logan-voss-dAo9K7PG1kQ-unsplash.jpg
  breadcrumb: true
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

## Arguments

The content block supports the following arguments:

{{< args bookshop-hero >}}
