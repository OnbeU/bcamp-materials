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
