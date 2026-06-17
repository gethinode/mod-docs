---
author: Mark Dumay
title: Table
date: 2026-06-17
description: Use the table shortcode to make your Markdown table responsive.
type: docs
tags: component
modules: ["simple-datatables"]
weight: 330
---

## Overview

{{< release version="v0.8.0" >}}

> [!IMPORTANT]
> Bootstrap styling attributes require an explicit class argument as of release {{< release version="v0.22.0" short="true" link-type="link" >}}. For example, use the following argument to accentuate a table with table-striped: `class="table-striped"`.

### Responsive table

Use the table shortcode to make your markdown table responsive. Responsive tables scroll horizontally to improve the layout on smaller screens. The following example illustrates how this works.

<!-- markdownlint-disable MD037 MD058 -->
{{< example lang="markdown" >}}
{{</* table */>}}
| #  | Heading | Heading | Heading | Heading | Heading | Heading | Heading | Heading | Heading |
|----|---------|---------|---------|---------|---------|---------|---------|---------|---------|
| 1. | cell    | cell    | cell    | cell    | cell    | cell    | cell    | cell    | cell    |
| 2. | cell    | cell    | cell    | cell    | cell    | cell    | cell    | cell    | cell    |
| 3. | cell    | cell    | cell    | cell    | cell    | cell    | cell    | cell    | cell    |
{{</* /table */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 MD058 -->

### Table wrapping

Set `wrap=true` to wrap the last column around on smaller viewports.

<!-- markdownlint-disable MD037 MD058 -->
{{< example lang="markdown" >}}
{{</* table wrap=true */>}}
| #  | Heading | Heading | Wrapped                                                               |
|----|---------|---------|-----------------------------------------------------------------------|
| 1. | cell    | cell    | Lorem ipsum dolor sit amet, consectetur adipiscing elit.              |
| 2. | cell    | cell    | Nunc pretium, diam non euismod tincidunt, odio libero feugiat ligula. |
| 3. | cell    | cell    | Cras eu odio sit amet lectus efficitur accumsan.                      |
{{</* /table */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 MD058 -->

### Data table

{{< release version="v0.24.13" >}}

Include the module `simple-datatables` to add advanced controls to your table. Features include in-line pagination, search, and sorting. Include the module in the frontmatter of your content page:

```yml
---
modules: ["simple-datatables"]
---
```

As an example, the following shortcode displays a responsive table that is `searchable`, `sortable`, and enables paging (`paginate`) with a page size (`pagination`) of 5.

<!-- markdownlint-disable MD037 MD058 -->
{{< example lang="markdown" >}}
{{</* table searchable="true" sortable="true" paginate="true" pagination=5 */>}}
| #   | Heading |
|-----|---------|
| 1.  | Item 1  |
| 2.  | Item 2  |
| 3.  | Item 3  |
| 4.  | Item 4  |
| 5.  | Item 5  |
| 6.  | Item 6  |
| 7.  | Item 7  |
| 8.  | Item 8  |
| 9.  | Item 9  |
| 10. | Item 10 |
| 11. | Item 11 |
| 12. | Item 12 |
| 13. | Item 13 |
| 14. | Item 14 |
| 15. | Item 15 |
{{</* /table */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 MD058 -->

## Configuration

With [Simple Datatables](https://github.com/gethinode/mod-simple-datatables) enabled, add the attribute `data-table` to the class of any Markdown table. The following arguments are supported:

<!-- markdownlint-disable MD060 -->
| Argument                | Default | Description |
|-------------------------|---------|-------------|
| `data-table-sortable`   | `true`  | Toggle the ability to sort the columns. |
| `data-table-paging`     | `true`  | Whether paging is enabled for the table. |
| `data-table-paging-option-perPage`     | `10`  | Paging option: Sets the maximum number of rows to display on each page. Type: int  |
| `data-table-paging-option-perPageSelect`     | `[5, 10, 20, 50, ["{{ T "tablePerPageSelectAll" }}", -1]]`  | Paging option: Sets the per page options in the dropdown. i18n translation id for all: `tablePerPageSelectAll`. |
| `data-table-searchable` | `true`  | Toggle the ability to search the dataset. |
<!-- markdownlint-enable MD060 -->

## Styling

The file `assets/scss/components/_table.scss` defines the Hinode-specific styling of the `table` shortcode.

{{< file file="assets/scss/components/_table.scss" show="false" >}}

## Arguments

The shortcode supports the following arguments:

{{< args structure="table" group="shortcode" >}}
