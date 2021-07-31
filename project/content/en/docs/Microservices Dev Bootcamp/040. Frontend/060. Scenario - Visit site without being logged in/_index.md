---
type: docs
title: "Scenario: Visit site without being logged in"
linkTitle: "Scenario: Visit site without being logged in"
weight: 60
description: >
  As you fulfill your project's first user story, you will:
   - Receive your first Gherkin
   - Set up BDD testing
   - Create your app's `test-fixture-app`
   - Complete the Gherkin
---


You'll create
`test-fixture-app`: a tool that will allow you to
test your app prior to putting your app into
Production.

## Your project's first Gherkin

~~~
Scenario: Visit site without being logged in
Given the user is not logged in
When the user visits any page
Then the page should redirect to the authentication site
~~~

## Create a branch

`feature/us-202107172050-visit-without-login`
