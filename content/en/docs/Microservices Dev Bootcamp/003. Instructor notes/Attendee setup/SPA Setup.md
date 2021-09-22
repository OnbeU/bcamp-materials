---
type: docs
title: "SPA Setup"
linkTitle: "SPA Setup"
weight: 040
description: >
  Modifying the SPA.
---

## Remove the Drive-Ins Inc. Pact file

Remove `dii-theatermanagement-spa-dii-theatermanagement-bff.json`

Commit with comment "Removed Pact from the template project"

## fake\.gitignore and fake\.gitattributes

Copy these from a C# project.

## npm test

~~~
npm install
npm test
~~~

Commit with comment "fake\.gitignore and fake\.gitattributes; npm test"

## Remove the .suo file and such from source control

Remove the directory under `fake\.vs` from the fake\.vs directory

Commit with comment "Removed .suo and such from source control"

## FeatureFlagsService and FeatureFlag class

Generate some code. Note that our `Config` class is a just a DTO and doesn't need
automated tests, so we use the `--skip-tests=true` option.

~~~
npx ng generate class core/singleton-services/featureflags/featureflag --skip-tests=true
npx ng generate service core/singleton-services/featureflags/featureflags
~~~

Inspect the changes made to:

~~~
src\app\core\singleton-services\config\config.service.ts
src\app\core\singleton-services\config\config.ts
src\app\core\singleton-services\config\config.service.spec.ts
~~~

Commit with comment "ng g class & service featureflags featureflag"