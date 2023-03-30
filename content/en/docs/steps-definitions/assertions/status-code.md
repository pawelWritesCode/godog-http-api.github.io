---
title: "HTTP response status code"
description: "HTTP response status code."
lead: "HTTP response status code."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### the response status code should (not )?be (\d+)
This step checks against last HTTP(s) response [status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).

Examples:
```gherkin
Then the response status code should be 201
But the response status code should not be 200
```
