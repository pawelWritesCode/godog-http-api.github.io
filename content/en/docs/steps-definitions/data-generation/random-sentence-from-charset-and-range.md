---
title: "Random sentence from provided charset and range"
description: "Generate random sentence from provided charset and range"
lead: "Generate random sentence"
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I generate a random sentence having from "(\d+)" to "(\d+)" of "(ASCII|UNICODE|polish|english|russian|japanese|emoji)" words and save it as "([^"]*)"
This step generates sentence and save it in scenario cache. To obtain once saved value, use syntax from [text/template](https://pkg.go.dev/text/template) package. This step is something like lorem-ipsum generator.

First two arguments `from "(\d+)" to "(\d+)" of` allows to pick length of sentence - number of words in it.

Argument `of "(ASCII|UNICODE|polish|english|russian|japanese|emoji)" words` determine charset from which each word will be generated. Last argument `save it as "([^"]*)"$` allows to pick name under which randomly generated sentence will be saved in scenario cache.

{{< alert icon="👉" context="info" text="In default setup, each word is defined to have between 3 and 10 characters. You can change it, by passing another values to step's definition method in 'main_test.go'" />}}

Examples:
```gherkin
Given I generate a random sentence having from "2" to "2" of "english" words and save it as "NAME_AND_SURNAME"
Given I generate a random sentence having from "1" to "4" of "polish" words and save it as "RANDOM_DESCRIPTION"
```