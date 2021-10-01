---
type: docs
title: "Microservice Rules for Feature Management"
linkTitle: "Rules for Feature Management"
description: >
  The rules for feature management (synthetic behavior, feature flags) that make microservices work.
---

## Rule: Each microservice should define its synthetic behavior

## Rule: Feature toggles are never applied to backend services
If you break this rule…
 - …then untestable/unusable code will be deployed.

## Rule: The source of truth for any report is an aggregation of domain events
If you break this rule…
 - …by pulling report data from a microservice’s database then you also break Rule: Each microservice has its own database; no sharing.
 - …the microservice will have to hang onto the data forever, which breaksRule: When the microservice no longer needs data for its own purposes that data may be deleted.
