---
title: "Sending request using multiple steps"
description: "Sending request using multiple steps."
lead: "Sending request using multiple steps."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I prepare new "(GET|POST|PUT|PATCH|DELETE|HEAD)" request to "([^"]*)" and save it as "([^"]*)"
This step prepares new HTTP(s) request.

First argument `send "(GET|POST|PUT|PATCH|DELETE|HEAD)" request` is one of well known HTTP request methods.

Second argument `to "([^"]*)" with` should be full valid URL. Argument accepts template values. For example `to "{{.MY_APP_URL}}/api/user" with` or `to "https://www.example.com" with`. Of course `{{.MY_APP_URL}}` should be previously saved in scenario cache.

Last argument `and save it as "([^"]*)"$` allows you to pick name under which prepared request will be saved in scenario cache.

Example:
```gherkin
Given I prepare new "POST" request to "{{.MY_APP_URL}}/users" and save it as "CREATE_USER"
```

#### I set following headers for prepared request "([^"]*)":
This step allows to set headers for previously prepared request

First argument `request "([^"]*)"` should be name under which request is saved in scenario cache. For example `request "CREATE_USER"`.

Second argument should be Docstring in form of YAML or JSON with headers. It accepts template values.

Example:
```gherkin
Given I set following headers for prepared request "CREATE_USER":
"""
---
Content-Type: application/json
"""
```
or
```gherkin
Given I set following headers for prepared request "CREATE_USER":
"""
{
   "Content-Type": "application/json"
}
"""
```

<a name="iSetFollowingForm"></a>
#### I set following form for prepared request "([^"]*)":
This step allows to set form for prepared request.

First argument `request "([^"]*)"` should be name under which request is saved in scenario cache. For example `request "CREATE_USER"`.

Second argument should be Docstring in YAML or JSON with form fields and their corresponding values. To attach any file, use following syntax: `file://path/to/file` as key value.

Its worth to mention that method automatically sets `Content-Type: multipart/form-data` header with proper boundary. If you want to change
`Content-Type` header to `application/x-www-form-urlencoded`, afterwards use step for setting headers to overwrite it.

Example:
```gherkin
Given I set following form for prepared request "AVATAR_REQUEST":
"""
{
    "name": "{{.RANDOM_AVATAR_NAME}}.gif",
    "avatar": "file://{{.CWD}}/assets/gifs/hand-pointing-left.gif"
}
"""
```

#### I set following cookies for prepared request "([^"]*)":
This step allows to set cookies for prepared request.

First argument `request "([^"]*)"` should be name under which request is saved in scenario cache. For example `request "CREATE_USER"`.

Second argument should be Docstring in YAML or JSON with list of elements having keys `name` and `value`.

Examples:
```gherkin
Given I set following cookies for prepared request "CREATE_USER":
"""
[
  {
     "name": "csrf_token",
     "value": "this_cookie_is_unnecessary_just_added_for_demonstration"
  }
]
"""
```

#### I set following body for prepared request "([^"]*)":
This step allows to set request body in any format.

First argument `request "([^"]*)"` should be name under which request is saved in scenario cache. For example `request "CREATE_USER"`.

Second argument should be Docstring in any form. It accepts template values.

Examples:
```gherkin
Given I set following body for prepared request "CREATE_USER":
"""
{
    "firstName": "{{.RANDOM_FIRST_NAME}}",
    "lastName": "{{.RANDOM_LAST_NAME}}",
    "age": {{.RANDOM_AGE}}
}
"""
```

```gherkin
Given I set following body for prepared request "CREATE_USER":
"""
plain text
"""
```

```gherkin
Given I set following body for prepared request "CREATE_USER":
"""
---
firstName: {{.RANDOM_FIRST_NAME}}
age: {{.RANDOM_AGE}}
"""
```

#### I send request "([^"]*)"
This step sends previously prepared request. May be used many times for one request.

Example:
```gherkin
When I send request "CREATE_USER"
```