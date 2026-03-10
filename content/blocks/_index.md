---
title: Blocks
description: Assemble your pages using configurable content blocks.
date: 2026-02-23
weight: 10
type: docs
tags: block
content_blocks:
  - _bookshop_name: hero
    heading:
      title: Blocks
      content: >-
        Hinode provides more than 15 ready-to-use content blocks. These blocks
        allow you to quickly assemble your content pages using visual elements.
        Powered by [Bookshop](https://github.com/CloudCannon/bookshop), these
        blocks are ready for visual editing using [CloudCannon](https://cloudcannon.com/).
        Click on an item for more details.
      align: start
    breadcrumb: true

  - _bookshop_name: articles
    hide_empty: false
    input:
      reverse: false
      sort: title
    more:
      title: More Blocks
    cols: 5
    padding: 0
    paginate: true
    pagination: 25
    cover: false
    header_style: none
    body_style: minimal
    class: card-minimal
---
