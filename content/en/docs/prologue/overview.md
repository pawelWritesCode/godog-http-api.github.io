---
title: "Overview"
description: "Directory structure explained."
lead: "Directory structure explained."
date: 2023-03-27T13:59:39+01:00
lastmod: 2023-03-27T13:59:39+01:00
draft: false
images: []
weight: 120
toc: true
---

## Unmodified cloned project
```text
.
├── assets
│   ├── gifs
│   ├── svg
│   └── test_server
├── compose.yaml
├── defs
│   └── scenario.go
├── Dockerfile
├── features
│   ├── 7timer
│   ├── helium
│   ├── httpbin
│   └── test_server
├── go.mod
├── go.sum
├── LICENSE
├── main_test.go
├── Makefile
└── README.MD
```

{{< alert icon="👉" context="info" text="Above structure contains directories and files that you won't need in long run. However, It's convenient to play around before stripping them." />}}

## Make clean
Predefined command `make clean` strips project from unnecessary files and directories (also hidden ones).
You can run it when you are done with experimenting, and you understand basic concepts of project.
```text
├── compose.yaml
├── defs
│   └── scenario.go
├── Dockerfile
├── go.mod
├── go.sum
├── LICENSE
├── main_test.go
├── Makefile
└── README.MD
```


## assets/
{{< alert icon="👉" context="danger" text="Subject to remove by 'make clean'" />}}

This directory contains `gifs/` and `svgs/` subdirectories with images used by `README.MD`.

`test_server/` directory contains example web server binary that allows to make CRUD operations for User entity to play around and
its documentation in OpenAPI format. See [pawelWritesCode/user-crud](https://github.com/pawelWritesCode/user-crud) repository, Docker Hub [image](https://hub.docker.com/r/pawelwritescode/user-crud)
and predefined [tests for it](https://github.com/pawelWritesCode/godog-http-api/tree/main/features/test_server).

## defs/
This directory contains definitions used behind defined steps (golang code). Add your custom definitions code here.

## features/
{{< alert icon="👉" context="danger" text="Subject to remove by 'make clean'" />}}

This directory contains tests. Those are files with `*.feature` extension grouped in logical subdirectories.

## compose.yaml
This file contains definition of multi container application. It exists only for demonstration purposes to show how
tests can be defined in it.

## Dockerfile
This file contains containerization definition for project.

## go.mod & go.sum
Those files lists used GoLang packages. 

## main_test.go
Contains definition of steps and framework setup.

## Makefile
Source of useful commands to work with project.

## LICENCE
Pure informational file with license description.