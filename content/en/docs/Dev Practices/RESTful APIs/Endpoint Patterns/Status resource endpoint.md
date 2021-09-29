---
type: docs
title: "Status Resource Endpoint Pattern"
linkTitle: "Status Resource Endpoint Pattern"
weight: 8
description: >
  The HTTP pattern to follow for a status resource endpoint.
aliases:
  - /link-to/types-of-rest-endpoints-status-resource
---
<p><a href="/link-to/types-of-rest-endpoints-status-resource">Permalink</a> to this page</p>

## Sync vs Async

A
[collection endpoint](../collection-endpoint)'s
POST and DELETE may be handled two ways: synchronously or asynchronously.

If either of these is asynchronous, a 
[status resource](../types-of-rest-endpoints/#status-resource-endpoint)
is needed to provide the status of the asynchronous operation.

## Expected HTTP status codes

The HTTP status codes that should be expected for 
a status resource endpoint (*e.g.* `/myapi/v1/users/postqueue/9876`) are:

<table>
<thead>
  <tr>
    <th>Condition</th>
    <th>GET</th>
    <th>DELETE</th>
  </tr>
</thead>
<tbody>
  <tr>
    <!-- Condition   --><td>In all cases</td>
    <!-- GET         --><td>200 (OK)<br/>303 (See other)<br/>404 (Not Found)</td>
    <!-- DELETE      --><td></td>
  </tr>
  <tr>
    <!-- Condition   --><td>If the pending operation can be cancelled</td>
    <!-- GET         --><td></td>
    <!-- DELETE      --><td>204 (No Content)<br/>404 (Not Found)</td>
  </tr>
  <tr>
    <!-- Condition   --><td>If method has authorization</td>
    <!-- GET         --><td>403 (Forbidden)</td>
    <!-- DELETE      --><td>403 (Forbidden)</td>
  </tr>
</tbody>
</table>

## HTTP methods that do not/might not apply to status resource endpoints

| Method   | Reason it doesn't apply
|----------|---
| POST     | A status resource is created by the server and may not be created by an API client.
| PUT      | PUT modifies a resource and is only applied to a [resource endpoint](../types-of-rest-endpoints/#resource-endpoint), never to a status resource endpoint.
| DELETE   | DELETE only applies if the operation can be cancelled.