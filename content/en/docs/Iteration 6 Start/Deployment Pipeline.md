---
type: docs
title: "Deployment Pipeline"
linkTitle: "Deployment Pipeline"
weight: 4
description: >
  Continuous Deployment.
---


Continuous deployment is a strategy in software development where code changes to an application are released automatically into the production environment. In practice, continuous deployment means that a developer’s change to the application could go live within minutes of writing it (assuming it passes automated testing). This is an excellent way to accelerate development and take pressure off the team as there isn't a *ReleaseDay* anymore.

At Onbe we will be using a common way to deploy application code. We have built a unified deployment pipeline for each type of application. Development team needs to call the unified pipeline from their code. Below are the instructions on how to consume the unified pipeline(s) for Service (C#), SPA (Angular) and Shared Library (Nuget) applications. 

### Service (C#) Application
---
This pipeline will be used by all the BFFs and Services that were created following the *CSharp Microservice Project structure and naming guidelines*. 
- **Prerequisites** before consuming the pipeline into your application. 
  - Application needs to be docker enabled. See [Add Container Orchestration Support](/docs/iteration-6-start/create-a-new-service/#csharp-add-container-orchestrator)
  - Application must contain health check route ```/hc```. If /hc is not present then pipeline will not be able to deploy your application. The pipeline is configured to deploy application in Azure Kubernetes cluster with K8s Liveness and Readiness probe pointing to /hc route. See [Add Health Check and Health Check Route](/docs/iteration-6-start/create-a-new-service/#csharp-add-healthcheck)

_More information on [Kubernetes Container probes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-probes)_


- Add Github deployment pipeline
    1. Create a ```.github/workflows``` directory in your repository on GitHub if this directory does not already exist.
    2. In the ```.github/workflows``` directory, create a file named ```deploment.yml```. For more information, see ["Creating new files."](https://docs.github.com/en/repositories/working-with-files/managing-files/creating-new-files)
    3. Copy the below YAML contents into the ```deploment.yml``` file.
        - Change the value for **APP_NAME** parameter to the name of your application. (e.g. OmOrderApprovalSvc)
        - Change the value of **PACT_PACTICIPANT** parameter to the name of your repository. (e.g. om-orderapproval-svc)
        - If your application contains the provider pact test is verifying the pact consumer contracts then change the value to true.
        - You don't need to change any value for secrets or add any secrets. Secrets will be handled by devops team.

```
 name: deployment

on:
  pull_request:
    types: [opened, synchronize, closed]
  push:
    branches:
      - main

jobs:
  call-svc-deployment-workflow:
    uses: Onbe/devopssetup/.github/workflows/csharp-svc-deployment.yml@main
    with:
        APP_NAME: YourAppName   #Name of your main csproj
        PACT_PACTICIPANT: PactPacticipantId # unique name of the application that is being used at pact broker for this application. mostly this is same as your git repo name.
        VERIFY_PROVIDER_PACT: false   # true if this application is acting as pact provider for other applications else false
    secrets:
        AZURE_CREDENTIALS: ${{ secrets.AZURE_CREDENTIALS }}
        PACT_BROKER_BASE_URL: ${{ secrets.PACT_BROKER_BASE_URL }}
        PACT_BROKER_TOKEN: ${{ secrets.PACT_BROKER_TOKEN }}
        REGISTRY_LOGIN_SERVER: ${{ secrets.REGISTRY_LOGIN_SERVER }}
        REGISTRY_PASSWORD: ${{ secrets.REGISTRY_PASSWORD }}
        REGISTRY_USERNAME: ${{ secrets.REGISTRY_USERNAME }}
        STAGE_SITE_AKS_NAME: ${{ secrets.STAGE_SITE_AKS_NAME }}
        STAGE_SITE_AKS_RESOURCE_GROUP: ${{ secrets.STAGE_SITE_AKS_RESOURCE_GROUP }}
        PROD_SITE_AKS_NAME: ${{ secrets.PROD_SITE_AKS_NAME }}
        PROD_SITE_AKS_RESOURCE_GROUP: ${{ secrets.PROD_SITE_AKS_RESOURCE_GROUP }}
        HOST_NAME: ${{ secrets.HOST_URL }}
        STAGE_SITE_AZ_SUBSCRIPTION_ID : ${{ secrets.STAGE_SITE_AZ_SUBSCRIPTION_ID }}
        PROD_SITE_AZ_SUBSCRIPTION_ID: ${{ secrets.PROD_SITE_AZ_SUBSCRIPTION_ID}}   
        STG_HOST_NAME: ${{ secrets.STG_HOST_URL }}     

``` 

_More information on [Github Actions and Workflows](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)_



### SPA (Angular) Application
This pipeline will be used by all the Frontend (Single Page Application) Angular applications.