---
type: docs
title: "c# Microservice Project Structure"
linkTitle: "c# Microservice Project Structure"
weight: 2
description: >
  c# Microservice Project Structure.
---

This document describes the rule and recommendations for placing different c# projects and folders in your microservice like mvc app, test project, fake project services etc. The main purpose is to define the general guidelines to enforce consistent folder structure across services.

{{% alert title="Note" color="warning" %}}
*The basic project structure will be auto provided to you in your repository when you request a new service. you need to add some folders as per the need. Make sure you adhere to below folder/project structure for all your services.*
{{% /alert %}}

## Structure

```
<repo root>/                              // Repository root
|-- README.md                                 // project-level README
|-- src/                                      // Source code of your service
  |-- **APPNAME**/                            // App-Name directory
      |-- **APPNAME**.csproj (Example: OmOrderManagementSvc.csproj)                 
      |-- Controllers                                               
          |-- HomeController.cs
      |-- Services                            // Services that holds business logic
          |-- IHomeService.cs
          |-- HomeService.cs
      |-- Messages                            // Model classes to send and receive the Messages for commands and events
          |-- Commands
              |-- **Domain**
                  |-- **MessageCommand**.cs
                  |-- **MessageResponse**.cs
              |-- Funds(Example)
                  |-- ValidateFundCommand.cs
                  |-- ValidateFundResponse.cs
          |-- IntegrationEvents
                  |-- ** Domain **
      |-- Features                          // Any helper functions, utilities other 3rd party libraries code 
          |-- ExtensionMethods (Example)
              |-- StringExtensions.cs
          |-- SeedData (Example)
              |-- SeedAddressData.cs
          |-- Encryption
              |-- Encrypt.cs (Example)
      |-- Data
          |-- Models
          |-- Context
              |-- Migrations
              DBContext.cs
      |-- appsettings.json
      |-- Dockerfile
      |-- Startup.cs
      |-- Program.cs
      |-- MTs**APPNAME**.cs                   // This class will have all the app specific logging message Templates.
|- fakes/                                     // directory to store all fake services
  |- **APPNAMEofFake1*.Fake/                  // (Example : OmPurseManagementSvc.Fake/ )App Name of the Service that this app is making external calls to
      |-- **APPNAMEofFake1*.Fake.csproj           
      |-- appsettings.json
      |-- Dockerfile
      |-- other c# project files
  |- **APPNAMEofFake2*.Fake/                  // (Example : OmFeeManagementSvc.Fake/ )App Name of the Service that this app is making external calls to
      |-- **APPNAMEofFake2*.Fake.csproj        
      |-- appsettings.json
      |-- Dockerfile
      |-- other c# project files
|- tests/                                     // folder for test projects (Create Directory for each test type even if there is no Test)
  |- Acceptance.Tests/           // Acceptance Test directory
     |-- **APPNAME**.Acceptance.Tests.csproj
  |- PactConsumer.Tests/         // Pact Consumer Test directory
     |-- **APPNAME**.PactConsumer.Tests.csproj 
  |- PactProvider.Tests/         // Pact Provider Test directory
     |-- **APPNAME**.PactProvider.Tests.csproj 
  |- Unit.Tests/                 // App-Name directory
     |-- **APPNAME**.Unit.Tests.csproj 
  |- **OtherLibrary**.Unit.Tests/            // App-Name directory
     |-- **OtherLibrary**.Unit.Tests.csproj   
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
