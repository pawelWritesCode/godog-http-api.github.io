---
title: "TemplateEngine"
description: "Service responsible for templates."
lead: "Service responsible for templates."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
weight: 120
toc: true
---

### TemplateEngine of type template.Engine
This service is responsible for string templating. It allows to inject previously cached/generated data into step's arguments.
```go
// Engine is entity that has ability to work with templates.
type Engine interface {
	// Replace replaces template values using provided storage.
	Replace(templateValue string, storage map[string]interface{}) (string, error)
}
```

To replace it with your own implementation use following setter:
```go
func (apiCtx *APIContext) SetTemplateEngine(t template.Engine)
```

Some examples of custom template engine may be:
- one which uses different syntax for injecting variables
- one which logs somewhere injected values