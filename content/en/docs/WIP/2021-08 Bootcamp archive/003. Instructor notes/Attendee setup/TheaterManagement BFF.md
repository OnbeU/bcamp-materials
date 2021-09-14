---
type: docs
title: "TheaterManagement BFF"
linkTitle: "TheaterManagement BFF"
weight: 020
description: >
  TheaterManagement BFF.
---

## Create a new project and solution.

~~~
Template: ASP.NET Core Web API
Project name: Bc###TheaterManagementBff
Location: c:\src\onbe

Target Framework: .NET 5.0
Authentication Type: None
Configure for HTTPS: Off
Enable Docker: Off
Enable OpenAPI support: On
~~~

### Move the project into the src directory

### Move the project into the src directory

 - Remove the project from the solution.
 - Create a `src` directory.
 - Move the project folder `Bc###TheaterManagementBff` into that directory.
 - Add the project back into the solution.


## Create GitHub repo

{{% alert title="No more masters" color="primary" %}}
We're going to take some steps so that the branch is named `main` and not `master`.
{{% /alert %}}

On the "Git Changes" tab, hit "Create Git Repository..."

Choose "Local only". (Do not choose "Push to a new remote / GitHub" at this time because this would make it harder to name the branch `main` and not `master`.)

Hit the "Create" button.

Git > Open In Command Prompt

~~~
git branch -m master main
exit
~~~

On the "Git Changes" tab, hit "Push"

Choose "Push to a new remote / GitHub"

~~~
Owner: OnbeUStudent
Repository name: bc###-theatermanagement-bff
Private repository: Off
Push "Push" button
~~~

## Lock down main

On the GitHub repository page:
 - Settings | Branches | Add rule
 - Branch name pattern: main
 - Require pull request reviews before merging: true
 - Include administrators: False

## Docker setup

### Create feature branch

~~~
feature/docker-setup
~~~

### Add Docker compose orchestration

Right-click on project.

Add > Container Orchestrator Support... > Docker Compose

Target OS: Linux

Commit with comment "Added Docker compose orchestration.".

