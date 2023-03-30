---
title: "Sending request using single step."
description: "Sending request using single step."
lead: "Sending request using single step."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I send "(GET|POST|PUT|PATCH|DELETE|HEAD)" request to "([^"]*)" with body and headers:
This steps allows to send HTTP(s) request.

First argument `send "(GET|POST|PUT|PATCH|DELETE|HEAD)" request` is one of well known HTTP request methods.

Second argument `to "([^"]*)" with` should be full valid URL. Argument accepts template values. For example `to "{{.MY_APP_URL}}/api/user" with` or `to "https://www.example.com" with`. Of course `{{.MY_APP_URL}}` should be previously saved in scenario cache.

Last argument, should be Docstring in form of YAML or JSON with keys: `body`, `headers`. For example
```
    """
    {
        "body": {
            "firstName": "{{.RANDOM_FIRST_NAME}}",
            "lastName": "{{.RANDOM_LAST_NAME}}",
            "age": {{.RANDOM_AGE}}
        },
        "headers": {
            "Content-Type": "application/json"
        }
    }
    """
```
or YAML equivalent
```
"""
---
body:
  firstName: "{{.RANDOM_FIRST_NAME}}"
  lastName: "{{.RANDOM_LAST_NAME}}"
  age: {{.RANDOM_AGE}}
headers:
  Content-Type: application/json
"""
```

Example:
```gherkin
    When I send "DELETE" request to "{{.MY_APP_URL}}/users/{{.USER_ID}}" with body and headers:
    """
    {
        "body": {},
        "headers": {
            "Content-Type": "application/json"
        }
    }
    """
```