---
type: docs
title: "Types of REST endpoints"
linkTitle: "Types of REST endpoints"
weight: 3
description: >
  The types of REST endpoints: Collection, resource, status resource and (yuck!) verb.
aliases:
  - /link-to/types-of-rest-endpoints
---
<p><a href="/link-to/types-of-rest-endpoints">Permalink</a> to this page</p>

## Example endpoints

| Endpoint                                                 | Type             | Notes
|----------------------------------------------------------|------------------|--
| `/myapi/v1/users`                                       | Collection       | `users` is an aggregate
| `/myapi/v1/users/postqueue/9876`                      | Status resource  | Provides status of the asynchronous POST operation of `users`
| `/myapi/v1/users/123`                                  | Resource         |
| `/myapi/v1/users/123/accounts`                        | Collection        | `accounts` is the `user` resource's value object
| `/myapi/v1/users/123/accounts/456`                    | Resource         |
| `/myapi/v1/users/123/accounts/456/age`                | Resource         | `age` is the `account` resource's value object
| `/myapi/v1/users/123/accounts/456/updateandapprove`  | Verb             | `updateandapprove` is a verb performed against the `account` resource

## The four types of REST endpoints

### Collection endpoint

A collection endpoint represents a collection of resources. It is either an aggregate or a value object.

If you are writing this type of endpoint, follow the
[collection endpoint pattern](../collection-endpoint).

Example request:

    POST /myapi/v1/users
    Content-Type: application/json
    Accept: application/json

    {
        "name": "Joe Smith",
        ...
    }

Example response (if the POST handling is asynchronous):

    HTTP/1.1 202 (Accepted)
    Location /myapi/v1/users/postqueue/9876

Example request:

    POST /myapi/v1/users/123/accounts
    Content-Type: application/json
    Accept: application/json

    {
        "accounttype": "checking",
        ...
    }

Example response (if the POST handling is synchronous):

    HTTP/1.1 201 Created
    Location: /myapi/v1/users/123/accounts/456
    Content-Type: application/json

    {
        "id" : 456,
        "accounttype": "checking",
        ...
    }

### Resource endpoint

A resource endpoint represents an individual resource.

That resource is either an entity or an entity's value object. In either case it is identified by the entity's ID.

If you are writing this type of endpoint, follow the
[resource endpoint pattern](../resource-endpoint).

Example request:

    GET /myapi/v1/users/123
    Content-Type: application/json
    Accept: application/json

Example response:

    HTTP/1.1 200 (OK)
    Content-Type: application/json

    {
        "id" : 123,
        "name": "Joe Smith",
        ...
    }

### Status resource endpoint

A collection's POST or DELETE operation might be either synchronous or asynchronous.

If either of these is asynchronous, a status resource is needed to provide the status of the asynchronous operation.

If you are writing this type of endpoint, follow the
[status resource pattern](../types-of-rest-endpoints/#status-resource-endpoint).

Example request:

    GET /myapi/v1/users/postqueue/9876

Example response (if further waiting is necessary):

    HTTP/1.1 200 (OK)
    Location: /myapi/v1/users/postqueue/9876
    Retry-After: 10

Example response (if resource is available):

    HTTP/1.1 303 (See other)
    Location: /myapi/v1/users/123

### Verb endpoint

You should really avoid this approach because it goes against REST principles. There are many ways to get around doing this.

But if you really must write a verb endpoint, follow the
[verb endpoint pattern](../types-of-rest-endpoints/#verb-endpoint).

Example request:

    POST /myapi/v1/users/123/accounts/456/updateandapprove

Example response:

     HTTP/1.1 200 (OK)