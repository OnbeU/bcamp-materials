---
type: docs
title: "HTTP Endpoint Patterns"
linkTitle: "HTTP Endpoint Patterns"
weight: 4
description: >
  Some simple patterns to determine the HTTP status codes your REST endpoints should return. 
aliases:
  - /link-to/types-of-rest-endpoints
---
<p><a href="/link-to/types-of-rest-endpoints">Permalink</a> to this page</p>

## Why getting the HTTP status codes right is important

Not only do we want to make sure that our APIs provide HTTP status codes
in a consitent way across all APIs, it's also important that (nearly) all REST APIs
provide an accurate OpenAPI specification.

The OpenAPI specification lists the status codes that a client can expect.

## Don't use *that* chart!

When writing a REST endpoint, choosing from the number of available HTTP status codes 
can be overwhelming.

For example, 
[this chart](https://github.com/for-GET/http-decision-diagram).

<img src="/images/restful-apis/endpoint-patterns/http-decision-diagram.png" alt="HTTP Decision Diagram v4.0.201410" width=40% />

But you don't need that chart. Presented here are some simple patterns to determine which HTTP status codes your REST endpoints should
provide

## How to get your endpoint's HTTP status codes right

First, determine which type of endpoint you're writing.

Then follow the associated pattern, below.