---
author: Mark Dumay
title: Card Group
date: 2023-12-29
description: Use the card-group shortcode to display a group of cards.
type: docs
tags: component
weight: 100
---

## Overview

{{< release version="v0.18.6" >}}

Use the `card-group` shortcode to display a group of cards. Add inner `<card>` elements for each [card](card). As an example, the following shortcode displays a group of three cards. See the [card component](card) for additional styling options.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* card-group padding="3" gutter="3" */>}}
    {{</* card title="Bootstrap framework" icon="fab bootstrap" */>}}
        Build fast, responsive sites with Bootstrap 5. Easily customize your site with the
        source Sass files.
    {{</* /card */>}}
    {{</* card title="Full text search" icon="fas magnifying-glass" */>}}
        Search your site with FlexSearch, a full-text search library with zero dependencies.
    {{</* /card */>}}
    {{</* card title="Development tools" icon="fas code" */>}}
        Use Node Package Manager to automate the build process and to keep track of
        dependencies.
    {{</* /card */>}}
{{</* /card-group */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

## Aligned rows

Set `align-rows` to `true` to line up the parts of the cards in each visual row. Every card is split into six bands: the image or icon, the title, the subtitle, the highlight, the body, and the footer. Each band is as tall as its tallest entry in the row, so a long subtitle in one card pushes the highlights of all its neighbours down by the same amount. A card that lacks a part keeps an empty band, so its other parts stay on their neighbours' lines.

Alignment applies to stacked groups only, which is the default `orientation`. It has no effect for any other orientation, or when `scroll` or `bento` is set. The `spacer` and `separator` arguments are not rendered in an aligned group. Alignment uses CSS subgrid; browsers without subgrid support show the regular layout.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* card-group cols="3" gutter="3" align-rows=true */>}}
    {{</* card title="Starter" icon="fas seedling"
        subtitle="For individuals."
        highlight="**€0** per month" */>}}

- One project
- Community support

    {{</* /card */>}}
    {{</* card title="Team" icon="fas users"
        subtitle="For growing teams that share their projects."
        highlight="**€9** per user per month" */>}}

- Unlimited projects
- Shared workspaces
- Priority support

    {{</* /card */>}}
    {{</* card title="Enterprise" icon="fas building"
        subtitle="For organizations with *custom* needs, such as single sign-on and audits."
        highlight="**Custom pricing**" */>}}

- Dedicated account manager
- Custom contracts

    {{</* /card */>}}
{{</* /card-group */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

Alignment also works with colored and bordered cards. The card's background and border wrap all six bands.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* card-group cols="3" gutter="3" align-rows=true */>}}
    {{</* card color="primary" title="Starter"
        subtitle="For individuals."
        highlight="**€0** per month" */>}}

- One project
- Community support

    {{</* /card */>}}
    {{</* card color="primary" title="Team"
        subtitle="For growing teams that share their projects."
        highlight="**€9** per user per month" */>}}

- Unlimited projects
- Shared workspaces
- Priority support

    {{</* /card */>}}
    {{</* card color="primary" title="Enterprise"
        subtitle="For organizations with *custom* needs, such as single sign-on and audits."
        highlight="**Custom pricing**" */>}}

- Dedicated account manager
- Custom contracts

    {{</* /card */>}}
{{</* /card-group */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

## Arguments

The shortcode supports the following arguments:

{{< args structure="card-group" group="shortcode" >}}

In addition, the following arguments are passed to the individual cards.

{{< args structure="card" group="shortcode" parent="true" >}}
