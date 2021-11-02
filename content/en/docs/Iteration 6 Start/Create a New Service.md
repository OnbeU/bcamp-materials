---
type: docs
title: "Create a New Service"
linkTitle: "Create a New Service"
weight: 3
description: >
  Create a New Service.
---

### Requesting Repository
{{< blocks/section color="warning" >}}
This is a temporary process to request the new application. We will automate this process soon.
{{< /blocks/section >}}
\
\
The infrastructure team will be responsible to provide you the source code repository and base project following the Project naming guidelines.
You will need to send the following email to "pedro.mula@onbe.com".

{{% alert title="Email Subject" color="primary" %}}
New CSharp microservice application request- {Application Name}
{{% /alert %}}
{{% alert title="Email Body" color="primary" %}}
Infrastructure Team,

I am part of Team {Team Name} and would like to request a new cSharp service. Below are the details of my service:

- **Application Name:** _Name of your application as per [application naming](/docs/iteration-6-start/c-sharp-microservice-naming) guidelines Use Pascal case (CompanyAreaType)_

- **Description:** _Description of your service (Min 2 lines)_
- **Repository Name:** _Name of your application as per [application naming](/docs/iteration-6-start/c-sharp-microservice-naming) guidelines Use Kebab case(company-area-type)_
- **Dependent Application(s):** _List of Application Name of services that your service will be dependent on. You'll be able to add more applications later. This will be used to create the fakes._
- **Story Reference:** _Work item number (story) & work item URL for this request_
  {{% /alert %}}

_You will receive an email with the url of your repository once your application and repository is ready to use._

---

### Setup Services (c#) Project
Once you receive the repository information clone to your local and follow the instructions below: 
<a name="csharp-add-container-orchestrator"></a>
- Add Container Orchestrator Support 
  
  Right click your application in visual studio and click **Add Container Orchestrator Support** you need to choose orchestrator type Docker Compose and Target OS as Linux.This will add a docker compose project as well as a docker file to application and fakes.  More information on [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/architecture/containerized-lifecycle/design-develop-containerized-apps/visual-studio-tools-for-docker)
{{% pageinfo color="warning" %}}
Note: You need to add Container Orchestrator support for main application as well for all the fakes in your solution.
In future if you add more fakes remember to add container orchestrator support.
{{% /pageinfo %}}
_More information on  [Docker and Docker Compose](https://docs.docker.com/compose/)_

  ![Visual Studio Add Container Orchestrator Support](/images/ContinuousDeployment/AddContainerOrchestratorSupport.jpg)
  
  

- Add Dapr Support in Docker Compose:
  
  Since we will be using dapr (Distributed application runtime) [_More information on [Dapr](https://docs.dapr.io/)_] to build our event-driven and resilient distributed applications, We need to add dapr service (Side car) in docker compose for main application and all fakes. For each of the fake and the main application add the following lines in ```docker-compose.yml``` file: 
   
```
 {Application Name}-dapr:
     image: "daprio/daprd:latest"
     command: [ "./daprd", "-app-id", "{Repository Name of Main/Fake's application}", "-app-port", "80" ]
     depends_on:
        - {Application Name}
     network_mode: "service:{Application Name}" 

  ```
  
  Example Docker Compose File

```
version: '3.4'

services:
  OmClientApiBff:
    image: ${DOCKER_REGISTRY-}OmClientApiBff
    build:
      context: .
      dockerfile: src/OmClientApiBff/Dockerfile
  OmClientApiBff-dapr:
     image: "daprio/daprd:latest"
     command: [ "./daprd", "-app-id", "om-clientapi-bff", "-app-port", "80" ]
     depends_on:
        - OmClientApiBff
     network_mode: "service:OmClientApiBff" 

  OmOrderManagementHistorySvc.fake:
    image: ${DOCKER_REGISTRY-}OmOrderManagementHistorySvc
    build:
      context: .
      dockerfile: fake/OmOrderManagementHistorySvc.Fake/Dockerfile
  OmOrderManagementHistorySvc-dapr:
     image: "daprio/daprd:latest"
     command: [ "./daprd", "-app-id", "om-ordermanagementhistory-svc", "-app-port", "80" ]
     depends_on:
        - OmOrderManagementHistorySvc.fake
     network_mode: "service:OmOrderManagementHistorySvc.fake" 
```

- Add Health Check and Health Check Route.<a name="csharp-add-healthcheck"></a>
  
  You also need to add health check to your application. The health check needs to be configured for <font color="red">**```/hc```**</font> route. 
_More information on [Health checks in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/health-checks?view=aspnetcore-5.0)_

```
 public class Startup
{
    public Startup(IConfiguration configuration)
    {
            Configuration = configuration;
    }
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddHealthChecks();   <-------------
    }

    public void Configure(IApplicationBuilder app)
    {
        app.UseRouting();

        app.UseEndpoints(endpoints =>
        {
            endpoints.MapControllers();
            endpoints.MapHealthChecks("/hc");  <------------
        });
    }
}
``` 
- Pact Test project changes.<a name="csharp-pacttestprojectchanges"></a>

  We are using PACTNET library for our Pact contract testing. Pactnet library needs different packages based on your operating system. We need to update pact provider and consumer test projects to add conditional packages. Add/Update the pact test csproj files with the following content.

```
 <PackageReference Include="PactNet.Linux.x64" Version="3.0.0" Condition="$([MSBuild]::IsOsPlatform('Linux'))" />
 <PackageReference Include="PactNet.Windows" Version="3.0.0" Condition="$([MSBuild]::IsOsPlatform('Windows'))" />

``` 

