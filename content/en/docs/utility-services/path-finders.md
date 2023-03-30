---
title: "PathFinders"
description: "Services responsible for querying nodes of data from different formats."
lead: "Services responsible for querying nodes of data from different formats."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
weight: 120
toc: true
---

### PathFinders of struct type PathFinders
Those services allows to query response body tree to obtain nodes.

```go
// PathFinders is container for different data types pathfinders.
type PathFinders struct {
	// JSON is entity that has ability to obtain data from bytes in JSON format.
	JSON pathfinder.PathFinder

	// YAML is entity that has ability to obtain data from bytes in YAML format.
	YAML pathfinder.PathFinder

	// XML is entity that has ability to obtain data from bytes in XML format.
	XML pathfinder.PathFinder

	// HTML is entity that has ability to obtain data from bytes in HTML format.
	HTML pathfinder.PathFinder
}
```
To replace them with your own implementation use following setters:
```go
// SetJSONPathFinder sets new JSON pathfinder for APIContext.
func (apiCtx *APIContext) SetJSONPathFinder(r pathfinder.PathFinder)

// SetYAMLPathFinder sets new YAML pathfinder for APIContext.
func (apiCtx *APIContext) SetYAMLPathFinder(r pathfinder.PathFinder)

// SetXMLPathFinder sets new XML pathfinder for APIContext.
func (apiCtx *APIContext) SetXMLPathFinder(r pathfinder.PathFinder)

// SetHTMLPathFinder sets new HTML pathfinder for APIContext.
func (apiCtx *APIContext) SetHTMLPathFinder(r pathfinder.PathFinder)
```

`JSON` allows to query JSON nodes,
`YAML` allows to query YAML nodes,
`XML` allows to query XML nodes,
`HTML` allows to query HTML nodes.


Some examples of custom path finders may be:
- one that uses different syntax
- one that allows to work with many different json-path engines at once. (self aware)