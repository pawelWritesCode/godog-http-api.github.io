---
title: "Activate/deactivate debug mode."
description: "Activate/deactivate debug mode."
lead: "Activate/deactivate debug mode."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I start debug mode
This step temporarily turns on debugging mode inside scenario. You can think of it as setting environment variable `GODOG_DEBUG` to `true` for a while.

Example:

```gherkin
Given I start debug mode
```

#### I stop debug mode
This step turns off debugging mode in given scenario.

Example:

```gherkin
Given I stop debug mode
```