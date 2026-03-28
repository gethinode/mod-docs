---
_schema: default
title: Separator
description: >-
  Adds a section separator. The separator spans the entire page from edge to
  edge on smaller devices. On larger screens, the separator is bound by the
  maximum container width that contains the section.
type: docs
tags: block
---

## Overview

The `separator` content block renders a section separator. The separator spans the entire page from edge to edge on smaller devices. On larger screens, the separator is bound by the maximum container width that contains the section.

### Line separator

The default separator renders a horizontal line.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: separator
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

### Clear separator

Set the argument `clear: true` to render a clear separator.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: separator
  clear: true
  section_class: bg-info
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

## Arguments

The content block supports the following arguments:

{{< args bookshop-separator >}}
