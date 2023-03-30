---
title: "Time object"
description: "Generate time object."
lead: "Generate time object."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I generate current time and travel "(backward|forward)" "([^"]*)" in time and save it as "([^"]*)"
This step allows to generate time object, moved backward/forward in time and save it to scenario cache.

First argument `and travel "(backward|forward)"` tells whether user want to move forward or backward in time. If you want to simply get current time object just pass any of both.

Second argument `"([^"]*)" in time` should be string acceptable by [time.ParseDuration](https://pkg.go.dev/time#ParseDuration). It tells how much time should we travel in time.

Last argument `and save it as "([^"]*)"$` allows you to pick name under which generated time object will be saved in scenario cache.

Futher use of this saved time object should be done through templates. You most probably want to format it according to your needs. Syntax is:
`{{.CACHE-KEY-OF-TIME-OBJECT.Format "time-format"}}`. See avaialble [time-formats](https://pkg.go.dev/time#pkg-constants).
Examples:
```gherkin
Given I generate current time and travel "forward" "0s" in time and save it as "CURRENT_TIME"
Given I generate current time and travel "forward" "31d" in time and save it as "NEXT_MONTH"
Given I generate current time and travel "backward" "5m" in time and save it as "5_MINUTES_AGO"
```

Examples of usage in Docstring (assuming, that time object is saved under `TIME` key in scenario cache):
```
`{{.TIME}}`
`{{.TIME.Format "2006-01-02T15:04:05Z07:00"}}`
`{{.TIME.Format "2006-01-02"}}`
```