---
_schema: default
title: Team
description: Use the team content block to show a group of team members.
type: docs
tags: block
---

## Overview

The `team` content block renders a group of team members.

<!-- markdownlint-disable MD037 -->
{{< example-bookshop lang="bookshop" >}}

```yml
- _bookshop_name: team
  heading:
    title: Team
    align: start
  input:
    section: team
    reverse: false
    sort: title
  cols: 3
  hide_empty: false
  header_style: none
  padding: 0
  background:
    color: body-tertiary
    subtle: false
  class: border-0 card-zoom card-body-margin
  justify: start
```

{{< /example-bookshop >}}
<!-- markdownlint-enable MD037 -->

## Arguments

The content block supports the following arguments:

{{< args bookshop-team >}}
