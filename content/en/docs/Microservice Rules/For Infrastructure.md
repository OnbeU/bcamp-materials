---
type: docs
title: "Microservice Rules for Infrastructure"
linkTitle: "Rules for Infrastructure"
description: >
  The rules for infrastructure that make microservices work.
---

## Rule: Each microservice specifies its infrastructure needs via files in its repo
If you break this rule…
 - …there will be nothing to stop your microservice from being deployed if its infrastructure needs won’t be met.
 - …the microservice will fail in Production if its infrastructure needs aren’t met.
