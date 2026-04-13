---
author: Mark Dumay
title: Timeline
date: 2024-04-18
description: Use the timeline shortcode to show items ordered on a vertical timeline.
type: docs
tags: component
weight: 340
---

## Overview

{{< release version="v0.15.3" >}}

Use the timeline shortcode to show items ordered on a vertical timeline.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* timeline data="timeline-sample" background="body-tertiary" */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

### Start layout

{{< release version="v2.7.0" >}}

Use `layout="start"` to render a compact, start-aligned timeline without icons. Each item shows a linked date and a short excerpt. This variant is well suited for sidebar widgets and changelogs. Use `limit` to cap the number of items rendered.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* timeline data="timeline-sample" layout="start" limit="3" */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

You can also source timeline items directly from a Hugo content section by passing `section` to the partial (see the [partial arguments](#arguments)). Items are taken from the section's regular pages, sorted by date descending. The `title`, `date`, `description`, and `permalink` of each page are mapped to the timeline fields automatically.

## Data format

Define a file in the `data` folder that contains the timeline data. The format supports the following attributes:

| Attribute | Required | Description                                                                                  |
|-----------|----------|----------------------------------------------------------------------------------------------|
| title     | Yes      | Required title of the timeline element.                                                      |
| icon      | Yes      | Required class and name of a Font Awesome icon to include. The icons use shorthand notation. |
| color     | No       | Optional theme color of the timeline element, defaults to `primary`.                         |
| date      | No       | Optional date of the timeline element, placed below the title.                               |
| badge     | No       | Optional label of a pill badge placed next to the title.                                     |
| url       | No       | Optional url of the timeline element, added as link to the title when set[^1].               |
| content   | No       | Optional content of the timeline element, supports markdown.                                 |

[^1]: The url is joined with the `release` attribute of the documentation configuration, unless the url is absolute (e.g. starts with `http`).

The following snippet defines a single timeline element in `yml` format.

```yml
- title: Product launch
  icon: rocket
  color: primary
  date: 2023-07-03
  badge: v0.15.3
  url: https://github.com/gethinode/hinode/releases/tag/v0.15.3
  content:
    Lorem ipsum dolor sit amet, consectetur adipisicing elit.
```

## Styling

The file `assets/scss/components/_timeline.scss` defines the Hinode-specific styling of the `timeline` shortcode.

{{< file file="assets/scss/components/_timeline.scss" show="false" >}}

## Arguments

The shortcode supports the following arguments:

{{< args structure="timeline" group="shortcode" >}}
