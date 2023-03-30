---
title: "Create your own steps"
description: "How to create your own steps."
lead: "How to create your own steps."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
images: []
weight: -1
toc: true
---

This repository contains only skeleton with low-level steps for testing JSON/XML/YAML or HTML API. As you start testing your unique project, most likely you will create new steps matching your business logic. 

To do so, first, you have to add it in `defs/scenario.go` and later, use it to map it with reg-exp - english sentence in `main_test.go`.

This setup supports you with adding new steps by exposing internal [APIContext's services](https://github.com/pawelWritesCode/gdutils/blob/master/context.go#L18).

As an example, let's assume, before you can work with your API, you have to log-in user. Most likely, at first, you will write scenario like this:
```gherkin
Feature: Authentication

  Scenario: Successful login

    #---------------------------------------------------------------------------------
    # Successful authentication
    Given I send "POST" request to "{{.MY_APP_URL}}/auth/login" with body and headers:
    """
    {
        "body": {
            "email": "{{.ADMIN_EMAIL}}",
            "password": "{{.ADMIN_PASSWORD}}"
        },
        "headers": {}
    }
    """
    Then the response status code should be 200
    And the response body should have type "JSON"
    And the "JSON" response should have node "access_token"
    And I save from the last response "JSON" node "access_token" as "USER_TOKEN"
```

Naturally, previously you added environment variables similar to `GODOG_ADMIN_EMAIL` and `GODOG_ADMIN_PASSWORD` into `.env` file and then injected it, into all scenario caches with following directives (`main_test.go`):
```go
	ctx.Before(func(ctx context.Context, sc *godog.Scenario) (context.Context, error) {
		scenario.APIContext.ResetState(isDebug)

		// Here you can define more scenario-scoped values using scenario.APIContext.Cache.Save() method
		scenario.APIContext.Cache.Save("MY_APP_URL", os.Getenv(envMyAppURL))
		scenario.APIContext.Cache.Save("CWD", wd) // current working directory - full OS path to this file

        scenario.APIContext.Cache.Save("ADMIN_EMAIL", os.Getenv("GODOG_ADMIN_EMAIL"))
        scenario.APIContext.Cache.Save("ADMIN_PASSWORD", os.Getenv("GODOG_ADMIN_PASSWORD"))

		return ctx, nil
	})
```

Quickly, you realize, that each scenario need to contain above steps. You try to figure out, how to minimize amount of steps required in each scenario and you come up with idea of writing equivalent higher-level step:
```gherkin
Given I log in user with email "{{.ADMIN_EMAIL}}" and password "{{.ADMIN_PASSWORD}}" and save its access token in scenario cache as "ADMIN_ACCESS_TOKEN"
``` 

First, what you should do, is to write placeholder method in `scenario.go`:
```go
func (s *Scenario) ILogInUserWithEmailAndPasswordAndSaveItsAccessTokenInScenarioCacheAs(emailTemplate, passwordTemplate, cacheKey string) error {
	return godog.ErrPending
}
```

Then, you should map this func to sentence in `main_test.go`:
```go
ctx.Step(`^I log in user with email "([^"]*)" and password "([^"]*)" and save its access token in scenario cache as "([^"]*)"$`, scenario.ILogInUserWithEmailAndPasswordAndSaveItsAccessTokenInScenarioCacheAs)
```

At this moment, you have pending step. Now, you need to fulfill method's body.

First what you want to do is to use `APIContext.TemplateEngine` service to obtain data from template values of first and second step argument. You may want to pass fixed email and password, but also you may want to generate data, register user with it and then pass template values of new user or obtain them from `.env` file like you did above. For example:
```gherkin
Given I log in user with email "admin@gmail.com" and password "admin123" and ...
Given I log in user with email "{{.RANDOM_EMAIL}}" and password "{{.RANDOM_PASSWORD}}" and ...
Given I log in user with email "{{.ADMIN_EMAIL}}" and password "{{.ADMIN_PASSWORD}}" and ...
``` 
So you have to add following code to make it happen:
```go
func (s *Scenario) ILogInUserWithEmailAndPasswordAndSaveItsAccessTokenInScenarioCacheAs(emailTemplate, passwordTemplate, cacheKey string) error {
	email, err := s.APIContext.TemplateEngine.Replace(emailTemplate, s.APIContext.Cache.All())
	if err != nil {
		return err
	}

	password, err := s.APIContext.TemplateEngine.Replace(passwordTemplate, s.APIContext.Cache.All())
	if err != nil {
		return err
	}
}
```

Next, you need to send HTTP(s) request. To do so, you use already written method (_ISendRequestToWithBodyAndHeaders_):
```go
func (s *Scenario) ILogInUserWithEmailAndPasswordAndSaveItsAccessTokenInScenarioCacheAs(emailTemplate, passwordTemplate, cacheKey string) error {
	email, err := s.APIContext.TemplateEngine.Replace(emailTemplate, s.APIContext.Cache.All())
	if err != nil {
		return err
	}

	password, err := s.APIContext.TemplateEngine.Replace(passwordTemplate, s.APIContext.Cache.All())
	if err != nil {
		return err
	}

	docString := godog.DocString{Content: fmt.Sprintf(`{
	"body": {
		"email": "%s",
		"password": "%s"
	},
	headers: {}
}`, email, password)}
	if err = s.ISendRequestToWithBodyAndHeaders(http.MethodPost, "{{.MY_APP_URL}}/auth/login", &docString); err != nil {
		return err
	}
}
```

After that, you want to make few assertions:
```go
func (s *Scenario) ILogInUserWithEmailAndPasswordAndSaveItsAccessTokenInScenarioCacheAs(emailTemplate, passwordTemplate, cacheKey string) error {
	email, err := s.APIContext.TemplateEngine.Replace(emailTemplate, s.APIContext.Cache.All())
	if err != nil {
		return err
	}

	password, err := s.APIContext.TemplateEngine.Replace(passwordTemplate, s.APIContext.Cache.All())
	if err != nil {
		return err
	}

	docString := godog.DocString{Content: fmt.Sprintf(`{
	"body": {
		"email": "%s",
		"password": "%s"
	},
	headers: {}
}`, email, password)}
	if err = s.ISendRequestToWithBodyAndHeaders(http.MethodPost, "{{.MY_APP_URL}}/auth/login", &docString); err != nil {
		return err
	}

	if err = s.TheResponseStatusCodeShouldBe(200); err != nil {
		return err
	}

	if err = s.TheResponseBodyShouldHaveType("JSON"); err != nil {
		return err
	}

	if err = s.TheResponseShouldHaveNode("JSON", "access_token"); err != nil {
		return err
	}
}
```

Now, you only need to save `access_token` node and add short step documentation, to help others and future yourself work with that step:
```go
// ILogInUserWithEmailAndPasswordAndSaveItsAccessTokenInScenarioCacheAs logs in user in my app and save it's access token in provided cacheKey
// internally method relies upon MY_APP_URL cache key.
func (s *Scenario) ILogInUserWithEmailAndPasswordAndSaveItsAccessTokenInScenarioCacheAs(emailTemplate, passwordTemplate, cacheKey string) error {
	email, err := s.APIContext.TemplateEngine.Replace(emailTemplate, s.APIContext.Cache.All())
	if err != nil {
		return err
	}

	password, err := s.APIContext.TemplateEngine.Replace(passwordTemplate, s.APIContext.Cache.All())
	if err != nil {
		return err
	}

	docString := godog.DocString{Content: fmt.Sprintf(`{
	"body": {
		"email": "%s",
		"password": "%s"
	},
	headers: {}
}`, email, password)}
	if err = s.ISendRequestToWithBodyAndHeaders(http.MethodPost, "{{.MY_APP_URL}}/auth/login", &docString); err != nil {
		return err
	}

	if err = s.TheResponseStatusCodeShouldBe(200); err != nil {
		return err
	}

	if err = s.TheResponseBodyShouldHaveType("JSON"); err != nil {
		return err
	}

	if err = s.TheResponseShouldHaveNode("JSON", "access_token"); err != nil {
		return err
	}

	if err = s.ISaveFromTheLastResponseNodeAs("JSON", "access_token", cacheKey); err != nil {
		return err
	}
	
	return nil
}
```