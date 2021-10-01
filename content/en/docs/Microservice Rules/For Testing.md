---
type: docs
title: "Microservice Rules for Testing"
linkTitle: "Rules for Testing"
description: >
  The rules for testing that make microservices work.
---

## Rule: Each microservice tests its own behavior
If you break this rule…
 - …then the microservices must be manually tested via exploratory testing, which is more error-prone.

## Rule: No microservice tests the behavior of another microservice
If you break this rule…
 - …then the microservices aren’t independent.
 - …then you’ve created tests that aren’t connected to the other microservices’ repo or deployment pipeline, so they have no teeth.
 - …then in the future your tests could fail (and your microservice will be unable to deploy) when the other microservice changes its behavior, which it is allowed to do.

## Rule: Each microservice specifies consumer-defined contracts with its providers
If you break this rule…
 - …then a provider can deploy a version that breaks the microservice.
 - …then the consumer can deploy a version when its providers don’t support its needs, so the consumer will fail in Production.

## Rule: Each microservice tests all its consumers’ consumer-defined contracts
If you break this rule…
 - …then the consumers won’t be able to deploy.
 - …in the case of a BFF and its frontend consumer’s contracts, then the frontend will have to implement non-HTTP Pact contracts with the backend services, which are more difficult to write and maintain.

## Rule: Each HTTP client class for a provider must have 100% line-of-code coverage by its Pact tests
If you break this rule…
 - …then you might accidentally break Rule: Each microservice specifies consumer-defined contracts with its providers.

## Rule: Each domain event type should be the “Then” clause in one or more Gherkins
If you break this rule…
 - …then the business/reporting needs for the domain event will not be clearly defined.
