---
title: "TypeMappers"
description: "Services responsible for mapping internal data structures onto different formats data types."
lead: "Services responsible for mapping internal data structures onto different formats data types."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
weight: 120
toc: true
---

### TypeMappers of struct type TypeMappers
Those services are responsible for mapping internal data structures onto different formats data types.

```go
// TypeMappers is container for different data format mappers
type TypeMappers struct {
	// JSON is entity that has ability to map underlying data type into JSON data type
	JSON types.Mapper

	// YAML is entity that has ability to map underlying data type into YAML data type
	YAML types.Mapper

	// GO is entity that has ability to map underlying data type into GO-like data type
	GO types.Mapper
}
```

Each mapper has to implement following interface:
```go
// Mapper is entity that has ability to map data's type into corresponding DataType of given format.
type Mapper interface {
	// Map maps data type.
	Map(data any) DataType
}
```

To replace them with your own implementation use following setters:
```go
// SetJSONTypeMapper sets new type mapper for JSON.
func (apiCtx *APIContext) SetJSONTypeMapper(c types.Mapper) {
	apiCtx.TypeMappers.JSON = c
}

// SetYAMLTypeMapper sets new type mapper for YAML.
func (apiCtx *APIContext) SetYAMLTypeMapper(c types.Mapper) {
	apiCtx.TypeMappers.YAML = c
}

// SetGoTypeMapper sets new type mapper for Go.
func (apiCtx *APIContext) SetGoTypeMapper(c types.Mapper) {
	apiCtx.TypeMappers.GO = c
}
```