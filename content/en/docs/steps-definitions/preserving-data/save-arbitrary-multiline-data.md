---
title: "Save arbitrary multiline data."
description: "Save arbitrary multiline data."
lead: "Stop scenario execution."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I save as "([^"]*)":
This step allows to save arbitrary multiline data into scenario cache under any key passed as first argument. DocString accepts template values.

Example:
```gherkin
Given I save as "EMPTY_HEADER_AND_BODY":
"""
{
    "body": {},
    "headers": {}
}
"""
```