---
title: Write a Koppeltaal Connector
category: How-to
order: 1
---

# How to write a Koppeltaal connector

## About this guide
This guide assumes the reader knows Koppeltaal terminology. One source for that kind of knowledge is the [Technical Design Document]. This document is explicitly not technical, but rather a descriptive/explanatory guide on how to write a connector. This guide tries do that by answering questions developers will likely have.

## What is a Koppeltaal connector?
Every application that communicates with the Koppeltaal server will need code to do this. A Koppeltaal "connector" provides reusable code in the form of a library that provides this functionality (figure 1). These connectors are open source and hosted on Github.com.

![figure 1]
**Figure 1**. _Every application communicates with the Koppeltaal server through a connector that encapsulates most of the complexity._

### Existing connectors, adding functionality, creating a new connector
You may be able to use an existing connector in the language of your choice that functionally covers all needs you have. If your application needs functionality in an existing connector that has not been implemented, feel free to contribute to the connector project and create a pull request at the repository at the [Koppeltaal organization on GitHub]. When no connector exists in the programming language that you need, you can write one yourself. 

Because these connectors are open source it is important that the source code is clear and readable for other developers that may need to debug or want to add features.

Existing connectors can be found at the [Koppeltaal organization on GitHub]. If you want to contribute a connector a new repository can be created there as well.

In this document we'll describe the process for starting a connector from scratch. When extending an existing connector some steps can (obviously) be skipped.

## Before you begin
- Which FHIR resources need to be supported?
- Is there a FHIR model library for programming language X?
- Determine which version of Koppeltaal to support
- Study the sample requests to the Koppeltaal server

### Which FHIR resources to support
The needs of the application(s) that use the connector will determine which FHIR resources the connector needs to support. It is not necessary for a connector to be able to handle all `Message` types. In the administration console on the Koppeltaal server an application can be subscribed to specific message types.

### FHIR model libraries
HL7.org provides so called _Reference Implementations_ for a small number of programming languages. These are basic libraries that contain FHIR resource models and validation schemas that can be used in writing a connector: [DSTU1] / [current version].

### Which Koppeltaal versions to support
The first release of the connector should support the current version of Koppeltaal. Subsequent releases of the connector should still support older implementations of Koppeltaal. The current version is the [latest release of the Koppeltaal server].

Example: the current version of Koppeltaal is 1.2.1. When we write a new connector it should support that version of Koppeltaal. Any subsequent releases of this new connector should support 1.2.1 and up.

### Sample requests
You can find examples of messages in this [SoapUI project]. The [description of the SoapUI project] contains more in-depth information about how to use this project. We recommend using these examples to debug your own requests.

## Connector responsibilities
A Koppeltaal connector communicates directly with the Koppeltaal Server REST interface (using JSON or XML), while exposing a simple API (e.g., a [Facade]) to the application. Koppeltaal specific complexity should be handled by the connector - e.g., composing a message that conforms to Koppeltaal ontology.

Which functionalities a connector should provide depends on the applications that use it. However, we think there is a set of basic functionalities that each connector should support.

- Retrieve the `Conformance Statement`
- Send/retrieve `Messages` to/from a domain
    - Create a Message bundle with FHIR Resources (send)
    - Extract FHIR Resources from the Message bundle (receive)
    - Update the _ProcessingStatus_ of a Message
- Retrieve and update `Activity Definitions`
- "Launch" a user to a specific application

A connector can also support the following functionality:

- Implement support for _NewMessage_ push notifications, using [SignalR]
- Using the `Storage Service` as data persistence utility

The connector will have most of this functionality simply by sending/retrieving Messages according to Koppeltaal specifications.

### Basic features

#### The Conformance Statement
A `Conformance Statement` is the set of capabilities of a FHIR Server. The conformance statement of the Koppeltaal Server contains information required for the OAuth2 implementation of [the single sign on]. The conformance statement also contains a number of important endpoints that are needed for certain actions. This statement can be requested via _${koppeltaal.server.url}/FHIR/Koppeltaal/metadata_ (e.g. http://edgekoppeltaal.vhscloud.nl/FHIR/Koppeltaal/metadata).
The connector must extract these endpoints from the conformance statement and use them for other actions. For instance, to request authorization for the launch of a game, the authorization endpoint must be read from the statement.

#### Koppeltaal Messages
Communication with the Koppeltaal server consists largely of exchanging `Messages`. A single Koppeltaal message consists of a "bundle" of `FHIR Resources`. More information on the [FHIR resources] used in Koppeltaal.

The first resource in the bundle is the `MessageHeader`, which should always be present. The header contains important information about the content of the message like the [message event types]. A connector can use this information to convert the resources in the bundle so an application can use them - e.g. an object that holds the values that are relevant to an application.

_Note_: When building an outgoing message make sure that the MessageHeader is the first Resource of the bundle.

##### Message authentication
A connector should be able to exchange `Messages` using `Basic Authentication` as well as an `OAuth2 Bearer Token`. Using a `Bearer Token` implicitly only requests information for the user bound to the `Bearer Token`. Requesting patient-specific `Messages` with `Basic Authentication` requires a `patient` parameter.

#### Message ProcessingStatus
When [handling messages] it is important that the `ProcessingStatus` of a message is changed. That way the Koppeltaal server knows a message has been handled. A connector should also be able to mark a message as `Failed` and provide an exception description to go along with this state.

#### ActivityDefinitions
`ActivityDefinitions` are treated somewhat different than the rest of the FHIR resources. They are of resource type `Other` and the content is as such not defined in the FHIR spec. In Koppeltaal, they should be created or updated without the use of Message resource bundles. To create an ActivityDefinition send a simple HTTP POST request containing the [ActivityDefinition] in the request body.

Updating ActivityDefinitions ??

#### "Launching" Users To An Application 
Koppeltaal provides a [Web Launch Sequence]. Functionally this is like a single sign on which also navigates to a specific location in the target system. The Web Launch Sequence allows users to login to an application and launch a `Resource`. The launch allows users to work on a `CarePlan(Sub)Activity`.

### Additional features

#### Storage Service
More information following. [Storage service]

#### Push Notifications: (since 1.2.1)

For applications that require real-time updates from Koppeltaal, it is advised **not** to use long-polling. Koppeltaal supports pushing notifications to applications when a new Message is available. Since Koppeltaal v1.2.1 there are two ways of using the push mechanism. Both options are preferred over polling to reduce server load on both sides:

- Implement [SignalR] with subscription mechanism for the connector
- Configure a REST webhook for an application exposing a REST endpoint

##### SignalR (connector feature)
When available, use a SignalR library to aid in creating a _HubConnection_ to the Koppeltaal server and subscribe to the `NewMessage` event.
The connector then triggers the internal [GetNextNewAndClaim] action to fetch the new message(s).

##### REST webhook (application feature)
The application that connects to the Koppeltaal domain exposes a RESTful endpoint, a webhook. The URL for this webhook can be configured in the _admin console of the application_. The Koppeltaal server makes an HTTP request to the URI configured for the webhook.
The application then triggers the [GetNextNewAndClaim] action in the connector to fetch the new message(s).

!! Let's add a screenshot of where to configure that. Or a Click > Click > Click path on how to get there.

## Connector quality assessment
When you create a Koppeltaal connector it is not automatically accepted as an official connector, it will be vetted by Koppeltaal first.
The code will be assessed by Koppeltaal on a number of matters, such as:

- Code clarity and readability
- Unit Test availability
- Technical documentation

?? Who or what do we mean with "Koppeltaal" up here? Stichting Koppeltaal? Who specifically then? Do people first create their own repo and then they move their code the KT organisation on GitHub?

### Code clarity and readability
Make sure the code is consistent, clear and readable.
Remind yourself while developing, that the connector code is open source and will be transferred to the community at some point.

?? What's the process for this?

### Integration testing
There is a domain specifically for connectors to execute their integration tests with the Koppeltaal server (called _TestConnector_). Some useful tests:

- Create `ActivityDefinition`
- Create `Patient`
- Create `CarePlan` for `Patient` with `CarePlanActivity` based on `ActivityDefinition`
- Launch `CarePlan(Sub)Activity` from `CarePlan` as `Patient`/`CareGiver`
- Update `ActivityStatus` on `CarePlan(Sub)Activity`

### Technical documentation
The documentation for a connector should be written in a `README.md` file, placed in the root of the project. This should contain the technologies used to develop the connector, including relevant technical details and caveats, if any. It should also document how to use the connector in an application and which features are supported. Readme examples are available in the connector repositories on the [Koppeltaal organization on GitHub].

## Development process

Exact details TBD for connector projects, but a general outline would be:

- Use a git repository on [Koppeltaal organization on GitHub]
- Release management
    - Which features to support (roadmap)
    - Design / develop
    - Plan release (feature / bug fix)
- Tests
- Release (major / minor)

### Domain configuration for testing purposes
Configuring a domain to test the connector integration with the Koppeltaal server.

- _TestConnector_ domain is available on the edge server
- Register the connector (as an application) to this domain through [Koppeltaal support]
- Configure connector in the admin area
    - Configure SSO url for launch purposes

## Delivery aftercare

- Answer support questions (?), fix bugs (?)
    - What does Koppeltaal expect

## Still have questions?
The Koppeltaal team is available for questions on [Slack chat].


[comment]: # (Below a list of keys and hyperlinks used in this document)

[Facade]:                             https://en.wikipedia.org/wiki/Facade_pattern
[Edge]:                               https://edgekoppeltaal.vhscloud.nl/portal/login.aspx
[Next]:                               https://nextkoppeltaal.vhscloud.nl/portal/login.aspx
[Stable]:                             https://stablekoppeltaal.vhscloud.nl/portal/login.aspx
[Koppeltaal organization on GitHub]:  https://github.com/Koppeltaal
[SoapUI project]:                     https://github.com/Koppeltaal/Koppeltaal-Server/tree/master/tests/Connectors
[Slack chat]:                         https://koppeltaal-dev.slack.com/messages/questions-remarks/details/
[FHIR resources]:                     https://koppeltaal.github.io/documentation/koppelaal-1.2/specification/#message-content-ontology
[Koppeltaal support]:                 https://www.koppeltaal.nl/support
[description of the SoapUI project]:  https://www.koppeltaal.nl/wiki/Registration_to_Test_Environment#Connecting_to_the_Koppeltaal_test_server_using_SOAP_UI
[Technical Design Document]:          https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2
[Message event types]:                https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Messages
[storage service]:                    https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Storing_data_in_the_storage_service
[GetNextNewAndClaim]:                 https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Retrieving_messages
[ActivityDefinition]:                 https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Retrieving_and_updating_activity_definitions
[Web Launch Sequence]:                https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Web_Launch_Sequence
[handling messages]:                  https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Updating_the_ProcessingStatus_for_a_Message
[SignalR]:                            https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2.1#Receiving_a_notification_when_a_new_message_becomes_available
[DSTU1]:                              http://www.hl7.org/FHIR/DSTU1/downloads.html#refimpl
[current version]:                    http://www.hl7.org/FHIR/downloads.html#refimpl
[latest release of the Koppeltaal server]: https://github.com/Koppeltaal/Koppeltaal-Server/releases

[comment]: # (Below a list of keys and images used in this document)

[figure 1]: write_connector__figure1.png "The application exchanges with Koppeltaal through a connector."
