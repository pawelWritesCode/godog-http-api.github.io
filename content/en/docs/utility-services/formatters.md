---
title: "Formatters"
description: "Services responsible for serialization/deserialization data of given formats."
lead: "Services responsible for serialization/deserialization data of given formats."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
weight: 120
toc: true
---

### Formatters of struct type Formatters
Those service are responsible for serialization and deserialization data.

```go
// Formatters is container for entities that know how to serialize and deserialize data.
type Formatters struct {
	// JSON is entity that has ability to serialize and deserialize JSON bytes.
	JSON formatter.Formatter

	// YAML is entity that has ability to serialize and deserialize YAML bytes.
	YAML formatter.Formatter

	// XML is entity that has ability to serialize and deserialize XML bytes.
	XML formatter.Formatter
}
```

Each formatter has to implement
```go
// Formatter describes ability to serialize and deserialize data
type Formatter interface {
	// Deserialize deserializes data on v
	Deserialize(data []byte, v interface{}) error

	// Serialize serializes v
	Serialize(v interface{}) ([]byte, error)
}
```

To replace them with your own implementation use following setters:
```go
// SetJSONFormatter sets new JSON formatter for APIContext.
func (apiCtx *APIContext) SetJSONFormatter(jf formatter.Formatter) 

// SetYAMLFormatter sets new YAML formatter for APIContext.
func (apiCtx *APIContext) SetYAMLFormatter(yd formatter.Formatter)

// SetXMLFormatter sets new XML formatter for APIContext.
func (apiCtx *APIContext) SetXMLFormatter(xf formatter.Formatter)
```

`JSON` has ability to serialize/deserialize data in JSON format, `YAML` has ability to serialize/deserialize data in YAML format, `XML` has ability to serialize/deserialize data in XML format


Some examples of custom formatters may be:
- one that format with indentation