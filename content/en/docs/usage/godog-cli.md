---
title: "CLI: godog"
description: "How to run tests using godog CLI."
lead: "How to run tests using godog CLI."
date: 2023-03-27T13:59:39+01:00
lastmod: 2023-03-27T13:59:39+01:00
draft: false
images: []
weight: 100
toc: true
---

### Description
[Godog](https://github.com/cucumber/godog) CLI is program that knows how to run tests written with gherkin/cucmber syntax. Under the hood
it uses GoLang.

{{< alert icon="👉" context="warning" text="Godog CLI is depreciated method for running tests, see https://github.com/cucumber/godog/discussions/478" />}}

{{< alert icon="👉" context="info" text="This section assumes you have already run 'make all' or 'make download-dependencies' command from root project directory and have globally visible godog binary in your shell." />}}

### Usages
Project's Makefile contains command that demonstrates usage of godog CLI to run tests:
```shell
make tests-using-host
```

To run tests directly by `godog` CLI try:
```shell
godog run features/
```
This mode run all tests from `features/` directory synchronously.

To run all tests from `features/` asynchronously add `--concurrency` flag with desired value.
General rule of thumb is that value should not be greater than number of CPUs on host machine.
It is also beneficial to add `--format=progress` flag to change display of format to more convenient for asynchronous mode. 
```shell
godog run features/ --format=progress --concurrency=2
```

Tests also can be run selectively simply by passing path to them
```shell
godog run features/path/to/your/test.feature
```

If you mark few scenarios or features with any tag (for example: `smoke`), you can run them by
```shell
godog run --tags=smoke
```

For more info see [godog's README CLI section](https://github.com/cucumber/godog#cli-mode).