---
type: docs
title: "c# Microservice Naming Convention"
linkTitle: "c# Microservice Naming Convention"
weight: 1
description: >
  c# Microservice Naming.
---

This document describes the rule and recommendations for naming different components of your microservice like repository, application, project, class etc. in .NET using C# as a language. The main purpose is to define the general guidelines to enforce consistent naming across services which can be useful for each team to quickly understand the use of each component.

## Naming Conventions

There are various type of naming convention generally used.

- Pascal Convention – First character of all word is in upper case and other characters are in lower case.
  Example: OnbeOrderValidationSvc, OnbeKnowYourCustomerBff
- Camel Case Convention – The first character of all words, except the first word, is upper case and other characters are lower case.
  Example: orderValidation, physicalCard
- Kebab case - Naming convention where a developer replaces the spaces between words with a dash.
  Example: onbe-knowyourcustomer-svc, ordering-svc
- Snake case: Naming convention where a developer replaces the spaces between words with an underscore.
  Example: Physical_Card, Client_Id

| Module                 |                                                        Description                                                         |                               Example |
| ---------------------- | :------------------------------------------------------------------------------------------------------------------------: | ------------------------------------: |
| Source Code Repository |                                           Use Kebab case<br>(company-area-type)                                            |             onbe-knowyourcustomer-svc |
| Application Name       |                                           Use Pascal case <br>(CompanyAreaType)                                            |               OnbeKnowYourCustomerSvc |
| Solution Name          |                                           Use Pascal case <br>(CompanyAreaType)                                            |               OnbeKnowYourCustomerSvc |
| Project Name           |                                           Use Pascal case <br>(CompanyAreaType)                                            |               OnbeKnowYourCustomerSvc |
| c# namespace           |                                           Use Pascal case <br>(CompanyAreaType)                                            |               OnbeKnowYourCustomerSvc |
| Test Project Name      |                                    Use Pascal case <br>(CompanyAreaType.TestType.Tests)                                    |    OnbeKnowYourCustomerSvc.Unit.Tests |
| Pact Pacticipant Id    |                                           Use Kebab case<br>(company-area-type)                                            |             onbe-knowyourcustomer-svc |
| Dapr app_id            |                                           Use Kebab case<br>(company-area-type)                                            |             onbe-knowyourcustomer-svc |
| Class                  |                                                      Use Pascal case                                                       |                          OrderService |
| Filename               |                                   Filename should match with class name i.e. Pascal case                                   |                       OrderService.cs |
| Method                 |                                                      Use Pascal case                                                       |                         ValidateOrder |
| Interface              |                                             Use Prefix “I” with Pascal Casing                                              |                         IOrderService |
| Local Variables        |                       Use Meaningful, descriptive words to name variables. Do not use abbreviations                        |          string clientName int amount |
| Member Variables       | Member variables must be prefix with underscore (\_) so that they can be identified by other local variables and constants | private IOrderService \_orderService; |
| Boolean variables      |                                             Prefix Boolean variables with “is”                                             |               private bool \_isActive |

\
\
\
![Naming Conventions for Microservices Projects](/images/bootcamp-slides/microservices-bootcamp/Slide45.PNG)
