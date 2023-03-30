---
title: "Random word from provided charset and range"
description: "Generate random word from provided charset and range."
lead: "Generate random word from provided charset and range."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I generate a random word having from "(\d+)" to "(\d+)" of "(ASCII|UNICODE|polish|english|russian|japanese|emoji)" characters and save it as "([^"]*)"
This step generates random word and save it in scenario cache.

First two arguments:
`from "(\d+)" to "(\d+)" of`
allows to set length of the word. For example,
`from "2" to "4" of`
will generate word having between 2 and 4 characters. If you want to generate word of fixed length simply pass two times the same value:
`from "4" to "4" of`
This will generate word having 4 characters.

Next argument `of "(ASCII|UNICODE|polish|english|russian|japanese|emoji)" characters` allows to pick charset from which word will be generated. At the moment of writing this guide, there are only few available:
* ASCII - basic set of [characters](https://www.w3schools.com/charsets/ref_html_ascii.asp) like: a, b
* UNICODE - contains multi byte [characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) like: a, b, ą, ⚔, 🐞
* polish - characters that exist in [polish alphabet](https://pl.wikipedia.org/wiki/Alfabet_polski)
* english - characters that exist in english alphabet
* russian - characters that exist in russian alphabet
* japanese - characters that exist in japanese alphabet
* emoji - small subset of emojis

If you want to add ability to generate word from your custom charset, see `IGenerateARandomRunesOfLengthWithCharactersAndSaveItAs` [method](https://github.com/pawelWritesCode/godog-http-api/blob/main/defs/scenario.go#L26).
You have to add another `case` with your charset. You have to add it also to step definition. 
For example, lets say you want to add ability to generate word from german characters, then - in method, add
```go
case "german":
		generateWordFunc = s.APIContext.IGenerateARandomRunesInTheRangeToAndSaveItAs("aAäÄ...")
```
and update step definition: `of "(ASCII|UNICODE|polish|english|russian|japanese|emoji|german)" characters`.
Repository [charset](https://github.com/pawelWritesCode/charset/blob/master/charset.go) holds many pre-defined charsets, you can use any if you want and add it to your step definition.

Last argument `and save it as "([^"]*)"$` allows you to pick name under which generated word will be saved in scenario cache.

Examples:
```gherkin
Given I generate a random word having from "5" to "10" of "russian" characters and save it as "RANDOM_FIRST_NAME"
Given I generate a random word having from "5" to "15" of "UNICODE" characters and save it as "RANDOM_LAST_NAME"
```