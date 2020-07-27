---
title: What is Koppeltaal
category: Integrator
order: 1
---

# integrator-what\_is\_koppeltaal

The Koppeltaal Server is a system that works like a mailbox. All the registered applications \(e-interventions and portals\) can drop messages in the mailbox.

Koppeltaal has two functions. On one level, Koppeltaal defines entities in healthcare, describing the content of the messages that are sent through the Koppeltaal Server.

On the other level, Koppeltaal defines an infrastructure for exchanging messages between the various connected applications. The Koppeltaal Server routes the message to the subscribed application queues. The subscribed applications can take the messages for their own use.

### ![image alt text](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/what_is_koppeltaal.png)

### API based

The Koppeltaal server works as a REST API using Basic authentication to enable the connecting parties to exchange messages with each other. All responses can be obtained in JSON or XML format.

### FHIR based

The information that is sent through the Koppeltaal Server can be broken down in so-called resources. Each resource contains a structured set of data that describes a concept or entity about which information needs to be exchanged.

Resources are described using the FHIR standard. FHIR is a specification of entities often used in healthcare and a protocol to exchange information about these entities between systems. Read more about FHIR at [http://www.hl7.org/implement/standards/fhir/index.html](http://www.hl7.org/implement/standards/fhir/index.html).

### Connectors

There are connectors available that can be used by clients to transform Koppeltaal messages from XML or JSON into their native language \(C\#, Python etc\) and vise versa. You can find all available connectors here.

### SSO via OAuth

Koppeltaal contains an SSO mechanism that makes it unnecessary for applications to implement specific logic for each intervention it needs to work with. Applications therefore do not have to maintain specific configuration for each application that they access via SSO.

Koppeltaal Single Sign-On is based on the OAuth2 standard and implemented as recommended by the SMART-on-FHIR initiative \(see [http://docs.smartplatforms.org/](http://docs.smartplatforms.org/)\)

In the context of OAuth2 two types of clients are defined:

* "Public Client" refers to applications that run entirely on an end-user’s device \(e.g. JavaScript app in the browser\), meaning that the application is unable to protect a “client secret”. The Ranj Kick ASS game is an example of a Public Client.
* "Confidential Client" are applications that are able to protect the “client secret”, usually because the app has server-side business logic.

The only real difference between the implementation for Public and Confidential clients is in step 6, when the client accesses the Token endpoint, where the Confidential client must pass the client\_id and client\_secret in a Basic Authentication header. It is configured at the client level if public token requests are allowed.

### Security and privacy

Koppeltaal has some methods to guarantee security of data:

* Data is nearly always specific to a domain. An application should not republish any received messages in another domain. Any information received through messages in a given domain should only be published within the same domain.

### Definitions

Within the context of Koppeltaal the terms 'Application', 'Koppeltaal Server' \(or just 'Server'\) and 'Domain' have very specific meanings. Understanding the relation between these three concepts is central to understanding how to integrate via Koppeltaal.

#### Koppeltaal Server

The Koppeltaal Server is the central connection point for all connecting parties. There are a number of different Koppeltaal Servers; currently each one is intended for use during a specific part of an application's development cycle \(see Environments\).

#### Domain

A domain is the context in which Koppeltaal messages are exchanged. For every domain there is one \(healthcare\) organization that is owner of the patient data that is exchanged in that domain. The domain is usually named after that organization. Messages are only sent within one domain for security reasons. The only exception to this are information messages \(currently only 'CreateOrUpdateActivityDefinition', which is only sent by the server itself\). The domain is mainly added to the domain model for security reasons.

#### Application

An application is an intervention, portal or other eHealth software that will connect with other applications through a Koppeltaal Server. EMHP, KickAss and the Koppeltaal Demo Portal are examples of applications. Each application is part of one or more domains. When an application is added to a domain the resulting combination of application and domain is known as an application instance. A set of credentials is always linked to an application instance, meaning that one set of credentials can only be used to send messages in one domain.

#### Message

A message can be published in a domain by an application. Only applications in that domain can receive the message.

#### MessageType

Each message has a type. An application will only receive messages of a type they have registered for. Examples of message types are CreateOrUpdatePatient, CreateOrUpdateCarePlan and CreateOrUpdateActivityDefinition.

#### ActivityDefinition

_Explain activity definition here_

#### CarePlan

_Explain CarePlan here_

## Messages

### Principles of message brokers

...

### Subscribe to message types

Each application instance can subscribe to a certain message type. Based on the subscription of an application instance, the Koppeltaal server will put a message in the application instance’s message queue.

### Get messages

#### Claim message

An application should claim a message in its queue prior to processing. When claimed, no other processes should handle this message. Since every application has its own message queue based on the message type subscription, this should protect the application from processing a message multiple times.

After a message has been successfully processed, the application must update its processing status to "Success". In case of a transient failure, the message should be put back to the processing status “New”, allowing it to be reprocessed later. In case of a permanent failure \(e.g. message content was incorrect\), the processing status should be updated to “Failed”, and an exception description must be passed.

#### Receiving a notification when a new message becomes available

Messages should be actively received by applications from the Koppeltaal server. However, the Koppeltaal Server offers a SignalR hub that sends a notification when a new message becomes available. The event informs the application that there is a new message, the message must then be actively retrieved by the application.

### Send message

#### Message versions

In Koppeltaal, all messages indicate an update to or creation of a resource. Since multiple applications may have an internal copy of a resource, applications must be aware of which version of the resource they are updating. Otherwise they risk overwriting changes made by another application. In order to guard against this type of error Koppeltaal uses a versioning system.

Koppeltaal will override any unprocessed older versions of messages that are still in a queue when a new version is received. This is done to reduce the number of messages an application has to parse.

Note that this means that an application can not rely on receiving any intermediate messages. For example, it is not guaranteed that a client portal receives status updates of an activity for each change from ‘available’ to ‘in progress’ to ‘finished’. If the activity is started and finished before the client portal retrieves its messages, any status message will list the activity status as ‘finished’ instead of ‘in progress’.

Each message received by the Koppeltaal is given a version. Any other applications that send the same type of message for a resource must subscribe to that type of message in order to keep the internally stored resource up to date.

Each message must specify what version is the latest known to the sending application. Koppeltaal will check this version against the latest version that is has received and reject a message if the versions do not match. This is known as a concurrent modification error.

