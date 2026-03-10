---
_schema: default
title: Articles
description: Use the articles block to show a group of article cards.
type: docs
tags: block
---

## Overview

The `articles` block renders a group of cards for selected content. By default, the block uses the content of the current section. You can override this by setting `input.section` to the name of a specific section of your site.

### Stacked cards

 Set `orientation` to `stacked` to render the article's illustration above the card body.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: articles
  heading:
    title: Blog
    align: start
  input:
    section: blog
    reverse: false
    sort: date
  hide_empty: false
  header_style: none
  orientation: stacked
  more:
    title: More Blogs
  padding: 0
  limit: 3
  background:
    color: body-tertiary
    subtle: false
  class: border-0 card-zoom card-body-margin
  justify: start
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Horizontal cards

Set `orientation` to `horizontal` to render the article's illustration before the card body.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: articles
  heading:
    title: Blog
    align: start
  input:
    section: blog
    reverse: false
    sort: date
  hide_empty: false
  header_style: none
  body_style: title
  orientation: horizontal
  more:
    title: More Blogs
  padding: 3
  limit: 3
  background:
    color: body-tertiary
    subtle: false
  class: card-zoom card-body-margin
  justify: start
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Rich cards

Adjust the `header_style`, `body_style`, and `footer_style` to refine the card elements being displayed.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: articles
  heading:
    title: Blog
    align: start
  input:
    section: blog
    reverse: false
    sort: date
  hide_empty: false
  header_style: publication
  body_style: full
  footer_style: tags
  orientation: stacked
  more:
    title: More Blogs
  padding: 0
  limit: 3
  background:
    color: body-tertiary
    subtle: false
  class: border-0 card-zoom card-body-margin
  justify: start
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Minimal cards

Set `body_style` to `minimal` to show the title of an article only. The predefined `class` attribute `card-minimal` applies an underline effect on hover.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: articles
  hide_empty: false
  input:
    section: blog
    reverse: false
    sort: date
  more:
    title: More Blogs
  cols: 5
  padding: 0
  cover: false
  header_style: none
  body_style: minimal
  class: card-minimal
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

## Arguments

The articles block supports the following arguments:

{{< args bookshop-articles >}}
