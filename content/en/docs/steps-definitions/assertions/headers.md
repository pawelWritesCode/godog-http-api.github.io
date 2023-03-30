---
title: "HTTP response headers"
description: "HTTP response headers."
lead: "HTTP response headers."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### the response should (not )?have header "([^"]*)"
This step checks whether last HTTP(s) response has/doesn't have given header. Argument `have header "([^"]*)"` is case sensitive.

Examples:
```gherkin
And the response should have header "Content-Length"
And the response should not have header "Content-Type"
```

#### the response should have header "([^"]*)" of value "([^"]*)"
This step checks whether last HTTP(s) response has given header of given value.

First argument `header "([^"]*)" of` should be name of header and is case-sensitive, second argument `of value "([^"]*)"` should be value of header, it may contain template values.

Examples:
```gherkin
And the response should have header "Content-Type" of value "{{.CONTENT_TYPE_JSON}}; charset=UTF-8"
```