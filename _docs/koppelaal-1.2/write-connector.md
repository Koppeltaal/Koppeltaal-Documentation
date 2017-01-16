---
title: Write a Koppeltaal Connector
category: How-to
order: 2
---

# How-to: Koppeltaal connector

## About this guide
This guide will not go into Koppeltaal terminology, but rather assumes this knowledge is available to the reader. Whether it is from memory or the [Technical Design Document]. This document is not technical, but rather a descriptive / explanatory guide to assist the implementer towards a usable connector. Mainly by answering question in advance, that we think developers will bump into.

## Connector repository and source code
Since the connector will be used by other parties and will also be handed over to the Koppeltaal Community at some point, it’s important that the source code is clear and readable for other developers that want to debug or add features in the (near) future.

A git repository can be created at the [Koppeltaal organization on GitHub]. Sources of connectors in other programming languages can be viewed there as well.

## Where to start
- Find out which FHIR resources need to be communicated about. Application dependent.
- Is there FHIR model library in my programming language?

## Connector responsibilities
A Koppeltaal connector is a library to be used by an application written in particular programming language. It communicates directly with the Koppeltaal Server REST interface, while exposing a simple API to the application, exchanging custom objects. Koppeltaal specific complexity should be handled by the connector - e.g., composing a message that conforms to Koppeltaal ontology.

_Note_: The Koppeltaal server supports both JSON and XML.

![figure 1]
![placeholder]
**Figure 1**. _Each application communicates with the Koppeltaal server through a connector to encapsulate most of the complexity._

Obviously, the functionalities a connector should provide depends on the applications that use it. However, we think there is a set of basic functionalities that a connector in general should support.
- Retrieve the `Conformance Statement`
- Send/retrieve `Messages` to/from a domain
-- Create a Message bundle with FHIR Resources (send)
-- Extract FHIR Resources from the Message bundle (receive)
-- Update the _ProcessingStatus_ of a Message
- Retrieve and update `Activity Definitions`

Additionally, a connector could also support the following functionality:
- Create a RESTful endpoint and configure a webhook on KT server
- Using the `Storage Service` as data persistance utitliy

The connector will achieve most of this functionality by sending/retrieving Messages according to Koppeltaal specifications.
view of the infrastructure entities that the connector will be dealing with.

### Basic features

#### The Conformance Statement
A `Conformance Statement` is a set of capabilities of a FHIR Server. The conformance statement of the Koppeltaal Server contains information required for the OAuth2 implementation for the single sign on. Besides the capabilities, it contains a number of important endpoints that are needed for certain actions. It can be requested via _<Koppeltaal server url>/FHIR/Koppeltaal/metadata_ (e.g. http://edgekoppeltaal.vhscloud.nl/FHIR/Koppeltaal/metadata).
The connector must extract these endpoints from the Conformance statement and use them for other actions. For instance, to request authorization for the launch of a game, the authorization endpoint must be read from the statement.

#### Koppeltaal Messages
Communication with the Koppeltaal server consists largely of exchanging `Messages`. The Koppeltaal message consists of a bundle of `FHIR Resources`. More information on the [FHIR resources] used in Koppeltaal.
The first resource in the bundle is the `MessageHeader`, which should always be present. The header contains important information about the content of the message, like the [message event types]. This information can be used to convert the resources in the bundle to a format that can be further processed by an application - e.g. an object holding all the important values to an application.
The relevant values of the Resource should be copied to simple objects that can be handled by the application. It is possible that HL7 provides a library that provides FHIR models and validation schema's: [DSTU1] / [current version].

_Note_: When building an outgoing message, mind that the MessageHeader should be the first Resource of the bundle, then add further resources.

#### Setting Message ProcessingStatus
It is important that the `ProcessingStatus` is changed when [handling messages]. That way the Koppeltaal server knows a message has been handled. Make sure to mark unprocessable messages as `Failed`, also providing an exception description.

#### Activity Definitions
`ActivityDefinitions` are treated somewhat different than the rest of the FHIR resources. They are of resource type `Other` and the content is as such not defined in the FHIR spec. In Koppeltaal, they should be created or updated without the use of Message resource bundles. A simple http POST request containing the [ActivityDefinition] in the request body suffices to create the ActivityDefinition.

### Additional features

#### New Message webhook vs New Message polling
The solution to polling the Koppeltaal server for new Messages is using a webhook, that must be configured in the _admin console of the application_ that uses the connector. The connector should expose a RESTful endpoint for the configurable webhook.
When a new Koppeltaal message is queued, the Koppeltaal server makes an HTTP request to the URI configured for the webhook. This should then trigger the [GetNextNewAndClaim] action in the connector to fetch the new message(s). We would recommend to implement this, since it only requires the exposition of a single rest endpoint to trigger the otherwise scheduled poll.

#### Storage Service
Not yet implemented in a connector: [Storage service]

## Quality assessment
[From the QA sheet](https://docs.google.com/spreadsheets/d/16I2M2feLDzqS9XANEizifueqacaHUiE2i721AXkWacY/edit?ts=5863cc45#gid=1641241298):
- Code clarity and readability (how clear is the code)
- "Code availability and review procedure (internal Review process / GIT integration)"
- Code management (Unit Test availability)
- Technical documentation (README): look at other connectors
-- In project root, to make it visible on GitHub
-- How to use the connector? (examples)
-- Technical details / caveats

## Development process
- Development process, unit / integration tests. 		Al doende. ‘praktisch’
- Release management (versioning / compatibility) Development process - kern functionele dekking

### Integration testing
There is a domain specifically for connectors to execute their intergration tests with the Koppeltaal server. Som inspiration for tests:
- Create `ActivityDefinition`
- Create `Patient`
- Create `CarePlan` for `Patient` with `CarePlanActivity` based on `ActivityDefinition`
- Launch `CarePlan(Sub)Activity` from `CarePlan` as `Patient`/`CareGiver`
- Send `ActivityStatus` update on `CarePlan(Sub)Activity`

## Setup a testing environment

### Domain configuration for testing purposes
Configuring a domain to test the connector.
- TestConnector domain
- Configure connector (as appliciation) in the admin area
- webhook configuration for 'push'

## Delivery aftercare
- Answer support questions (?), fix bugs (?)
-- What does Koppeltaal expect


[comment]: # (Below a list of keys and hyperlinks used in this document)

[Technical Design Document]: https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2
[Koppeltaal organization on GitHub]: https://github.com/Koppeltaal
[FHIR resources]: https://koppeltaal.github.io/documentation/koppelaal-1.2/specification/#message-content-ontology
[Message event types]: https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Messages
[storage service]: https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Storing_data_in_the_storage_service
[GetNextNewAndClaim]: https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Retrieving_messages
[ActivityDefinition]: https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Retrieving_and_updating_activity_definitions
[ProcessingStatus]: https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Updating_the_ProcessingStatus_for_a_Message
[DSTU1]: http://www.hl7.org/FHIR/DSTU1/downloads.html
[current version]: http://www.hl7.org/FHIR/downloads.html
[handling messages]: https://www.koppeltaal.nl/wiki/Technical_Design_Document_Koppeltaal_1.2#Updating_the_ProcessingStatus_for_a_Message

[comment]: # (Below a list of keys and images used in this document)

[figure 1]: /images/write_connector__figure1.png "The application exchanges with Koppeltaal through a connector."
[placeholder]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "placeholder"
