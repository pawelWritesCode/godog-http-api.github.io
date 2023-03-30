---
title: "HTTP response body"
description: "HTTP response body."
lead: "HTTP response body."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### the response body should (not )?have format "(JSON|YAML|XML|HTML|plain text)"
This step allows to check whether given last HTTP(s) response body has/doesn't have given format.

First argument `format "(JSON|YAML|XML|HTML|plain text)"` should be one of available data formats.

Example:
```gherkin
And the response body should have format "JSON"
And the response body should not have format "YAML"
And the response body should have format "XML"
And the response body should have format "plain text"
And the response body should have format "HTML"
```

#### the response body should be valid according to schema "([^"]*)"
This step allows to check wheter given last HTTP(s) response body is valid according to schema. In tesitng, it is common to do that type of assertions. Schema may be used not only in tests, but also in documentation. That kind of step allows to check not only last response body but also helps keep documentation up to date.

Argument `schema "([^"]*)"` may be:
* full OS path to schema
* relative OS path to schema. During default setup, command `make env` creates `.env` file with env variable `GODOG_JSON_SCHEMA_DIR=./assets/test_server/doc/schema`. Let's assume, you keep your schemas in `your-project-root-dir/docs/schemas/` and placed godog-example-setup in `your-project-root-dir/tests/godog/`. Then, you have to change environment variable to: `GODOG_JSON_SCHEMA_DIR=./../../docs/schemas`. From now on, you need to pass relative path as you were in `schemas/` directory.
* full valid URL to schema.
  Also this argument accepts template values.

Examples:
```gherkin
And the response body should be valid according to schema "/usr/local/schemas/user/get_user.json"
And the response body should be valid according to schema "user/get_user.json"
And the response body should be valid according to schema "{{.CWD}}/assets/test_server/doc/schema/user/user.json"
And the response body should be valid according to schema "https://raw.githubusercontent.com/pawelWritesCode/godog-example-setup/main/assets/test_server/doc/schema/user/get_user.json"
```

#### the response body should be valid according to schema:
This step allows to check wheter given last HTTP(s) response body is valid according to schema.

The only one argument, should be Docstring with schema and may contain template values.

Example:
```gherkin
And the response body should be valid according to schema:
"""
{
   "$schema": "https://json-schema.org/draft/2020-12/schema",
   "title": "create user",
   "description": "Valid response from create user endpoint",
   "type": "object"
}
"""
```