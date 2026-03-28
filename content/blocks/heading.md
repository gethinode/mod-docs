---
_schema: default
title: Heading
description: Use the heading content block to show a heading with optional regular content.
type: docs
tags: block
---

## Overview

The `heading` content block renders a section heading with optional regular content.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: heading
  heading:
    preheading: Preheading
    title: Section heading
    content: Regular content that is placed below the title.
  width: 8
  justify: center
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

## Arguments

The content block supports the following arguments:

{{< args bookshop-heading >}}
