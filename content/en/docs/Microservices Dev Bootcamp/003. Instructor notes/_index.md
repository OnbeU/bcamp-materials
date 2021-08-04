---
type: docs
title: "Instructor Notes"
linkTitle: "Instructor Notes"
weight: 003
description: >
  You'll want to read these if you're leading the bootcamp.
---

## Attendee repos, etc. setup

### Create feature branch

feature/attendee-setup

### bc000-theatermanagement-spa

Create repo in GitHub.

.gitignore
~~~
/dist
/node_modules
.vscode
.DS_Store
Thumbs.db
~~~

~~~
npm init
~~~

~~~
npm install -D copyfiles http-server
~~~

package.json
~~~
{
  "name": "project",
  "version": "0.0.0",
  "scripts": {
    "start": "http-server .",
    "build": "copyfiles index.html dist/project/.",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "devDependencies": {
    "copyfiles": "^2.4.1",
    "http-server": "^0.12.3"
  }
}
~~~

index.html
~~~
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=yes">

    <title>Hello World!</title>
</head>

<body>
    Hello World!
</body>

</html>
~~~

### Workflow initial setup

You'll want to do this on **main**, so push, create a pull request, complete the pull request and delete the branches.

Azure | STATIC WEB APPS

Hit the + sign and choose the subscription.

Choose "Angular" as the build preset.

Use the defaults for everything but **location**, which should be `dist/project` (and not just `dist`).

### Workflow customization

Create a branch **feature/workflow-like-onbe-pipeline**

Alter the workflow to look like this one:
~~~
name: Azure Static Web Apps CI/CD

on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - main
  workflow_dispatch:

jobs:
  build_and_stage_job:
    if: github.ref != 'refs/heads/main' && (github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed'))
    runs-on: ubuntu-latest
    name: Build and Stage Job
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true
      - name: Build And Stage
        id: buildstage
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_ORANGE_FOREST_01379A710 }}
          repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for Github integrations (i.e. PR comments)
          action: "upload"
          ###### Repository/Build Configurations - These values can be configured to match your app requirements. ######
          # For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig
          app_location: "/" # App source code path
          api_location: "fake-backend" # Api source code path - optional
          output_location: "dist/project" # Built app content directory - optional
          ###### End of Repository/Build Configurations ######

  close_pull_request_job:
    if: github.event_name == 'pull_request' && github.event.action == 'closed'
    runs-on: ubuntu-latest
    name: Close Pull Request Job
    steps:
      - name: Close Pull Request
        id: closepullrequest
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_ORANGE_FOREST_01379A710 }}
          action: "close"

  build_and_deploy_job:
    if: github.ref == 'refs/heads/main' && (github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed'))
    runs-on: ubuntu-latest
    name: Build and Deploy Job
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true
      - name: Build And Deploy
        id: builddeploy
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_ORANGE_FOREST_01379A710 }}
          repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for Github integrations (i.e. PR comments)
          action: "upload"
          ###### Repository/Build Configurations - These values can be configured to match your app requirements. ######
          # For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig
          app_location: "/" # App source code path
          api_location: "" # Api source code path - optional - LEAVE BLANK BECAUSE PRODUCTION WILL USE K8S NODE
          output_location: "dist/project" # Built app content directory - optional
          ###### End of Repository/Build Configurations ######
~~~

Commit with comment "Workflow is Onbe-fied.".

Push, create a pull request, complete the pull request and delete the branches.

### TODO

TODO: Add more steps.

Lock down main.

 - Settings | Branches | Add rule
 - Branch name pattern: main
 - Require pull request reviews before merging: true
 - Include administrators: False

