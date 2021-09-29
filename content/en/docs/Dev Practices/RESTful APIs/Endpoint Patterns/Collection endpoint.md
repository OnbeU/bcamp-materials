---
type: docs
title: "Collection Endpoint Pattern"
linkTitle: "Collection Endpoint Pattern"
weight: 8
description: >
  The HTTP pattern to follow for a collection endpoint.
aliases:
  - /link-to/types-of-rest-endpoints-collection
---
<p><a href="/link-to/types-of-rest-endpoints-collection">Permalink</a> to this page</p>

## Collection endpoint

A 
[collection endpoint](../types-of-rest-endpoints/#collection-endpoint)
 may be:

 - An aggregate, in which case the collection always exists and is not deleted.
 - A value object, in which case the collection can be created and deleted.

For example, this API has endpoints for a `users` aggregate and an `accounts` value object:

    /myapi/v1/users
    /myapi/v1/users/{user-id}/accounts

## To DELETE or not DELETE

The type of collection determines whether to not to handle DELETE.

| Type of collection          | Implement DELETE?
|-----------------------------|---
| Aggregate                   | No; aggregate collections are never deleted.
| Value object                | Yes; DELETE should set the parent's value object to null.

## Sync vs Async

Both POST and DELETE may be handled two ways: synchronously or asynchronously.

If either of these is asynchronous, a 
[status resource](../types-of-rest-endpoints/#status-resource-endpoint)
is needed to provide the status of the asynchronous operation.

| Handling                    | POST status       | POST Location header                  | DELETE status        | DELETE response body
|-----------------------------|-------------------|---------------------------------------|----------------------|---
| Synchronous handling        | `201 (Created)`  | Points to the newly created resource. | `204 (No Content)` | (empty)
| Asynchronous handling       | `202 (Accepted)` | Points to a status resource.          | `202 (Accepted)`   | (empty)

Note that some implementers recommend that DELETE should return a `200 (OK)` with the deleted entity
contained in the response body. We decided against that approach because:

 - Doing so would make DELETE no longer idempotent (since a repeat of the DELETE might not have the original resource available to it).
 - It's a waste of processing power.
 - A client could achieve nearly the same result by calling GET prior to DELETE.

## Expected HTTP status codes

The HTTP status codes that should be expected for 
a collection endpoint (*e.g.* `/myapi/v1/users` or `/myapi/v1/users/{user-id}/accounts`) are:

<table>
<thead>
  <tr>
    <th>Condition</th>
    <th>POST</th>
    <th>GET</th>
    <th>DELETE</th>
  </tr>
</thead>
<tbody>
  <tr>
    <!-- Condition   --><td>In all cases</td>
    <!-- POST        --><td>Sync POST: 201 (Created)<br/>Async POST: 202 (Accepted)<br/>400 (Bad Request)</td>
    <!-- GET         --><td>200 (OK)</br>400 (Bad Request)</td>
    <!-- DELETE      --><td>Sync DELETE: 204 (No Content)<br/>Async DELETE: 202 (Accepted)<br/>400 (Bad Request)</td>
  </tr>
  <tr>
    <!-- Condition   --><td>If method has authorization</td>
    <!-- POST        --><td>403 (Forbidden)</td>
    <!-- GET         --><td>403 (Forbidden)</td>
    <!-- DELETE      --><td>403 (Forbidden)</td>
  </tr>
</tbody>
</table>

## HTTP methods that do not/might not apply to collections

| Method   | Reason it doesn't apply
|----------|---
| GET      | GET only applies if the collection is enumerable. If the collection is not enumerable, then the collection endpoint should not implement GET. In this case the client must know the member's IDs without enumerating them.
| PUT      | PUT modifies a resource and is only applied to a [resource endpoint](../types-of-rest-endpoints/#resource-endpoint), never to a collection.
| DELETE   | DELETE only applies if the collection is a value object. If the collection is an aggregate, it cannnot be deleted.