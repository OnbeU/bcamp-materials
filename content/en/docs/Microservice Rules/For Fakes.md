---
type: docs
title: "Microservice Rules for Fakes"
linkTitle: "Rules for Fakes"
description: >
  The rules for fakes that make microservices work.
---

## Rule: Each pull request is a stage site
If you break this rule…
 - …then approvers will not be able to explore the microservice before approving.
 - …then no exploratory testing can occur between local development and production.

## Rule: Each microservice fakes its providers
If you break this rule…
 - …then you also break Rule: Every pull request is a stage site.
 - …the no exploratory testing can occur during local development.
