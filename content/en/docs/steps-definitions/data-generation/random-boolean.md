---
title: "Random boolean"
description: "Generate random boolean value"
lead: "Generate random boolean value"
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I generate a random bool value and save it as "([^"]*)"
This step allows to generate random boolean value and save it in scenario cache.

The only one argument `it as "([^"]*)"` allows you to pick name under which generated boolean value will be saved in scenario cache.

Example:
```gherkin
Given I generate a random bool value and save it as "IS_WATER_BOILING"
```