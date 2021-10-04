---
type: docs
title: "The Gherkin Connection"
linkTitle: "The Gherkin Connection"
weight: 110
description: >
  Defining the read model as a "Then" in a Gherkin is how we force the system to give the data team what they need.
---

You want be able to run a report that tells you who has booked which concert halls.

Your data team will be listening for domain events like "ConcertHallWasBooked" in order to put that data into the datalake. And it's clear that the concert hall name and the booking data need to appear on that report.

So how does a PO ensure that the event will contain that data?

In an event storming board we'd see that data as the (green) read model that emerges from the event, like so:

![Event storm](/images/the-gherkin-connection/storm.png)

Event storming posties don't have any teeth; they aren't enforced. But automated tests are requirements with teeth, so all we have to do is to turn those posties into an automated test.

Fortunately that's easy, because there's a natural mapping between event storming and Gherkins.

![Event storm](/images/the-gherkin-connection/storm-plus-gherkin.png)

*Et voila!* You have a BDD-based automated test that ensures the name and date are included in the event, and therefor are available for the reports.

For further discussion of the event-storm/BDD connection:
[From PostIt To Test](https://www.slideshare.net/AndrejThiele/from-postit-to-test)
