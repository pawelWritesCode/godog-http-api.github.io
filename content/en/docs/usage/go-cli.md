---
title: "CLI: go"
description: "How to run tests using go CLI."
lead: "How to run tests using go CLI."
date: 2023-03-27T13:59:39+01:00
lastmod: 2023-03-27T13:59:39+01:00
draft: false
images: []
weight: 110
toc: true
---

### Description
Go CLI is a tool shipped with GoLang installation. It contains various commands for working with your Go projects.

{{< alert icon="👉" context="warning" text="Go CLI is recommended method for running tests." />}}

{{< alert icon="👉" context="info" text="This section assumes you have already run 'make all' or 'make download-dependencies' command from root project directory." />}}

### Usages

To run all tests:

```shell
go test
```

To run all tests in random order marked with tag `wip` asynchronously using 2 CPUs:
```shell
go test -v --godog.random --godog.tags=wip --godog.concurrency=2
```


For more info see [godog's README TestMain section](https://github.com/cucumber/godog#testmain).