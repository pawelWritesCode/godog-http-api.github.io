---
title: "Debugger"
description: "Service responsible for debugging."
lead: "Service responsible for debugging."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
weight: 120
toc: true
---

### Debugger of type debugger.Debugger
This service is useful for debugging. It is self-aware service with mutate state.

```go
// Debugger represents debugger.
type Debugger interface {
	// Print prints provided info.
	Print(info string)

	// IsOn tells whether debugging mode is activated.
	IsOn() bool

	// TurnOn turns on debugging mode.
	TurnOn()

	// TurnOff turns off debugging mode.
	TurnOff()

	// Reset resets debugging mode to init state.
	Reset(isOn bool)
}
```
To replace it with your own implementation use following setter.
```go
// SetDebugger sets new debugger for State.
func (apiCtx *APIContext) SetDebugger(d debugger.Debugger)
```

Some examples of custom debugger may be:
- one which do not print to console, but to file
- one which output is colored
- one which output may be prefixed or formatted differently
