---
type: docs
title: "Idempotency"
linkTitle: "Idempotency"
weight: 4
description: >
  What does your user need to understand about your project in order to use it - or potentially contribute to it? 
aliases:
  - /link-to/endpoint-patterns-idempotency
---
<p><a href="/link-to/endpoint-patterns-idempotency">Permalink</a> to this page</p>

{{% pageinfo %}}
This is a placeholder page that shows you how to use this template site.
{{% /pageinfo %}}

## (What to do with this?)
By convention, some methods are considered 
[safe](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Safe_methods)
and are therefore
[nullipotent](https://en.wiktionary.org/wiki/nullipotent);
in other words they are not expected to change the resource and
should have no side effects.

Some methods are considered 
[idempotent](https://en.wikipedia.org/wiki/Idempotence#Computer_science_meaning)
and are expected to change the resource.

API methods should never return `401 (Unauthorized)`. Authorization should have occurred prior to the method being invoked.

| HTTP method | Authorization                    | Resource  | Request validity            | Change to resource | First time returns           | Subsequent time returns
|-------------|----------------------------------|-----------|-----------------------------|--------------------|------------------------------|---
| GET         | Blocked by owned-resource policy | (any)     | (any)                       | No change          | 403 (Forbidden)              | Same as first time (nullipotent)
| GET         | Passed                           | (any)     | Invalid                     | No change          | 400 (Bad Request)            | Same as first time (nullipotent)
| GET         | Passed                           | Not exist | Valid                       | No change          | 404 (Not Found)              | Same as first time (nullipotent)
| GET         | Passed                           | Exist     | Valid                       | No change          | 200 (OK) with resource state | Same as first time (nullipotent)

Example:

Abe is logged into the DiiConsumer.Angular app with the authenticated **sub*** of `"ABE00000-0000-0000-0000-000000000000"`.

Abe has previously obtained a ticket with `ticket-id` of `78127`. That ticket is associated with his **sub***.

The app makes an API call, passing `"sub": "ABE00000-0000-0000-0000-000000000000"` in the JWT, to:

    GET /consumer_v1/tickets/78127

Because the ticket exists and the JWT's **sub** matches the ticket's `consumeruser-id`,
the API call returns `200 (OK)` and the ticket's information.

However, if Betsy is logged in and makes the same `GET` call for `ticket-id` of `78127`
with `"sub": "BE751E00-0000-0000-0000-000000000000"` in her JWT 
she will receive `404 (Not Found)` because she has no right to know whether the ticket exists
(which, in this case, it does).

Example:

Abe is logged into the DiiConsumer.Angular app with the authenticated **sub*** of `"ABE00000-0000-0000-0000-000000000000"`.

Abe has previously obtained a ticket with `ticket-id` of `78127`. That ticket is associated with his **sub***.

The app makes an **incorrectly-formed** API call, passing `"sub": "ABE00000-0000-0000-0000-000000000000"` in the JWT, to:

    GET /consumer_v1/tickets/byrange?firstMonth=202211&lastMonth=8

Although the ticket exists and the JWT's **sub** matches the ticket's `consumeruser-id`,
the API is incorrectly formed (since `8` isn't a valid `month-id` )
so the API call returns `400 (Bad Request)`.

| HTTP method | Creation | Client rights    | Valid request?  | Change to resource | First time returns                  | Subsequent time returns
|-------------|----------|------------------|-----------------|--------------------|-----------------|-------------------------------------|----------------|------------------
| POST        | Sync     | Right to read    | Is valid        | Created            | 201 (Created) with resource state   | Non-idempotent
| POST        | Async    | Right to read    | Is valid        | No change yet      | 202 (Accepted) with ???             | Non-idempotent
| POST        | (any)    | No right to read | (any)           | No change          | 403 (Forbidden)                     | Non-idempotent

| HTTP method                  | Resource  | Valid request?  | Change resource | First time returns                  | Subsequent time returns
|------------------------------|-----------|-----------------|-----------------|-------------------------------------|---
| PUT                          | Not exist | n/a             | No change       | Expected                            | Idempotent
