---
type: docs
title: "Microservice Rules for Domain Events"
linkTitle: "Rules for Domain Events"
description: >
  The rules for domain events that make microservices work.
---

## Rule: Any synchronous operation should result in the emission of one or more domain events.

## Rule: All domain events which alter data should be emitted via the outbox pattern
If you break this rule…
 - …there is a risk that the operation will succeed but the event will not be emitted.

