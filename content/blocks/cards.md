---
_schema: default
title: Cards
description: Use the cards block to show a group of content cards.
type: docs
tags: block
---

## Overview

The `cards` content block renders a group of content cards. You can define the card's content, including an illustration, using frontmatter inputs.

### Stacked cards with an image

Set the `image` attribute of each `element` to an image asset to render illustrated cards.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: cards
  heading:
    preheading: Preheading
    title: Heading
    content: Cards content. It supports multiple lines.
    align: start
  background:
    color: body-tertiary
    subtle: false
  orientation: stacked
  class: bg-body
  align: center
  elements:
    - title: First Card
      image: /img/placeholder.png
    - title: Second Card
      image: /img/placeholder.png
    - title: Third Card
      image: /img/placeholder.png
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Horizontal cards with an image

Set the `orientation` attribute to `horizontal` to render horizontally oriented cards.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: cards
  heading:
    preheading: Preheading
    title: Heading
    content: Cards content. It supports multiple lines.
    align: start
  background:
    color: body-tertiary
    subtle: false
  orientation: horizontal
  class: bg-body
  align: center
  elements:
    - title: First Card
      image: /img/placeholder.png
      content: Content of the first card
    - title: Second Card
      image: /img/placeholder.png
      content: Content of the second card
    - title: Third Card
      image: /img/placeholder.png
      content: Content of the third card
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Stacked cards with an icon

Set the `icon` attribute of each `element` to an icon to render illustrated cards. Adjust the icon's styling with `icon-rounded` and `icon-style`.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: cards
  heading:
    preheading: Preheading
    title: Heading
    content: Cards content. It supports multiple lines.
    align: start
  background:
    color: body-tertiary
    subtle: false
  orientation: stacked
  icon_style: text-primary
  align: start
  padding: 0
  elements:
    - title: First Card
      icon: 1-circle
      content: Content of the first card
    - title: Second Card
      icon: 2-circle
      content: Content of the second card
    - title: Third Card
      icon: 3-circle
      content: Content of the third card
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Horizontal cards with an icon

Set the `icon` attribute of each `element` to an icon to render illustrated cards. Adjust the icon's styling with `icon-rounded` and `icon-style`.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: cards
  heading:
    preheading: Preheading
    title: Heading
    content: Cards content. It supports multiple lines.
    align: start
  background:
    color: body-tertiary
    subtle: false
  orientation: horizontal
  icon_style: text-primary
  align: start
  padding: 0
  elements:
    - title: First Card
      icon: 1-circle-fill
      content: Content of the first card
    - title: Second Card
      icon: 2-circle-fill
      content: Content of the second card
    - title: Third Card
      icon: 3-circle-fill
      content: Content of the third card
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Aligned rows

Set `align_rows` to `true` to line up the parts of the cards in each row: the image or icon, the title, the subtitle, the highlight, the content, and the button of an element with a `link`. Add a `subtitle` and a `highlight` to each element to show a tagline and a key figure between the title and the content. Both fields support inline Markdown.

Alignment applies to stacked cards only, so set `orientation` to `stacked`. It has no effect on horizontal cards. Without an explicit `orientation`, the block shows horizontal cards on small screens, where alignment does not apply. Alignment uses CSS subgrid; browsers without subgrid support show the regular layout.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: cards
  heading:
    preheading: Pricing
    title: Aligned rows
    content: The titles, subtitles, highlights and content of the cards line up.
    align: start
  background:
    color: body-tertiary
    subtle: false
  orientation: stacked
  align_rows: true
  icon_style: text-primary
  align: start
  padding: 0
  elements:
    - title: Starter
      icon: fas seedling
      subtitle: For individuals.
      highlight: "**€0** per month"
      content: |
        - One project
        - Community support
    - title: Team
      icon: fas users
      subtitle: For growing teams that share their projects.
      highlight: "**€9** per user per month"
      content: |
        - Unlimited projects
        - Shared workspaces
        - Priority support
    - title: Enterprise
      icon: fas building
      subtitle: >-
        For organizations with *custom* needs, such as single sign-on and
        audits.
      highlight: "**Custom pricing**"
      content: |
        - Dedicated account manager
        - Custom contracts
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

## Arguments

The content block supports the following arguments:

{{< args bookshop-cards >}}
