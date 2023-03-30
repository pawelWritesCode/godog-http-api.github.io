---
title: "Save data from last response body."
description: "Save data from last response body."
lead: "Stop data from last response body."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I save from the last response "(JSON|YAML|XML|HTML)" node "([^"]*)" as "([^"]*)"
This steps allows to obtain JSON/YAML/XML/HTML node from last HTTP(s) response and save it in scenario chace under given key.

First argument `the "(JSON|YAML|XML|HTML)" node` should be expected data format of response body.

Second argument `node "([^"]*)"` use APIContext's [PathFinders](/docs/utility-services/path-finders/) utility service. Default setup allows to use syntax from two different libraries (for JSON) and one for YAML and XML, which are described above. Argument accepts template values.

Last argument `as "([^"]*)"` allows you to pick name under which picked node value will be saved in scenario cache.

Example:
```gherkin
And I save from the last response "JSON" node "id" as "USER_ID"
And I save from the last response "YAML" node "$.id" as "USER_ID"
And I save from the last response "XML" node "//id" as "USER_ID"
And I save from the last response "JSON" node "@this.size" as "TOWN_SIZE"
And I save from the last response "JSON" node "@this.{{.SIZE_KEY}}" as "TOWN_SIZE"
```