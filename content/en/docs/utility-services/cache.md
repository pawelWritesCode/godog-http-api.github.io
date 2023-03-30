---
title: "Cache"
description: "Service responsible for storing data across scenario."
lead: "Service responsible for storing data across scenario."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
weight: 120
toc: true
---

### Cache of type cache.Cache
This service preserve data between steps in one scenario.

```go
// Cache is entity that has ability to store/retrieve arbitrary values.
type Cache interface {
	// Save preserve provided value under given key.
	Save(key string, value interface{})

	// GetSaved retrieve value from given key.
	GetSaved(key string) (interface{}, error)

	// Reset turns cache into init state - clears all entries.
	Reset()

	// All returns all cache entries.
	All() map[string]interface{}
}
```
To replace it with your own implementation use following setter.
```go
func (apiCtx *APIContext) SetCache(c cache.Cache)
```

Some examples of custom cache may be:
- one which stores data in database (Redis, mongoDB, any SQL-like)
- one which logs every saved value for debugging purposes