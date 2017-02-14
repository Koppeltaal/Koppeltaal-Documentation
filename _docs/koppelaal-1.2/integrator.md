---
title: Introduction
category: Integrator
order: 1
---
#Table of contents

[TOC]

# Introduction

Koppeltaal is a foundation in which mental healthcare organisations and IT suppliers take place. Koppeltaal offers two main propositions:

* **Koppeltaal** - a community supported information standard based on HL7 FHIR used for defining a current set of messages

* **Koppeltaal Server** - a message platform with a REST API

Using these it is possible to develop reliable, portable integrations between two ehealth applications. Koppeltaal will not define exactly how to build a feature, but it will provide a basis to design the interfaces, the process and the data involved. It will also provide the infrastructure to develop, test, accept the integration and eventually ramp up to production.  

When planning an integration (*koppeling) *IT suppliers may choose to use Koppeltaal to

* Increase the portability of integrations between customers

* Decrease dependency of implementation specifics of other IT suppliers

* Tailor to the needs of a customer that is planning to or already using Koppeltaal

* Increase the quality of a software solution from using a well known standard (FHIR and Koppeltaal)

Healthcare organisations may choose to use Koppeltaal to:

* Reduce IT problems with integration, and associated costs

* Increase choice

* Cost reduction

* Improve quality of care

## Use cases

So what can be achieved using Koppeltaal? Koppeltaal is being extended to support increasingly more use cases. Each extension is made available through a new Koppeltaal version. These versions are published on @@@

Current use cases are:

* Allow clinicians to provision patients with a Mobile Game via an eHealth platform

* Allow patients to see and access their ROM questionnaires through a patient portal

* Allow patients to access modules from various providers in a patient portal.

## Why Koppeltaal?

Mental healthcare in the Netherlands comprise of approximately 140 large and medium sized organisations (*source: Koppeltaal GGZ (IT meeting) presentation, 2014)*. Most of these organisations use one or more of a smaller group of eHealth products or services. EHealth products or services comprise of mobile apps, personal health records, patient portals and other platforms offering online (web based) eHealth in the form of treatments, measurements, monitoring etc.

Reasons for healthcare organisations and professionals to adopt ehealth are:

* Governments and insurance companies have long stimulated financially

* Budget costs lead to new way of organising care more efficiently

* Patients expect online healthcare

* Technology drive leads to more possibilities

This leads to the emergence of many ehHealth products and services. Naturally, there is a desire for these products and services to be integrated in the IT landscape of healthcare organisations. This tendency results in a large number of permutations, that calls for standardisation.

Koppeltaal use FHIR, their Koppeltaal community and a domain driven design process to evolve the *Koppeltaal* and the *Koppeltaal Server* implement the supported use cases.

# Reading guide

The Koppeltaal documentation will explain how to deal with Koppeltaal as an IT supplier, be it a software developer or a product, project or sales manager. It could also be useful for functional application managers or IT-professionals from the care provide side.

## Documentation structure

We’ve structured the documentation to be iteratively detailed, such that reading it linearly will take you from being completely new to being an expert developer. You may of course stop whenever you like. The sections are as follows:

1. An introduction to provide a quick overview of the various facets relevant in a Koppeltaal project. You will likely read this only once, if at all.

    1. A general project brief

    2. A more detailed decomposition of the anatomy of a Koppeltaal

    3. A similar decomposition of a Koppeltaal project.

2. Technical documentation necessary when building an adapter

    4. ...

3. Technical documentation necessary when using an adapter

    5. ...

## I need to know...

* Who do I need to contact when starting a project, Go to chapter 1

* Why am I receiving empty Json, go to chapter 3

* Where to start when doing regression tests, go to chapter 2

* Who defines what I can and can’t do with Koppeltaal.

* ...



# Who is involved in a Koppeltaal project

Various parties are involved in Koppeltaal in general.

![image alt text](image_0.png)

* Stichting Koppeltaal - governance (Board), operational and financial management  

* Participants e-health supplier - all IT suppliers associated with Koppeltaal

* Healthcare provider - as customers of the foundation

The direct participants for a Koppeltaal project are more specific.

Project using Koppeltaal do not revolve around Koppeltaal, the project achieve a goal set by the shared customer.

* The customer (healthcare organisation) requests an outcome and accepts the result of the Koppeltaal project

* IT supplier 1 (yourself) - provides access to resources and connects with Koppeltaal server

* IT supplier 2 - provides access to resources and connects with Koppeltaal server

* Koppeltaal - provides Koppeltaal server and facilitates the integration by means of the Koppeltaal standard, the Koppeltaal server and project support.

# What is Koppeltaal

The Koppeltaal Server is a system that works like a mailbox. All the registered applications (e-interventions and portals) can drop messages in the mailbox.

Koppeltaal has two functions. On one level, Koppeltaal defines entities in healthcare, describing the content of the messages that are sent through the Koppeltaal Server.

On the other level, Koppeltaal defines an infrastructure for exchanging messages between the various connected applications. The Koppeltaal Server routes the message to the subscribed application queues. The subscribed applications can take the messages for their own use.

## ![image alt text](image_1.png)

## API based

The Koppeltaal server works as a REST API using Basic authentication to enable the connecting parties to exchange messages with each other. All responses can be obtained in JSON or XML format.

## FHIR based

The information that is sent through the Koppeltaal Server can be broken down in so-called resources. Each resource contains a structured set of data that describes a concept or entity about which information needs to be exchanged.

Resources are described using the FHIR standard. FHIR is a specification of entities often used in healthcare and a protocol to exchange information about these entities between systems. Read more about FHIR at [http://www.hl7.org/implement/standards/fhir/index.html](http://www.hl7.org/implement/standards/fhir/index.html).

## Connectors

There are connectors available that can be used by clients to transform Koppeltaal messages from XML or JSON into their native language (C#, Python etc) and vise versa. You can find all available connectors here.

## SSO via OAuth

Koppeltaal contains an SSO mechanism that makes it unnecessary for applications to implement specific logic for each intervention it needs to work with. Applications therefore do not have to maintain specific configuration for each application that they access via SSO. The SSO mechanism is based on the accepted standard of OAuth 2.0.

Koppeltaal Single Sign-On is based on the OAuth2 standard, and implemented as recommended by the SMART-on-FHIR initiative (see [http://docs.smartplatforms.org/](http://docs.smartplatforms.org/))

In the context of OAuth2 two types of clients are defined:

* "Public Client" refers to applications that run entirely on an end-user’s device (e.g. JavaScript app in the browser), meaning that the application is unable to protect a “client secret”. The Ranj Kick ASS game is an example of a Public Client.

* "Confidential Client" are applications that are able to protect the “client secret”, usually because the app has server-side business logic.

The only real difference between the implementation for Public and Confidential clients is in step 6, when the client accesses the Token endpoint, where the Confidential client must pass the client_id and client_secret in a Basic Authentication header. It is configured at the client level if public token requests are allowed.

## Security and privacy

Koppeltaal has some methods to guarantee security of data:

* Data is nearly always specific to a domain. An application should not republish any received messages in another domain. Any information received through messages in a given domain should only be published within the same domain.

## Definitions

Within the context of Koppeltaal the terms 'Application', 'Koppeltaal Server' (or just 'Server') and 'Domain' have very specific meanings. Understanding the relation between these three concepts is central to understanding how to integrate via Koppeltaal.

### Koppeltaal Server

The Koppeltaal Server is the central connection point for all connecting parties. There is a number of different Koppeltaal Servers; currently each one is intended for use during a specific part of an application's development cycle (see Environments).

### Domain

### A domain is the context in which Koppeltaal messages are exchanged. For every domain there is one (healthcare) organization that is owner of the patient data that is exchanged in that domain. The domain is usually named after that organization. Messages are only send within one domain for security reasons. The only exception to this are information messages (currently only 'CreateOrUpdateActivityDefinition', which is only sent by the server itself). The domain is mainly added to the domain model for security reasons.

### Application

An application is an intervention, portal or other E-Health software that will connect with other applications through a Koppeltaal Server. EMHP, KickAss and the Koppeltaal Demo Portal are examples of applications. Each application is part of one or more domains. When an application is added to a domain the resulting combination of application and domain is known as an application instance. A set of credentials is always linked to an application instance, meaning that one set of credentials can only be used to send messages in one domain.

### Message

A message can be published in a domain by an application. Only applications in that domain can receive the message.

### MessageType

Each message has a type. An application will only receive messages of a type they have registered for. Examples of message types are CreateOrUpdatePatient, CreateOrUpdateCarePlan and CreateOrUpdateActivityDefinition.

### ActivityDefinition

*Explain activity definition here*

### CarePlan

*Explain CarePlan here*

# Messages

## Principles of message brokers

## Subscribe to message types

Each application instance can subscribe to a certain message type. Based on the subscription of an application instance, the Koppeltaal server will put a message in the application instance’s message queue.

## Get messages

### Claim message

An application should claim a message in his queue prior to processing. When claimed, no other processes should handle this message. Since every application has its own message queue based on the message type subscription, this should protect the application from processing a message multiple times.

After a message has been successfully processed, the application must update its processing status to "Success". In case of a transient failure, the message should be put back to the processing status “New”, allowing it to be reprocessed later. In case of a permanent failure (e.g. message content was incorrect), the processing status should be updated to “Failed”, and an exception description must be passed.

### Receiving a notification when a new message becomes available

Messages should be actively received by applications from the Koppeltaal server. However, the Koppeltaal Server offers a SignalR hub that sends a notification when a new message becomes available. The event informs the application that there is a new message, the message must then be actively retrieved by the application.

## Send message

### Message versions

In Koppeltaal, all messages indicate an update to or creation of a resource. Since multiple applications may have an internal copy of a resource, applications must be aware of which version of the resource they are updating. Otherwise they risk overwriting changes made by another application. In order to guard against this type of error Koppeltaal uses a versioning system.

Koppeltaal will override any unprocessed older versions of messages that are still in a queue when a new version is received. This is done to reduce the number of messages an application has to parse.

Note that this means that an application can not rely on receiving any intermediate messages. For example, it is not guaranteed that a client portal receives status updates of an activity for each change from ‘available’ to ‘in progress’ to ‘finished’. If the activity is started and finished before the client portal retrieves its messages, any status message will list the activity status as ‘finished’ instead of ‘in progress’.

Each message received by the Koppeltaal is given a version. Any other applications that sends the same type of message for a resource must subscribe to that type of message in order to keep the internally stored resource up to date.

Each message must specify what version is the latest known to the sending application. Koppeltaal will check this version against the latest version that is has received and reject a message if the versions do not match. This is known as a concurrent modification error.

## Domains

# How will it work?

* Development

* Testing

* Acceptation

* Production

* Support

* Contacts

# Starting a Koppeltaal project

In order to start with a Koppeltaal project, the following things need to be present:

* Two or more IT suppliers

    * Two or more applications

* At least one healthcare provider

    * Koppeltaal Domain

* One or more use cases

* Koppeltaal supplier access

    * Koppeltaal Server development and/or test environments

Whether explicitly in a project document or implicitly in an agile development setting, the following development phases will be followed:

1. **Definition of Scope -** the first step is ascertaining what exactly needs to be realised. This phase should be conducted by all parties involved.

2. **Design: Integration - **Design of the integration will done mainly by the IT suppliers and possibly Koppeltaal or the Koppeltaal community. The result of this phase will be a feasible design that will facilitate technical parties involved to create their own respective application designs. Roughly speaking this phase will yield:

    1. Functional Design

        1. Domain model

    2. Technical Design of Integration

        2. Stakeholders

        3. Systems

        4. Sequence Diagram

        5. Messages/Data

        6. Selection of Koppeltaal Version

3. **Make or "Buy" decision Adapter/Connector **- Based on the available connectors ([https://github.com/Koppeltaal](https://github.com/Koppeltaal)) a decision should be made whether to create a connector or build one.

4. **Design: Applications - **Koppeltaal will facilitate only in communication, and each IT supplier will need to design their respective applications as to create value for the users. This phase will yield:

    3. Functional Design

    4. Technical Design

    5. User Interface Design

5. **Development and/or configuration: Application**: Koppeltaal will facilitate only in communication, and each IT supplier will need to extend or configure their respective applications as to create value for the users. This phase will generally comprise of:  

    6. Integrating Connector

    7. Software development process

    8. Configuration process

6. **Testing: applications - **Each IT supplier should go about their own testing procedures

7. **Testing: integration - **In order to ensure the properly functioning integration as a whole, this phase should be conducted. For both applications and Koppeltaal server, the correct environments should be selected, based on Koppeltaal version.

8. **Acceptation - **After IT suppliers ascertained proper functioning of the integration, all other stakeholders should be involved for acceptation of the integration. Important should be the clear distinction between integration aspects and application aspects.

9. **Deployment of applications - **both applications deploy their respective versions and communicate about progress.

10. **Configuration of Koppeltaal - **Koppeltaal domain on Koppeltaal Server production environment should be configured appropriately.

11. **Integration Ramp Up - **When all parties involved provide a green light, the Koppeltaal messages can be exchanged!
