---
_schema: default
title: List
description: Use the list content block to show a list of articles.
modules: ["simple-datatables"]
type: docs
tags: block
---

## Overview

The `list` block renders a list of articles.

### Default List

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: list
  heading:
    title: Recent articles
    align: start
  input:
    section: blog
    reverse: true
    sort: date
  hide_empty: false
  background:
    color: body-tertiary
    subtle: false
  justify: start
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Filtered List

Add the following configuration to your page's frontmatter to enable data table features:

```yml
---
modules: ["simple-datatables"]
---
```

You can then use `sortable`, `paginate`, and `searchable` to enable inline sorting and filtering.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: list
  heading:
    title: Recent articles
    align: start
  input:
    section: blog
    reverse: false
    sort: date
  pagination: 5
  hide_empty: false
  background:
    color: body-tertiary
    subtle: false
  justify: start
  sortable: true
  paginate: true
  searchable: true
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Category Filter

Use `filter` to add a button group above the table that shows only rows matching a specific category. Set `filter_col` to the zero-indexed column in your hook's table that contains the category value. An **All** button is always prepended and selected by default.

The filter works alongside `sortable`, `paginate`, and `searchable` — sorting and pagination continue to operate on the filtered result set.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: list
  heading:
    title: Recent articles
    align: start
  input:
    section: blog
    reverse: false
    sort: date
  hide_empty: false
  hook: assets/table-filter-hook
  filter:
    - featured
    - tutorial
  filter_col: 1
  sortable: true
  background:
    color: body-tertiary
    subtle: false
  justify: start
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

Define the hook partial in your site's `layouts/_partials` folder. The following example renders a custom Markdown table that includes a `category` column sourced from each page's front matter.

{{< file file="./layouts/_partials/assets/table-filter-hook.html" full=false lang="go-template" >}}

Set `filter_responsive` to replace the button group with a dropdown below the site's main breakpoint. A group of more than a few categories is wider than a phone, and the button group does not wrap. The dropdown and the button group stay in step, so moving across the breakpoint never changes which category is selected. It defaults to `false`, so a list keeps its button group at every width unless you ask otherwise.

### Responsive Tables

A table with several columns runs off the side of a small screen. Set `wrap` to move a record's last column onto a row of its own below the site's main breakpoint, which is usually enough when one column holds most of the width — a description, say.

Set `wrap_cols` when it is not. It takes a column count per rendered row, so a record folds into groups and stacks as a card. `"1,2"` across the three-column hook below keeps the article on the lead row and folds the category and published date onto a row beneath it.

Only the first group keeps one cell per column, so it alone stays aligned down the table; every later group lays its values out in equal columns that reduce in number to fit the viewport. The counts must be positive and add up to the number of columns your hook renders — a list that does not, such as one left behind when a column was added, is refused and the table falls back to wrapping the last column only.

Folded columns hide their headings, so their values appear without labels. That suits self-describing content such as badges, which is why the grouping is yours to choose rather than derived.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: list
  heading:
    title: Recent articles
    align: start
  input:
    section: blog
    reverse: false
    sort: date
  hide_empty: false
  hook: assets/table-filter-hook
  wrap: true
  wrap_cols: "1,2"
  sortable: true
  background:
    color: body-tertiary
    subtle: false
  justify: start
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Custom List

Customize the list by providing a `hook` partial.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: list
  heading:
    title: Recent articles
    align: start
  input:
    section: blog
    reverse: false
    sort: date
  hide_empty: false
  hook: assets/table-hook
  background:
    color: body-tertiary
    subtle: false
  justify: start
  sortable: true
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

Define the hook partial in your site's `layouts/_partials` folder. The following example renders a custom Markdown table consisting of the article's title and publication date.

{{< file file="./layouts/_partials/assets/table-hook.html" full=false lang="go-template" >}}

## Arguments

The content block supports the following arguments:

{{< args bookshop-list >}}
