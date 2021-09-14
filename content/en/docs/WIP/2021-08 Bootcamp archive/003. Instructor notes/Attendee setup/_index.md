---
type: docs
title: "Per-Attendee Setup, done by Platform Team"
linkTitle: "Per-Attendee Setup, done by Platform Team"
weight: 010
description: >
  Get things ready for each attendee.
---

## What we need to automate

### Outcome, overall

 - Subscription for OnbeUStudent `bc-subscription`
   - An ACR `bc-acr`

### Outcome, per student
   - User added to the subscription

### Outcome, per team

*Note that, for now, we're assuming one person per team, but that might change later.*

 - A resource group `bc###-rg`
 - An AKS cluster `bc###-cluster-prod` within the resource group
   - Daprized
 - An AKS cluster `bc###-cluster-stage` within the resource group
   - Daprized
 - Service principal that the GitHub pipeline can use (`bc-###-sp`)
   - Provide contributor permission to resource group
   - Provide contributor permission to ACR
   - GitHub secret for the service principal

### Outcome, for the theatermanagement-spa, per team
 - repo named `bc###-theatermanagement-spa`
   - Lock down `main` (Require pull request reviews before merging: true, Include administrators: False)
 - Certain files in the repo
   - `.gitignore`, `package.json`, etc.
 - Workflow file in the `.github` directory.

### The pipeline will be responsible for:
 - In the cluster:
    - A node `bc###-theatermanagement-spa`
    - A node `bc###-theatermanagement-spa-fakeapi`
 
### Outcome, for the theatermanagement-bff, per team
 - repo named `bc###-theatermanagement-bff`
   - Lock down `main` (Require pull request reviews before merging: true, Include administrators: False)
 - Certain files in the repo
   - `.gitignore`, etc.
 - Workflow file in the `.github` directory.

### The pipeline will be responsible for:
 - In the cluster:
    - A node `bc###-theatermanagement-bff`
    - A Dapr sidecar (should be autoinserted because the cluster is Daprized)
    - A node `bc###-theatermanagement-bff-fakeapi`
    - A Dapr sidecar (should be autoinserted because the cluster is Daprized)

### Outcome, for the moviecatalog-svc, per team
 - repo named `bc###-moviecatalog-svc`
   - Lock down `main` (Require pull request reviews before merging: true, Include administrators: False)
 - Certain files in the repo
   - `.gitignore`, etc.
 - Workflow file in the `.github` directory.
 - Azure SQL database `bc###-moviecatalog-database`
   - Connection string made available to the `bc###-moviecatalog-svc` microservice at runtime. (Preferably through Dapr secrets.)

### The pipeline will be responsible for:
 - In the cluster:
    - A node `bc###-moviecatalog-svc`
    - A Dapr sidecar (should be autoinserted because the cluster is Daprized)
    - A node `bc###-moviecatalog-svc-fakeapi` (We probably won't need that, since the movie catalog doesn't have any providers.)
    - A Dapr sidecar (should be autoinserted because the cluster is Daprized)

### Outcome, for the booking-svc, per team

*We don't actually need this right now; provided as an example of a second backend service.*

 - repo named `bc###-booking-svc`
   - Lock down `main` (Require pull request reviews before merging: true, Include administrators: False)
 - Certain files in the repo
   - `.gitignore`, etc.
 - Workflow file in the `.github` directory.
 - In the cluster:
    - A node `bc###-booking-svc`
    - A Dapr sidecar (should be autoinserted because the cluster is Daprized)
 - Azure SQL database `bc###-booking-database`
   - Connection string made available to the `bc###-booking-svc` microservice at runtime. (Preferably through Dapr secrets.)

### TODO: Make sure the consumers know the IDs of their providers