---
type: docs
title: "c# Microservice Project Structure"
linkTitle: "c# Microservice Project Structure"
weight: 2
description: >
  c# Microservice Project Structure.
---

This document describes the rule and recommendations for placing different c# projects in your microservice like mvc app, test project, fake project service etc. The main purpose is to define the general guidelines to enforce consistent folder structure across services.

{{% alert title="Note" color="warning" %}}
_The project structure will be auto provided to you in your repository when you request a new service._
{{% /alert %}}

## Structure

```
<project root>/                              // Root of your project
|- README.md                                 // project-level README
|- src/                                      // Source code of your service
  |- **APPNAME**/                            // App-Name directory
      |- **APPNAME**.csproj                  // csharp MVC project files.
      |- appsettings.json
      |- other c# project files
|- fake/                                     // directory to store all fake services
  |- **FAKE1-APPNAME**/                      // Fake Service 1
      |- **FAKE1-APPNAME**.csproj            // csharp MVC project files.
      |- appsettings.json
      |- other c# project files
  |- **FAKE2-APPNAME**/                      // Fake Service 2
      |- **FAKE2-APPNAME**.csproj            // csharp MVC project files.
      |- appsettings.json
      |- other c# project files
|- test/                                     // folder for test projects (Create Directory for each test type even if there is no Test)
  |- **APPNAME**.Acceptance.Tests/           // Acceptance Test directory
  |- **APPNAME**.PactConsumer.Tests/         // Pact Consumer Test directory
  |- **APPNAME**.PactProvider.Tests/         // Pact Provider Test directory
  |- **APPNAME**.Unit.Tests/                 // App-Name directory
  |- **OtherLibrary**.Unit.Tests/            // App-Name directory
|- pacts
  |- contracts                               // This stores the generated contract json files
  |- logs
|- .gitignore
|- .dockerignore
|- **APPNAME**.sln                            // project solution file
|- docker-compose.dcproj
|- docker-compose.override.yml
|- docker-compose.yml

```
