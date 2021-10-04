---
type: docs
title: "Microservice Rules for Data"
linkTitle: "Rules for Data"
description: >
  The rules for data that make microservices work.
---

## Rule: Each microservice has its own database; no sharing

## Rule: Each microservice has a command line container which performs database migrations at deploy-time
If you break this rule…
 - …by instead running the migrations at startup then your startup might fail because multiple instances try to run the migrations simultaneously.
 - …by instead running the migrations at startup then it’s too late to prevent a version from deploying if that version’s migration has bugs, which means the microservice will simply stop functioning.

## Rule: When the microservice no longer needs data for its own purposes that data may be deleted.
