---
title: "Random number from the range"
description: "Generate random int or float from provided range."
lead: "Generate random int or float from provided range."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I generate a random "(int|float)" in the range from "([^"]*)" to "([^"]*)" and save it as "([^"]*)"
This step generates random number and save it in scenario cache. To obtain once saved value, use syntax from [text/template](https://pkg.go.dev/text/template) package.

First argument `random "(int|float)" in` allows to pick type of number.

Second argument `from "([^"]*)" to "([^"]*)" and` allows to pick interval from which number will be generated.

Last argument `and save it as "([^"]*)"$` allows you to pick name under which generated number will be saved in scenario cache.

**Tip**: Later, if you want to use generated float, you can format it using functions from [text/template](https://pkg.go.dev/text/template#hdr-Functions) package, for example
```gherkin
    Given I generate a random "float" in the range from "34.5" to "39.4" and save it as "RANDOM_TEMPERATURE_C"
    When I send "POST" request to "{{.MY_APP_URL}}/data" with body and headers:
    """
    {
        "body": {
            "temperature": {{printf `%.2f` .RANDOM_TEMPERATURE_C}}
        },
        "headers": {
            "Content-Type": "{{.CONTENT_TYPE_JSON}}"
        }
    }
    """
```

Examples:
```gherkin
Given I generate a random "int" in the range from "18" to "48" and save it as "RANDOM_AGE"
Given I generate a random "float" in the range from "35.5" to "38.3" and save it as "RANDOM_TEMPERATURE_C"
```