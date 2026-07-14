---
author: Mark Dumay
title: Example
date: 2023-12-29
description: The example shortcode displays a code example and renders a preview of the same input.
type: docs
tags: component
weight: 160
---

## Overview

{{< release version="v0.8.0" >}}

The `example` shortcode displays a code example and renders a preview of the same input. The shortcode accepts the languages supported by Hugo's [highlight function](https://gohugo.io/content-management/syntax-highlighting/#list-of-chroma-highlighting-languages).

### Hugo code example

Set the `lang` argument to `hugo` to render a Hugo code example. Be sure to escape the input with `/*` and `*/` delimiters to avoid rendering issues.

#### Preview

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo">}}
{{</* command */>}}
export MY_VAR=123
{{</* /command */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

#### Input

```go-html-template
{{</* example lang="hugo" */>}}
    {{</*/* command */*/>}}
    export MY_VAR=123
    {{</*/* /command */*/>}}
{{</* /example */>}}
```

### Hidden markup

Set `show-markup` to `false` to hide the code input and to display the preview only.

#### Preview

{{< example lang="hugo" show-markup=false >}}
This is a lead paragraph. It stands out from regular paragraphs.
{.lead}
{{< /example >}}

#### Input

```go-html-template
{{</* example show-markup=false */>}}
This is a lead paragraph. It stands out from regular paragraphs.
{.lead}
{{</* /example */>}}
```

### Hidden preview

Set `show-preview` to `false` to hide the output and to display the code input only.

#### Preview

{{< example lang="hugo" show-preview=false >}}
This is a lead paragraph. It stands out from regular paragraphs.
{.lead}
{{< /example >}}

#### Input

```go-html-template
{{</* example show-preview=false */>}}
This is a lead paragraph. It stands out from regular paragraphs.
{.lead}
{{</* /example */>}}
```

### Resizable preview

{{< release version="v3.2.0" >}}

Set `resize` to `true` to add a grip to the lower-right corner of the preview. Drag it to narrow the preview and observe how the component reflows.

> [!IMPORTANT]
> The grip demonstrates *fluid* reflow — content wrapping, text truncation, tables gaining a scrollbar, images scaling. It does **not** trigger responsive breakpoints. Bootstrap 5's responsive classes (`navbar-expand-*`, `col-md-*`, and similar) are viewport media queries, so they respond to the size of the browser window, not the size of the preview. To preview breakpoint behavior, resize the browser window instead.

#### Preview

{{< example lang="hugo" resize="true" >}}
This is a lead paragraph. It stands out from regular paragraphs.
{.lead}
{{< /example >}}

#### Input

```go-html-template
{{</* example resize="true" */>}}
This is a lead paragraph. It stands out from regular paragraphs.
{.lead}
{{</* /example */>}}
```

## Arguments

The shortcode supports the following arguments:

{{< args structure="example" group="shortcode" >}}
