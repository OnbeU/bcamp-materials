---
type: docs
title: "Parking Lot Topics"
linkTitle: "Parking Lot Topics"
weight: 100
description: >
  Topics we put in the parking lot, then addressed at the end of bootcamp.
---

## Should Pact tests be red first?

## How do we know we’re written enough tests (especially since J.R. says he doesn’t like a quota % for code coverage)?

## Who’s writing the Gherkins?

## How do we know we’re writing the tests correctly?

## Difference between acc tests written in Gherkin format for user story and the ones that could be applied to the actual ms?

## How do we tie a Gherkin in code to a Feature in ADO?

Needs more discussion and planning. Maybe we should just revisit this after we get some more experience.

## What if a Feature in ADO needs to be tied to Gherkins in several microservices?

Needs more discussion and planning. Maybe we should just revisit this after we get some more experience.

## Where will we save documentation?

Needs more discussion and planning.

 - [Day 2](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-16%20Day%202.mp4)
   3:51:20 Documentation in a developer-focused way

## Prod Release process

## What about giving clients keys to a non-production version of our APIs and such?

Can be solved with synthetic users.

## Will we standardize response objects, paths and such for APIs?

Two ways to answer that: Yes, because it's a good thing to be consistent. Second, we don't really care,
since we're doing consumer contracts and not provider contracts and as long as it works.

 - [Day 2](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-16%20Day%202.mp4)
   3:47:42 Whether/how to standardize API calls

## Will we transfer the bootcamp materials into Confluence or something like that?

Yes. (It's on the site where you're reading these words.)

## Should a Pact verification failure prevent the PR from being created?

Needs more discussion.

## Does PO have to be available for every PR approval?

Needs more discussion. Maybe we should just revisit this after we get some more experience.

## Does QA have to be available for every PR approval?

Needs more discussion. Maybe we should just revisit this after we get some more experience.

## Do we plan to have a centralized way of cataloging/tracking all the different microservices (such as Ortelius)?

Yes. Needs more discussion.

## Will we use synthetic behavior for our early-access clients?

Needs more discussion. Maybe we should just revisit this after we get some more experience.

## BFFs keeping data?

On a case-by-case basis, maybe. Probably keep it using Dapr state instead of a database.

## Sidecar to BFF to other service?

Yes.
