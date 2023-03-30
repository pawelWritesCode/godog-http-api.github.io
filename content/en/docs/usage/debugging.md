---
title: "Debugging"
description: "How to debug scenarios."
lead: "How to debug scenarios."
date: 2023-03-27T13:59:39+01:00
lastmod: 2023-03-27T13:59:39+01:00
draft: false
images: []
weight: 120
toc: true
---

Writing tests especially in the beginning is not easy. That is why framework is developed with debugging in mind.

Service responsible for debugging is [Debugger](/docs/utility-services/debugger/).

In code, inside methods, it usually looks like this:
```go
if s.Debugger.IsOn() {
	command, _ := http2curl.GetCurlCommand(req)
	s.Debugger.Print(command.String())
}
```
Whenever you write your own custom methods, add similar code to provide additional info while working with turned on debugging mode.

If you want to debug scenario, first thing you want to do is to selectively run feature. See [CLI: godog](/docs/usage/godog-cli/). :
```shell
godog run features/path/to/your/feature.feature
```

If you have to run only one scenario, the best way is to add tag over it:
```gherkin
@wip
Scenario: Successfully send avatar
```

and then run it with following command:
```
godog run --tags=wip
```
or
```shell
go test -v --godog.tags=wip
```

Debugging mode may be turned on in two ways:
1. globally, by setting environment variable: `GODOG_DEBUG=true` in `.env` file,
2. in scenario, using `I start debug mode` and `I stop debug mode` steps.

First option turns on debugger for every scenario. It is not good idea to run whole regression (all tests) when debug mode is on,
because output will be large and hard to read. Run test by OS path or tag as described above.

Second option allows to focus selectively on steps. For example
```gherkin
Given I start debug mode
When I send request "CREATE_USER"
Given I stop debug mode
```

Will only turn on debugger for `I send request "CREATE_USER"` step. In this case, output will be similar to:
```gherkin
Given I start debug mode                                                                # scenario.go:295 -> *Scenario
debug: curl -X 'POST' -d '    {
        "firstName": "CźĄda",
        "lastName": "doe-፫ﲀᆫ𝑙₰",
        "age": 35,
        "description": "hTIDcADY HWOiH olnXJiZT hFfusyFx",
        "friendSince": "2022-03-02T08:54:43Z"
    }' -H 'Content-Type: application/json' -H 'Cookie: csrf_token=this_cookie_is_unnecessary_just_added_for_demonstration' 'http://localhost:1234/users'
debug: last response body:

{"id":2,"firstName":"CźĄda","lastName":"doe-፫ﲀᆫ𝑙₰","age":35,"description":"hTIDcADY HWOiH olnXJiZT hFfusyFx","friendSince":"2022-03-02T08:54:43Z"}


When I send request "CREATE_USER"                                                  # scenario.go:146 -> /defs.Scenario.ISendRequest-fm
Given I stop debug mode  
```

As you see, debugging mode, for sending HTTP(s) request step shows CURL that is sent to server and response body from this request.
You can use this CURL to examine, whether your request was composed properly or play on-site with it.
Additionally, you see server response immediately for this request.

It's worth to mention, that you may run whole test regression (all tests) and output will be normal, but with additional lines from debugger just for that step.

Another thing, you may want to use is step:
```gherkin
Given I print last response body
```
It simply prints last response body to console.

Or you may want to see what's in scenario cache. Do it with following:
```gherkin
Given I print cache data
```

Lastly, if your scenario is too long, you may want to stop it half way. To do this, use step:
```gherkin
Given I stop scenario execution
```