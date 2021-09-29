---
type: docs
title: "REST Naming Conventions"
linkTitle: "Naming Conventions"
weight: 4
description: >
  Remember, your code will be read more times than it is written.
aliases:
  - /link-to/rest-naming
---
<p><a href="/link-to/rest-naming">Permalink</a> to this page</p>

## Rules for all URIs (not just REST)

"[Uniform Resource Identifier (URI): Generic Syntax (RFC 398)](https://pretty-rfc.herokuapp.com/RFC3986)"
dictates which characters are valid in any URI (not just REST).

### Path component

The 
[path component](https://pretty-rfc.herokuapp.com/RFC3986#path)
is the section of the URI that begins with the first slash (/) after the host name
and ends either at the end of the URI or when the optional query section begins with a pound sign (#).

The path component is broken into path segments, separated by the slash (/) character.

The rules for permissable path segment characters are particularly strict.
Certain characters
(colon, slash, question mark, at sign, <i>etc</i>)
have a
[reserved purpose](https://pretty-rfc.herokuapp.com/RFC3986#reserved)
for use in the URI and should not be used within a path segment.
Many other characters would have to be 
[percent-encoded](https://pretty-rfc.herokuapp.com/RFC3986#percent-encoding)
(<i>e.g.</i> the pound sign in `2#steak` encoded to `2%23steak`)
in order to be included in the path, and encoding within the path is discouraged.

Basically, only the 
[unreserved characters](https://pretty-rfc.herokuapp.com/RFC3986#unreserved)
(0-9, a-z, A-Z, hyphen, period, underscore, tilde)
should be used within a path segment.

(We discourage the use of a period anywhere within a path segment because
the path segments `.` and '..' have 
[special meaning](https://pretty-rfc.herokuapp.com/RFC3986#path)
and we wish to avoid confusion.)

## Query component

The optional
[query component](https://pretty-rfc.herokuapp.com/RFC3986#query)
contains non-hierarchical data and is usually
separated into ampersand-delimited key-value pairs 
in which the key and the value are separated by an equal sign.

Unlike the path component (in which percent-encoding is discouraged)
query values within the query component may contain any Unicode
character; the Unicode character will be 
[percent-encoded](https://pretty-rfc.herokuapp.com/RFC3986#percent-encoding).

(Note that percent-encoding of the query key is also possible, but it is
generally recommended to choose keys that do not require encoding.)

## Portions of a REST API URI
<div>
<iframe src="/images/restful-apis/endpoint-diagram/endpoint-diagram.html" style="border:none;position:relative;top:0;left:0;width:100%;height:250px"></iframe>
</div>

## Summary of our recommended ranges for characters in REST path segments and query component

|                                           | Application Context                         | Version                                           | Resource Name                               | ResourceId Name<br>(in OpenAPI spec)          | ResourceId Value                         | Query Key                                                                  | Query Value
|-------------------------------------------|---------------------------------------------|---------------------------------------------------|---------------------------------------------|-----------------------------------------------|------------------------------------------|-----------------------------------------------------------------------|---
| Recommended range of characters           | a-z                                         | 'v' + NUMERIC [+ 'pre']                           | a-z                                         | a-z, A-Z (camelCase)                          | 0-9, A-Z, a-z, hyphen, underscore, tilde | a-z, A-Z (camelCase)                                                  | 0-9, A-Z, a-z, hyphen, period, underscore, tilde
| Examples of Recommended                   | lendinglibrary                              | v1, v2, v2pre                                     | patron, useroption                          | patronId, digitalTokenId                      | 142093449X, 3u-5y_e5~u2-mcpL             | coverType, bookId, startingAfter                                      | 12, true, 1982RedVariant
| Discouraged (although allowed by RFC 398) | 0-9, A-Z, hyphen, period, underscore, tilde | other patterns, hyphen, period, underscore, tilde | 0-9, hyphen, period, underscore, tilde      | 0-9, A-Z, hyphen, period, underscore, tilde   | period                                   | 0-9, hyphen, period, underscore, tilde, characters requiring encoding | enums that use characters requiring encoding
| Examples of Discouraged                   | lending-library, lendingLibrary             | V1, v1.7.9, V1beta                                | Patron, UserOption, userOption, user_option | PatronId, patronID, digital-token-id          | .142093449X                              | cover-type, BookId, starting-after, starting_after, starting%5Fafter  | application/json, application%2Fjson

## Application context

✔️ DO use lower case, no punctuation for application context.

## Version

✔️ DO use "v" + major [+ "pre"] for version.

"v" is lower-case. Version number is MAJOR only; no MINOR or PATH (such as `v1.7.2-rc3`).

If this is preview version of a customer-facing API, append "pre"; <i>e.g.</i> `v1pre`.
APIs that are not client-facing do not have preview versions.

## Resources


### Resource name

✔️ DO use lower case, no punctuation for resource names. Numbers (0-9) are permissible.

## ResourceId

A ResourceId name 
(<i>e.g.</i> `digitalTokenId`)
will not appear in the URI path; it will appear in your
OpenAPI specification.
At run-time, a client will place a ResourceId value
in the position indicated by a ResourceId name.

### ResourceId name

✔️ DO use alphanumeric (0-9,A-Z,a-z) or hyphen (-) or underscore (_) or tilde (~)  for the names of ResourceIds.

So DO NOT use: 
  - `/client/{clientId}/DigitalToken/{digitalTokenId}/Status`

Instead USE:

  - `/client/{clientId}/digitaltoken/{digitalTokenId}/status`

### ResourceId value

✔️ Where you have control over the value that is used in a ResourceId value,
DO stick with character in the range of 0-9, A-Z, a-z, hyphen.

UUIDs are encouraged and should be encoded as 

So DO NOT use: 
  - `/client/{clientId}/DigitalToken/{digitalTokenId}/Status`
  - `/client/Generico/DigitalToken/DkxYNecd3ZsaRYZJ/Status`

Instead USE:

  - `/client/{clientId}/digitaltoken/{digitalTokenId}/status`
  - `/client/Generico/digitaltoken/DkxYNecd3ZsaRYZJ/status`

## Names in query parameters

## Names in JSON body

✔️ DO use camelCase for REST properties and class names.

So DO NOT use snake_case or PascalCase such as:

 - `digital_token` as class name
 - `creation_comment` as query parameter name
 - `issuance_id` as property name
 - `DigitalToken` as class name
 - `CreationComment` as query parameter name
 - `IssuanceId` as property name

Instead USE:

 - `digitalToken`
 - `creationComment`
 - `issuanceId`

Note that this applies to the REST APIs that your code
implements; not to your code. For example,
your C# classes should follow 
[.NET naming conventions](/link-to/dotnet-naming).

✔️ DO treat acronyms and capitalized abbreviations as words when using PascalCase or camelCase

This also applies to both acronyms
(<i>e.g.</i> REST for "Representational State Transfer")
and capitalized abbreviations
(<i>e.g.</i> ID for "identification").

So DO NOT use:

 - `oIDCSettings` as class name
 - `defaultRESTMode` as query parameter name
 - `issuanceID` as property name

Instead USE:

 - `oidcSettings`
 - `defaultRestMode`
 - `issuanceId`
