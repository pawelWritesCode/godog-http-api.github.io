---
title: "RequestDoer"
description: "Service responsible for sending HTTP requests."
lead: "Service responsible for sending HTTP requests."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
weight: 120
toc: true
---

### RequestDoer of type httpctx.RequestDoer
This service is responsible for sending HTTP requests.

```go
// RequestDoer describes ability to make HTTP(s) requests.
type RequestDoer interface {
	Do(req *http.Request) (*http.Response, error)
}
```

To replace it with your own implementation use following setter:
```go
func (apiCtx *APIContext) SetRequestDoer(r httpctx.RequestDoer)
```

Some examples of custom RequestDoer may be:
- one with custom timeout
- one with implemented tracing
- one with custom http.Transport field