---
title: "Save arbitrary inline data."
description: "Save arbitrary inline data."
lead: "Save arbitrary inline data."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I save "([^"]*)" as "([^"]*)"
This step allows to save arbitrary data from first argument into scenario cache under any key passed as second argument. Argument accepts template values.

Example:
```gherkin
Given I save "application/json" as "CONTENT_TYPE_JSON"
Given I save "Paweł" as "MY_NAME"
```