a---
title: "HTTP response Cookies"
description: "HTTP response Cookies."
lead: "HTTP response Cookies."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### the response should (not )?have cookie "([^"]*)"
This step checks whether last  HTTP(s) response has/doesn't have given cookie.

The only one argument `have cookie "([^"]*)"` should be name of cookie.

Examples:
```gherkin
And the response should have cookie "session_id"
And the response should not have cookie "csrf_token"
```

#### the response should have cookie "([^"]*)" of value "([^"]*)"
This step checks whether last HTTP(s) response has given cookie of given value.

First argument `cookie "([^"]*)" of` should be cookie name.

Second argument `value "([^"]*)"` should be cookie value. This argument accepts template values.

Examples:
```gherkin
And the response should have cookie "mobile_format" of value "false"
And the response should have cookie "user_name" of value "{{.RANDOM_USER_FIRST_NAME}}_{{.RANDOM_USER_LAST_NAME}}"
```

#### the response cookie  "([^"]*)" should (not )?match regExp "([^"]*)"
This step checks whether last HTTP(s) response has given cookie and compares it to provided regExp.

First argument `cookie "([^"]*)" of` should be cookie name.

Second argument `regExp "([^"]*)"` should be valid regular expression acceptable by standard go library.

Examples:
```gherkin
And the response cookie  "user_name" should match regExp "john.*"
```