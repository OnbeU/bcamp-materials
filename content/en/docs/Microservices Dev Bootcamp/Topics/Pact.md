---
type: docs
title: "Pact and Consumer-Defined Contracts"
linkTitle: "Pact and Consumer-Defined Contracts"
weight: 010
description: >
  Consumer-defined contracts prevent us from deploying breaking API changes to our internal services.
---

## Important links

 - Pact at https://pact.io
 - Pact Introduction video at https://docs.pact.io/#watch-a-video

## Watch the recording

 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   1:39:22 How Pact fits into the pipeline
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   1:47:24 Provider Contract vs Consumer Contracts
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   1:49:14 Technology comparisons: OpenAPI, AsyncAPI, Protobuf, Aero, Git, Pact
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   1:56:27 Deploying a consumer
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   1:59:05 How might the provider fail?
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   2:00:06 If your provider has a new endpoint, do you need a new contract? (Answer: No; the contract only changes if the consumer's needs change.)
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   2:01:20-2:06:13 Pact and Dapr Demo
     - The high level architecture
     - How does Pact work?
     - We created a Java app that uses Dapr pubsub to receive the TheaterCreated event.
     - The Java app has a unit test, which tests against the provider mock
     - The Java app created the contract.
     - The Java app published the contract to the Pact Broker.
     - At this point the Java app can’t be deployed because the contract isn’t verified.
     - We created a C# app that uses Dapr to publish the TheaterCreated event.
     - The C# app has a unit test to verify the contract from the Pact Broker.
     - Initially, the C# test failed because the contract wanted a lower-case t, not an upper-case T.
     - So we changed the C# app to fulfill the contract.
     - Now the C# app tests pass.
     - And now the Pact Broker reports that the contract is verified.
     - So now deployment may proceed. The pipeline ensure that the provider is in place in Production before it allows the consumer to deploy.
     - All of this has been deployed to an AKS cluster.
     - We are able to use a Redis pubsub or an MQTT pubsub. Dapr lets us switch.
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   2:06:13 Quick summary of Pact
     - TODO: Break this section into bullet points
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   2:08:10-2:12:37 What if two consumers have conflicting contracts? If they really conflict (because it's okay if they simply ask for non-conflicting properties), the answer is: The teams talk.
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   2:15:52 From an agile perspective, will we adjust when a need for contract changes come up in the middle of a sprint? Answer: We'd better be able to (but of course there are always priorities to consider).
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   2:20:00 Pending and Work-In-Progress pacts. *Note that this discussion incorrectly says that pending pacts and WIP pacts are the same thing, but [they are slightly different](https://docs.pact.io/pact_broker/advanced_topics/wip_pacts/).*
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   2:23:18 How does the Pact get generated?
      - Forget about Pact for a moment and let's just test the consumer's client code.
      - Now bring Pact back into it. The mock that we created to test the consumer's client code contains everything that the contract needs.
      - So the consumer simply uses the Pact library to provide its mock, then adds a few lines of code to generate the Pact.
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   2:35:15 Pact makes teams talk to each other.
 - [Day 3](https://onbeco.sharepoint.com/sites/Technology/Shared%20Documents/General/Architecture/Presentations/Onbe%20Microservices%20Bootcamp/Recorded%20Sessions/Bootcamp%202021-09-17%20Day%203.mp4)
   2:38:47 Pact Broker's network diagram

## Slides

![Provider Contract vs Consumer Contracts](/images/bootcamp-slides/microservices-bootcamp/Slide172.PNG)

![Technology comparisons](/images/bootcamp-slides/microservices-bootcamp/Slide174.PNG)

![Local Development/Stage Site vs. Production](/images/bootcamp-slides/microservices-bootcamp/Slide18.PNG)

![Deploying a consumer](/images/bootcamp-slides/microservices-bootcamp/Slide173.PNG)

![Pact and Dapr demo](/images/bootcamp-slides/pact-dapr-demo/Slide1.PNG)

![The high level architecture](/images/bootcamp-slides/pact-dapr-demo/Slide2.PNG)

![How does Pact work?](/images/bootcamp-slides/pact-dapr-demo/Slide3.PNG)

![We created a Java app that uses Dapr pubsub to receive the TheaterCreated event.](/images/bootcamp-slides/pact-dapr-demo/Slide4.PNG)

![The Java app has a unit test, which tests against the provider mock](/images/bootcamp-slides/pact-dapr-demo/Slide5.PNG)

![The Java app created the contract](/images/bootcamp-slides/pact-dapr-demo/Slide6.PNG)

![The Java app published the contract to the Pact Broker.](/images/bootcamp-slides/pact-dapr-demo/Slide7.PNG)

![At this point the Java app can’t be deployed because the contract isn’t verified.](/images/bootcamp-slides/pact-dapr-demo/Slide8.PNG)

![We created a C# app that uses Dapr to publish the TheaterCreated event.](/images/bootcamp-slides/pact-dapr-demo/Slide9.PNG)

![The C# app has a unit test to verify the contract from the Pact Broker.](/images/bootcamp-slides/pact-dapr-demo/Slide10.PNG)

![Initially, the C# test failed because the contract wanted a lower-case t, not an upper-case T.](/images/bootcamp-slides/pact-dapr-demo/Slide11.PNG)

![So we changed the C# app to fulfill the contract.](/images/bootcamp-slides/pact-dapr-demo/Slide12.PNG)

![Now the C# app tests pass.](/images/bootcamp-slides/pact-dapr-demo/Slide13.PNG)

![And now the Pact Broker reports that the contract is verified.](/images/bootcamp-slides/pact-dapr-demo/Slide14.PNG)

![So now deployment may proceed. The pipeline ensure that the provider is in place in Production before it allows the consumer to deploy.](/images/bootcamp-slides/pact-dapr-demo/Slide15.PNG)

![All of this has been deployed to an AKS cluster.](/images/bootcamp-slides/pact-dapr-demo/Slide16.PNG)

![And now the Pact Broker reports that the contract is verified.](/images/bootcamp-slides/pact-dapr-demo/Slide16.PNG)

![We are able to use a Redis pubsub or an MQTT pubsub. Dapr lets us switch.](/images/bootcamp-slides/pact-dapr-demo/Slide17.PNG)

![Gates Before Deployment](/images/bootcamp-slides/microservices-bootcamp/Slide55.PNG)
