---
title: "Pause for given period of time."
description: "Pause for given period of time."
lead: "Pause for given period of time."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I wait "([^"]*)"
This step allows to stop scenario execution for some time. Sometimes, if you know, that API does not process your request immediately, and you want to wait for short amount of time before sending another HTTP(s) request you can do it with this method.

The only one argument, should be string acceptable by [time.ParseDuration](https://pkg.go.dev/time#ParseDuration).

Example:

```gherkin
Given I wait "3s"
Given I wait "20ms"
```