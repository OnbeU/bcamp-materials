---
type: docs
title: "Microservice Rules for Deployment"
linkTitle: "Rules for Deployment"
description: >
  The rules for deployment that make microservices work.
---

## Rule: Each microservice is deployed independently; not in lock-step with other microservices’ deployments

## Rule: Deployments should be frequent and small
If you break this rule…
 - …defects become difficult to track to their causes.

## Rule: Each backend microservice should provide a health check endpoint

## Rule: All microservice projects must follow the naming conventions required by the pipeline
