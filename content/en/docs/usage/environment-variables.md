---
title: "Environment variables"
description: "Working with environment variables."
lead: "Working with environment variables."
date: 2023-03-27T13:59:39+01:00
lastmod: 2023-03-27T13:59:39+01:00
draft: false
images: []
weight: -2
toc: true
---

## Overview
{{< alert icon="👉" context="info" text="This section assumes you have already run 'make all' or 'make env' command from root project directory." />}}

Project has built-in support for environment variables. Freshly cloned project uses 3 of them.
```
GODOG_DEBUG=false
GODOG_MY_APP_URL=http://localhost:1234
GODOG_JSON_SCHEMA_DIR=./assets/test_server/doc/schema
```
which can be found in `.env` file.

## Further usage
You can add/modify/remove any environment variables.
In code, current environment variables are defined at top of `main_test.go` file
```go
const (
    //envDebug describes environment variable responsible for debug mode - (true/false).
    envDebug = "GODOG_DEBUG"
    
    // envMyAppURL describes URL to "My app" - should be valid URL.
    envMyAppURL = "GODOG_MY_APP_URL"
    
    // envJsonSchemaDir path to JSON schemas dir - relative path from this file's directory.
    envJsonSchemaDir = "GODOG_JSON_SCHEMA_DIR"
)
```
and further used for example as pre-defined variables in every scenario like [this](https://github.com/pawelWritesCode/godog-http-api/blob/main/main_test.go#L65) (`os.Getenv` obtains environment variable from `.env` file or shell):
```go
ctx.Before(func(ctx context.Context, sc *godog.Scenario) (context.Context, error) {
    scenario.APIContext.ResetState(isDebug)

    // Here you can define more scenario-scoped values using scenario.APIContext.Cache.Save() method
    scenario.APIContext.Cache.Save("MY_APP_URL", os.Getenv(envMyAppURL))
    scenario.APIContext.Cache.Save("CWD", wd) // current working directory - full OS path to this file

return ctx, nil
})
```
Above example shows usage of [Cache](/docs/utility-services/cache/) utility service, which is responsible for 
storing values across scenario.