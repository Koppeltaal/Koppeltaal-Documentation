---
title: Write a Koppeltaal Connector
category: How-to
order: 1
---

# How to write a Koppeltaal connector

## About this guide
This guide assumes the reader knows Koppeltaal terminology. One source for that kind of knowledge is the [Technical Design Document]. This document is explicitly not technical, but rather a descriptive/explanatory guide on how to write a connector. This guide tries do that by answering questions developers will likely have.

## When to write a connector?
Every application that communicates with the Koppeltaal server will need a layer that performs communication between applications over the Koppeltaal server. A Koppeltaal connector will provide that layer to be reused by other applications in the form of a library (figure 1).

![figure 1]
**Figure 1**. _Every application communicates with the Koppeltaal server through a connector that encapsulates most of the complexity._

If your application needs functionality in an existing connector that has not been implemented, feel free to contribute to the connector project and create a pull request at the repository at the [Koppeltaal organization on GitHub]. When no connector exists with an API in the programming language of the application you want to connect, you can write one yourself. 

## Connector repository and source code
Since the connector will be used by other parties and will also be handed over to the Koppeltaal Community at some point, it’s important that the source code is clear and readable for other developers that want to debug or add features in the (near) future.

A git repository can be created at the [Koppeltaal organization on GitHub]. Sources of connectors in other programming languages can be viewed there as well.

## Where to start
- Find out which FHIR resources need to be communicated about.
- Find out if there is a FHIR model library for my programming language.
- Determine which version of Koppeltaal should be supported.
- Study the sample requests to the Koppeltaal server

### Supported FHIR resources
This depends on the needs of the application(s) that will use the connector. It is possible to support a subset of `Message` types, to which an application subscribes through the administration console on the Koppeltaal [Edge] / [Next] / [Stable] server.

### FHIR libraries
HL7 provides so called _Reference Implementations_ for some programming languages. These are basic libraries that contain FHIR resource models and validation schemas, for more convenient implementation of a connector: [DSTU1] / [current version].

### Koppeltaal versions
The first release of the connector should support the current version of Koppeltaal. Subsequent releases of the connector should still support older implementations of Koppeltaal.

### Sample requests
Koppeltaal provides a [SoapUI project] on GitHub that contains sample requests for implementers gain more knowlegde about the exact structure of a message. The [description of the SoapUI project] contains more in-depth information about how to make use of it. It is recommended to use these examples, when debugging your own requests.

## Connector responsibilities
A Koppeltaal connector is a library to be used by an application written in a particular programming language. It communicates directly with the Koppeltaal Server REST interface, while exposing a simple API (e.g., a [Facade]) to the application, exchanging custom objects. Koppeltaal specific complexity should be handled by the connector - e.g., composing a message that conforms to Koppeltaal ontology.

_Note_: The Koppeltaal server supports both JSON and XML.

Obviously, the functionalities a connector should provide depends on the applications that use it. However, we think there is a set of basic functionalities that a connector in general should support.

- Retrieve the `Conformance Statement`
- Send/retrieve `Messages` to/from a domain
    - Create a Message bundle with FHIR Resources (send)
    - Extract FHIR Resources from the Message bundle (receive)
    - Update the _ProcessingStatus_ of a Message
- Retrieve and update `Activity Definitions`
- Launch a user to a specific application

Additionally, a connector could also support the following functionality:

- Implement support for _NewMessage_ push notifications, using [SignalR]
- Using the `Storage Service` as data persistence utility

The connector will achieve most of this functionality by sending/retrieving Messages according to Koppeltaal specifications.

### Basic features

#### The Conformance Statement
A `Conformance Statement` is a set of capabilities of a FHIR Server. The conformance statement of the Koppeltaal Server contains information required for the OAuth2 implementation of the single sign on. Besides the capabilities, it contains a number of important endpoints that are needed for certain actions. This statement can be requested via _${koppeltaal.server.url}/FHIR/Koppeltaal/metadata_ (e.g. http://edgekoppeltaal.vhscloud.nl/FHIR/Koppeltaal/metadata).
The connector must extract these endpoints from the conformance statement and use them for other actions. For instance, to request authorization for the launch of a game, the authorization endpoint must be read from the statement.

#### Koppeltaal Messages
Communication with the Koppeltaal server consists largely of exchanging `Messages`. A Koppeltaal message consists of a bundle of `FHIR Resources`. More information on the [FHIR resources] used in Koppeltaal.
The first resource in the bundle is the `MessageHeader`, which should always be present. The header contains important information about the content of the message, like the [message event types]. This information can be used to convert the resources in the bundle to a format that can be further processed by an application - e.g. an object holding all the important values to an application.

Please keep in mind that the connector should be able to exchange `Messages` using `Basic Authentication` as well as an `OAuth2 Bearer Token`. Using a `Bearer Token` implicitly only requests information for the user bound to the `Bearer Token`. Requesting patient-specific `Messages` with `Basic Authentication` requires a `patient` parameter.

_Note_: When building an outgoing message, mind that the MessageHeader should be the first Resource of the bundle, then add further resources.

#### Message ProcessingStatus
It is important that the `ProcessingStatus` is changed when [handling messages]. That way the Koppeltaal server knows a message has been handled. Make sure the connector can mark a message as `Failed`, also providing an exception description.

#### Activity Definitions
`ActivityDefinitions` are treated somewhat different than the rest of the FHIR resources. They are of resource type `Other` and the content is as such not defined in the FHIR spec. In Koppeltaal, they should be created or updated without the use of Message resource bundles. A simple http POST request containing the [ActivityDefinition] in the request body suffices to create an ActivityDefinition.

#### Launching Users To An Application
Koppeltaal provides a [Web Launch Sequence]. This allows users to login to an application and launch a `Resource`. The launch allows users to work on a `CarePlan(Sub)Activity`. 

### Additional features

#### Storage Service
More information following. [Storage service]

#### Push Notifications: (since 1.2.1)

For applications that require real-time updates from Koppeltaal, it is advised **not** to use long-polling. Koppeltaal supports push notifications to applications when a new Messages is available. Since Koppeltaal v1.2.1 there are two options to use the push mechanism. Both options are preferred over polling to reduce server load on both sides:

- Implement [SignalR] with subscription mechanism for the connector
- Configure a REST webhook for an application exposing a REST endpoint

##### SignalR (connector feature)
When available, use a SignalR library to aid in creating a _HubConnection_ to the Koppeltaal server and subscribe to the `NewMessage` event.
The connector then triggers the internal [GetNextNewAndClaim] action to fetch the new message(s).

##### REST webhook (application feature)
The application should expose a RESTful endpoint for the configurable webhook, configured in the _admin console of the application_. The Koppeltaal server makes an HTTP request to the URI configured for the webhook.
The application then triggers the [GetNextNewAndClaim] action in the connector to fetch the new message(s).

## Quality assessment
The connector code will be assessed by Koppeltaal on a number of matters, such as:

- Code clarity and readability
- Unit Test availability
- Technical documentation

### Code clarity and readability
Basically self explanatory. Remind yourself while developing, that the connector code is open source and transferred to the community at some point.

### Integration testing
There is a domain specifically for connectors to execute their integration tests with the Koppeltaal server (called _TestConnector_). Some useful tests:

- Create `ActivityDefinition`
- Create `Patient`
- Create `CarePlan` for `Patient` with `CarePlanActivity` based on `ActivityDefinition`
- Launch `CarePlan(Sub)Activity` from `CarePlan` as `Patient`/`CareGiver`
- Update `ActivityStatus` on `CarePlan(Sub)Activity`

### Technical documentation
This documentation should be written in a `README.md` file, placed in the root of the project. This should contain the used technologies to develop of the connector, including relevant technical details and caveats, if any. How to use the connector in an application and which features are supported. Readme examples are available in the connector repositories on the [Koppeltaal organization on GitHub].

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
[DSTU1]:                              http://www.hl7.org/FHIR/DSTU1/downloads.html
[current version]:                    http://www.hl7.org/FHIR/downloads.html

[comment]: # (Below a list of keys and images used in this document)

[figure 1]: write_connector__figure1.png "The application exchanges with Koppeltaal through a connector."
