---
type: docs
title: "Endpoint Types and Microsoft EF Core API Projects"
linkTitle: "Endpoint Types and Microsoft EF Core API Projects"
weight: 8
description: >
  Mapping endpoint types to a Controller created by Microsoft's wizard.
aliases:
  - /link-to/endpoints-and-ms-ef-core-api-projects
---
<p><a href="/link-to/endpoints-and-ms-ef-core-api-projects">Permalink</a> to this page</p>

{{% pageinfo %}}
Work in progress.
{{% /pageinfo %}}

## Creating an API with the wizard

<img src="/images/restful-apis/endpoint-patterns/visual-studio-api-ef-controller-wizard.jpg" alt="Visual Studio API EF Controller Wizrd"/>

| Controller     | DDD type     | Original endpoint   | Endpoint type | New endpoint
|----------------|--------------|---------------------|--------------|---
| FoosController | Aggregate    | GET: api/Foos       | Collection    | Aggregate    | (same)
|                |              | GET: api/Foos/5     | Resource      | Entity       | (same)
|                |              | PUT: api/Foos/5     | Resource      | Entity       | (same)
|                | POST: api/Foos      | Collection    | Aggregate    | (same)
|                | DELETE: api/Foos/5  | Resource      | Entity       | (same)
|                |                     |               |              | GET: api/Foos/5/Fvs
| FvsController  | GET: api/Fvs        | Collection    | (removed)    | (removed)
|                | GET: api/Fvs/6      | Resource      | Entity       | GET: api/Foos/5/Fvo
|                | PUT: api/Fvs/6      | Resource      | Entity       | GET: api/Foos/5/Fvo
|                | POST: api/Fvs       | Collection    | Aggregate    | POST: api/Foos/5/Fvo
|                | DELETE: api/Fvs/6   | Resource      | Entity       | DELETE: api/Foos/5/Fvo
| BarsController | GET: api/Bars       | Collection    | Entity       | api/Foos/5/Bars
|                | GET: api/Bars/7     | Resource      | Entity       | api/Foos/5/Bars/7
|                | PUT: api/Bars/7     | Resource      | Entity       | api/Foos/5/Bars/7
|                | POST: api/Bars      | Collection    | Entity       | api/Foos/5/Bars
|                | DELETE: api/Bars/7  | Resource      | Value object | api/Foos/5/Bars/7
| BvsController  | GET: api/Bvs        | Collection    | Aggregate    | (same)
|                | GET: api/Bvs/8      | Resource      | Entity       | (same)
|                | PUT: api/Bvs/8      | Resource      | Entity       | (same)
|                | POST: api/Fvs       | Collection    | Aggregate    | (same)
|                | DELETE: api/Bvs/8   | Resource      | Entity       | (same)
|                |                     |               |              | DELETE: api/Foos/5/Bars
|                |                     |               |              | DELETE: api/Foos/5/Bars
|                |                     |               |              | DELETE: api/Foos/5/Bars
|                |                     |               |              | DELETE: api/Foos/5/Bars
|                |                     |               |              | DELETE: api/Foos/5/Bars
|                |                     |               |              | DELETE: api/Foos/5/Bars
|                |                     |               |              | DELETE: api/Foos/5/Bars
|                |                     |               |              | DELETE: api/Foos/5/Bars
|                |                     |               |              | DELETE: api/Foos/5/Bars

## GetFoos()

    // GET: api/WeatherForecasts
    [HttpGet]
    public async Task<ActionResult<IEnumerable<WeatherForecast>>> GetWeatherForecasts()
