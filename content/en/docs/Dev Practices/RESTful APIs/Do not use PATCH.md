---
type: docs
title: "Do not use PATCH"
linkTitle: "Do not use PATCH"
weight: 8
description: >
  Use value objects instead.
aliases:
  - /link-to/do-not-use-patch
---
<p><a href="/link-to/do-not-use-patch">Permalink</a> to this page</p>

{{% pageinfo %}}
HTTP PATCH seems simple and many tools generate a a PATCH implementation for you.

But here's why you should delete PATCH from your projects 
and use DDD value objects instead.
{{% /pageinfo %}}


## Why you should not use PATCH

HTTP PATCH seems straight-forward. 
[IETF RFC 5789](https://tools.ietf.org/html/rfc5789) 
says:

> The PATCH method requests that a set of changes described in the
> request entity be applied to the resource identified by the Request-
> URI.

In practice, HTTP PATCH is very difficult to do correctly, both as an API implementer and as an API client.

To do PATCH correctly requires an API endpoint to receive the PATCH
with an `application/merge-patch+json` content type
in JSON Merge Patch format ([IETF RFC 7396](https://tools.ietf.org/html/rfc7396)).

JSON Merge Patch format is difficult to use for both API implementers
and API clients.

{{< alert title="Please. Don't Patch Like An Idiot." >}}
William Durand covered this topic well in an article he now calls
"[Please. Don't Patch Like That.](https://williamdurand.fr/2014/02/14/please-do-not-patch-like-an-idiot/)".

His original title for the article was 
"[Please. Don't Patch Like An Idiot.](https://web.archive.org/web/20140302195240/https://williamdurand.fr/2014/02/14/please-do-not-patch-like-an-idiot/)"
but he decided that came across as rude.

His original title was better.
{{< /alert >}}

## Delete any implementation of PATCH

Even if your tools generate a default implementation of HTTP PATCH for you, you should
delete that implementation and not use PATCH at all, because:

 - The generated implementation probably doesn't use JSON Merge Patch format.

 - Even if the generated implementation does use JSON Merge Patch format
   your API clients are not likely to use it.

## Use value objects instead

Instead of using PATCH, design your APIs to use DDD value objects, which are
[idempotent](https://en.wikipedia.org/wiki/Idempotent#Computer_science_meaning),
which means they are designed **not** to be modified (e.g. by PATCH)
but should instead be replaced (e.g. by PUT).

## What if I really need to use PATCH

If, for some reason, you really need to use PATCH, use a library that supports PATCH correctly
through JSON Merge Patch format.

For an example using ASP.NET 5.0, see 
"[JsonPatch in ASP.NET Core web API](https://docs.microsoft.com/en-us/aspnet/core/web-api/jsonpatch?view=aspnetcore-5.0)".