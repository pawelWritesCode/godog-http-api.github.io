---
title: "Quick Start"
description: "How to get copy of project and run tests."
lead: "How to get copy of project and run tests."
date: 2023-03-27T13:59:39+01:00
lastmod: 2023-03-27T13:59:39+01:00
draft: false
images: []
weight: 110
toc: true
---

## Prerequisites
* Git
* GoLang 1.19+
* Docker with built-in compose command (optional)
* Makefile support (optional)

## Setup 
**Note**: Some users may require to run commands with `sudo`
```shell
git clone https://github.com/pawelWritesCode/godog-http-api.git && cd godog-http-api
```
Next run `all` command:
```shell
make all
```
Afterwards you can run tests using 3 distinct ways

### Local OS
```shell
make tests-using-host
```

### Docker
```shell
make tests-using-docker
```

### Docker compose
```shell
make tests-using-compose
```
For more usage examples examine [Usage](/docs/usage/godog-cli/) section.

---

From now on, you can write your own tests (files with `*.feature` extension) using provided pre-defined steps.

{{< alert icon="👉" context="info" text="Note that at this moment project contains unnecessary files and directories which exists mainly for training purposes." />}}