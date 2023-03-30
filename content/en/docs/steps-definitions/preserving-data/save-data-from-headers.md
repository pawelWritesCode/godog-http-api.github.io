---
title: "Save data from headers."
description: "Save data from headers."
lead: "Save data from headers."
date: 2023-03-27T08:48:57+00:00
lastmod: 2023-03-27T08:48:57+00:00
draft: false
weight: 100
toc: true
---

#### I save from the last response header "([^"]*)" as "([^"]*)"
This step allows to save given header value from last response.

First argument `header "([^"]*)" as` should be upper case-sensitive name of header from last HTTP(s) response.

Last argument `as "([^"]*)"` allows you to pick name under which picked header value will be saved in scenario cache.