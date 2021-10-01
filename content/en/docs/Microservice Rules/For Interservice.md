---
type: docs
title: "Microservice Rules for Interservice Behavior and Communication"
linkTitle: "Rules for Interservice"
description: >
  The rules for interservice behavior and communication that make microservices work.
---

## Rule: For each domain-wide aggregate there is one microservice which owns the lifetime of that aggregate

## Rule: No microservice should expose endpoints in Production that weren’t requested as part of a consumer-defined contract
If you break this rule…
 - …you will have provided endpoints which are only useful to attackers.
 - …development time and testing time will be wasted.

## Rule: Each frontend microservice accesses backend services through a BFF microservice
If you break this rule…
 - …authorization becomes very complex.
 - …application-specific rules will have to be written into backend microservices, which makes the backend microservices trickier to write and which can break the boundaries between teams.
 - …the attack surface becomes wide.

## Rule: All aggregates should follow the value objects pattern: The aggregate has only an ID and all of its properties are immutable value objects.

## Rule: All communication between backend microservices should occur via Dapr sidecars
If you break this rule…
 - …proper tracing is not guaranteed.

## Rule: All microservice projects should be configured for HTTP and not HTTPS.

