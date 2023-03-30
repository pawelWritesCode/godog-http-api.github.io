---
title: "SchemaValidators"
description: "Services responsible for validating response body against JSON schema."
lead: "Services responsible for validating response body against JSON schema."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
weight: 120
toc: true
---

### SchemaValidators of struct type SchemaValidators
Schema validators are responsible for validating payload against json-schema

```go
// SchemaValidators is container for JSON schema validators.
type SchemaValidators struct {
	// StringValidator represents entity that has ability to validate document against string of containing schema.
	StringValidator validator.SchemaValidator

	// ReferenceValidator represents entity that has ability to validate document against string with reference
	// to schema, which may be URL or relative/full OS path for example.
	ReferenceValidator validator.SchemaValidator
}
```

To replace them with your own implementation use following setters:
```go
// SetSchemaStringValidator sets new schema StringValidator for APIContext.
func (apiCtx *APIContext) SetSchemaStringValidator(j validator.SchemaValidator) 

// SetSchemaReferenceValidator sets new schema ReferenceValidator for APIContext.
func (apiCtx *APIContext) SetSchemaReferenceValidator(j validator.SchemaValidator) 
```

Each validator has type
```go
// SchemaValidator describes entity that can validate document against some kind of schema.
type SchemaValidator interface {
	// Validate validates document against some kind of schema located in schemaPath.
	Validate(document, schemaPath string) error
}
```

`StringValidator` validates document against provided schema string, `ReferenceValidator` validates document against provided schema as reference (path/url)

Some examples of custom schema validators  may be:
- one which validates JSON schema of different specification than default one
- one which has ability to accept different type of reference to JSON-schema
- one which has ability to validate schema in YAML format