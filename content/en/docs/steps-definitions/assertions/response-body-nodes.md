---
title: "HTTP response body nodes"
description: "HTTP response body nodes."
lead: "HTTP response body nodes."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

### Overview 
Following steps allows to query nodes. Querying nodes is handled by [PathFinders](/docs/utility-services/path-finders/) utility service.
Default setup allows to use following JSON/XML/YAML/HTML path engines:

JSON:
* [tidwall/gjson](https://github.com/tidwall/gjson) 
* [oliveagle/jsonpath](https://github.com/oliveagle/jsonpath) 
* [antchfx/jsonquery](https://github.com/antchfx/jsonquery)

YAML:
* [goccy/go-yaml](https://github.com/goccy/go-yaml)

XML:
* [antchfx/xmlquery](https://github.com/antchfx/xmlquery)

HTML:
* [antchfx/htmlquery](https://github.com/antchfx/htmlquery)

#### the "(JSON|YAML|XML|HTML)" response should (not )?have node "([^"]*)"
This step checks whether last HTTP(s) response body does have/doesn't have given JSON/YAML/XML/HTML node.

Examples:
```gherkin
And the "JSON" response should have node "data.0.firstName"
But the "JSON" response should not have node "$.data[0].firstName"
And the "YAML" response should have node "$.data[0].firstName"
And the "XML" response should have node "//data[0]//firstName"
And the "HTML" response should have node "//head//title"
```

Last argument accepts template values.

#### the "(JSON|YAML|XML|HTML)" response should have nodes "([^"]*)"
This step checks whether last HTTP(s) response body has given JSON/YAML/XML/HTML nodes.

Argument should contain list of expressions-strings pointing at JSON/YAML/XML/HTML nodes, acceptable by APIContext's [PathFinders](/docs/utility-services/path-finders/) utility service,
separated by comma. Last argument may also contain template values.

Examples:
```gherkin
And the "JSON" response should have nodes "$.data[0].firstName, data.0.lastName, data.1.age"
And the "JSON" response should have nodes "id"
And the "YAML" response should have nodes "$.users[{{.USER1_ID}}], $.users[{{.USER2_ID}}]"
And the "XML" response should have nodes "//id"
And the "HTML" response should have nodes "//i[1],//i[2]"
```

#### the "(JSON|YAML|XML|HTML)" node "([^"]*)" should be "(bool|boolean|float|int|integer|number|scalar|string)" of value "([^"]*)"
This step allows to check last HTTP(s) response JSON/YAML/XML/HTML node against given value.

First argument `the "(JSON|YAML|XML|HTML)" node` should be expected data format of response body.

Second argument `node "([^"]*)" should` should be expression acceptable by JSON/XML/YAML/HTML-path engine associated with previously selected data format.
Argument accepts template values.

Third argument `be "(bool|boolean|float|int|integer|number|scalar|string)" of` should be one of available data types that you expect.

Last argument `value "([^"]*)"` should be value of given node. Argument accepts template values.

Examples:
```gherkin
And the "JSON" node "firstName" should be "string" of value "{{.RANDOM_FIRST_NAME}}"
And the "YAML" node "$.lastName" should be "scalar" of value "{{.RANDOM_LAST_NAME}}"
And the "JSON" node "{{.AGE_KEY}}" should be "int" of value "{{.RANDOM_AGE}}"
And the "JSON" node "$.age" should be "number" of value "18"
And the "XML" node "//age" should be "int" of value "18"
And the "HTML" node "//head//title" should be "string" of value "my page title"
```

#### the "(JSON|YAML|XML|HTML)" node "([^"]*)" should be "(bool|boolean|float|int|integer|number|scalar|string)" and contain one of values "([^"]*)"
This step allows to check last HTTP(s) response `JSON/YAML/XML/HTML` node against given set of values.

First argument `the "(JSON|YAML|XML|HTML)" node` should be expected data format of response body.

Second argument `node "([^"]*)" should` should be expression acceptable by JSON/XML/YAML/HTML-path engine associated with previously selected data format.
Argument accepts template values.

Third argument `be "(bool|boolean|float|int|integer|number|scalar|string)" of` should be one of available data types that you expect.

Last argument `"([^"]*)"` should be string containing values separated by comma (,).

Examples:
```gherkin
And the "JSON" node "$.age" should be "number" and contain one of values "18, 19, 20"
```

#### the "(JSON|YAML|XML|HTML)" node "([^"]*)" should (not )?contain sub string "([^"]*)
This step allows to check whether string node value contains/ does not contain provided substring.

First argument `the "(JSON|YAML|XML|HTML)" node` should be expected data format of response body.

Second argument `node "([^"]*)" should` should be expression acceptable by JSON/XML/YAML/HTML-path engine associated with previously selected data format.
Argument accepts template values.

Last argument `sub string "([^"]*)` should be any substring to check against.

Examples:
```gherkin
And the "JSON" node "$.lastName" should not contain sub string "smith"
But the "JSON" node "$.lastName" should contain sub string "doe"
And the "HTML" node "//head//title" should contain sub string "App"
```

#### the "(JSON|YAML|XML)" node "([^"]*)" should (not )?be slice of length "(\d+)"
This step allows to check whether given last HTTP(s) response body JSON/YAML/XML node is/is not slice of given length.

First argument `the "(JSON|YAML|XML)" node` should be expected data format of response body.

Second argument `node "([^"]*)" should` should be expression acceptable by JSON/XML/YAML/HTML-path engine associated with previously selected data format.
Argument accepts template values.

Third argument `of length "(\d+)"` should be non-negative integer.

Example:
```gherkin
And the "JSON" node "users" should be slice of length "3"
And the "YAML" node "$.users" should be slice of length "3"
And the "XML" node "//users" should be slice of length "3"
But the "XML" node "//users" should not be slice of length "3"
```

#### the "(JSON|YAML|XML)" node "([^"]*)" should (not )?be "(array|bool|boolean|float|int|integer|map|mapping|nil|null|number|object|sequence|scalar|slice|string)"
This step allows to check whether given last HTTP(s) response body JSON/YAML node has given type.

First argument `the "(JSON|YAML|XML)" node` should be expected data format of response body.

Second argument `node "([^"]*)" should` should be expression acceptable by JSON/XML/YAML/HTML-path engine associated with previously selected data format.
Expression accepts template values.

Third, `be "(array|bool|boolean|float|int|integer|map|mapping|nil|null|number|object|sequence|scalar|slice|string)"` should be one of predefined types.

Examples:
```gherkin
And the "JSON" node "users" should be "slice"
And the "JSON" node "$.data" should be "nil"
And the "YAML" node "$.data" should be "nil"
And the "JSON" node "data.users.{{.USER_ID}}.description" should be "string"
And the "JSON" node "users" should not be "int"
And the "JSON" node "$.data" should not be "null"
And the "YAML" node "$.data" should not be "nil"
And the "JSON" node "data.users.{{.USER_ID}}.description" should not be "bool"
And the "JSON" node "data.users.0.description" should not be "map"
```

#### the "(JSON|YAML|XML|HTML)" node "([^"]*)" should (not )?match regExp "([^"]*)"
This step allows to check whether given last HTTP(s) response body JSON/YAML/XML/HTML node matches/doesn't match given regExp.

First argument `the "(JSON|YAML|XML|HTML)" node` should be expected data format of response body.

Second argument `node "([^"]*)" should` should be expression acceptable by JSON/XML/YAML/HTML-path engine associated with previously selected data format.
Argument accepts template values.

Third argument `match regExp "([^"]*)"` should be valid [regular expression](https://pkg.go.dev/regexp#pkg-overview).

Examples:
```gherkin
And the "JSON" node "lastName" should match regExp "doe-.*"
And the "YAML" node "$.lastName" should not match regExp "doe-.*"
And the "XML" node "//lastName" should match regExp "doe-.*"
And the "HTML" node "//head//title" should match regExp "app-.*"
```

#### the "(JSON)" node "([^"]*)" should be valid according to schema "([^"]*)"
This step allows to check whether given JSON node is valid according to provided as reference schema

First argument `the "(JSON)" node` should be expected data format of response body.

Second argument `node "([^"]*)" should` should be expression acceptable by JSON-path engine.

Argument `schema "([^"]*)"` may be:
* full OS path to schema
* relative OS path to schema. During default setup, command `make env` creates `.env` file with env variable `GODOG_JSON_SCHEMA_DIR=./assets/test_server/doc/schema`. Let's assume, you keep your schemas in `your-project-root-dir/docs/schemas/` and placed godog-example-setup in `your-project-root-dir/tests/godog/`. Then, you have to change environment variable to: `GODOG_JSON_SCHEMA_DIR=./../../docs/schemas`. From now on, you need to pass relative path as you were in `schemas/` directory.
* full valid URL to schema.
  Argument also accepts template values

Examples:
```cucumber
And the "JSON" node "user[0].address" should be valid according to schema "https://www.json-schemas.com/adress.json"
And the "JSON" node "user[{{.USER_ID}}].address" should be valid according to schema "{{.MY_APP_URL}}/adress.json"
```

#### the "(JSON)" node "([^"]*)" should be valid according to schema:
This step allows to check whether given JSON node is valid according to provided as docstring schema

First argument `the "(JSON)" node` should be expected data format of response body.

Second argument `node "([^"]*)" should` should be expression acceptable by JSON-path engine. Argument accepts template values.

Third argument should be Docstring with schema. Argument accepts template values.

Examples:
```gherkin
And the "JSON" node "$.data" should be valid according to schema:
"""
{
    "$schema": "https://json-schema.org/draft/2020-12/schema",
    "title": "users data",
    "description": "users data",
    "type": "array",
    "items": {
        "type": "object",
        "properties": {
            "name": {
                "type": "string"
            },
	    "age": {
                "type": "integer"
            }
        }
    }
}
"""
```