---
title: Introduction
category: Integrator
order: 1
---
#Table of contents

[TOC]

# Introduction

Koppeltaal is a foundation in which mental healthcare organisations and IT suppliers take place. Koppeltaal’s offers two main propositions:

* **Koppeltaal** - a community supported information standard based on HL7 FHIR used for defining a current set of messages

* **Koppeltaal Server** - a message platform with a REST API

Using these it is possible to develop reliable, portable integrations between two ehealth applications. Koppeltaal will not define exactly how to build a feature, but it will provide a basis to design the interfaces, the process and the data involved. It will also provide the infrastructure to develop, test, accept the integration and eventually ramp up to production.  

When planning an Iintegration (*Kkoppeling) *IT suppliers may choose to use Koppeltaal to

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

* Allow clinicians to provision patients with a Mobile Game via an eHhealth platform

* Allow patients to see and access their ROM questionnaires through a patient portal

## Why Koppeltaal?

Mental healthcare in the Netherlands comprise of approximately 140 large and medium sized organisations (*source: Koppeltaal GGZ (IT meeting) presentation, 2014)*. Most of these organisations use one or more of a smaller group of eHealth products or services. EhHealth products or services comprise of mobile apps, personal health records, patient portals and other platforms offering online (web based) eHealth in the form of treatments, measurements, monitoring etc.

Reasons for healthcare organisations and professionals to adopt ehealth are:

* Governments and insurance companies have long stimulated financially

* Budget costs lead to new way of organising care more efficiently

* Patients expect online healthcare

* Technology drive leads to more possibilities 

This leads to the emergence of many ehHealth products and services. Naturally, there is a desire for these products and services to be integrated in the IT landscape of healthcare organisations. This tendency results in a large number of permutations, that calls for standardisation.

# Reading guide

This documentation will explain how to deal with Koppeltaal as an IT supplier, be it a software developer or a product, project or sales manager. It could also be useful for functional application managers or IT-professionals from the care provide side. 

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

 

# Who is involved in a Koppeltaal project - nvt

Various parties are involved in Koppeltaal in general. 

![Involved in Koppeltaal](https://lh4.googleusercontent.com/NWJb6ELpZ9fyTFhEj9cObtMt4xopEGdlRYJDdf7wQsKS84xpLxr_0bZxuEOlW5v5HaTWeuJF=w1833-h974)

* Stichting Koppeltaal - governance (Board), operational and financial management  

* Participants e-health supplier - all IT suppliers associated with Koppeltaal

* Healthcare provider - as customers of the foundation

The direct participants for a Koppeltaal project are more specific.

Project using Koppeltaal do not revolve around Koppeltaal, the project achieve a goal set by the shared customer. 

* The customer (healthcare organisation) requests an outcome and accepts the result of the Koppeltaal project

* IT supplier 1(yourself) - provides access to resources and connects with Koppeltaal server

* IT supplier 2 - provides access to resources and connects with Koppeltaal server

* Koppeltaal - provides Koppeltaal server and facilitates the integration by means of the Koppeltaal standard, the Koppeltaal server and project support.

# What is Koppeltaal - MZ

The Koppeltaal Server is a system that works like a mailbox. All the registered applications (e-interventions and portals) can drop messages in the mailbox. The Koppeltaal Server routes the message to the subscribed application queues. The subscribed applications can take the messages for their own use.

![Koppeltaal architecture](https://lh4.googleusercontent.com/9Q6LgSzkIhAXPAHECHvAPQLUbWTuvz3G2sLyv8WoA9aTR8yPPoklOgRbQoaOUj1ksbpVfTY-zrDZ08A=w1833-h930)

## API based
The Koppeltaal server works as a REST API using Basic authentication. All responses can be obtained in JSON or XML format.

## FHIR based
_Short description of FHIR (what is it, why does Koppeltaal use it, what does using is mean?)_

## Connectors
There are connectors available that can be used by clients to transform Koppeltaal messages from XML or JSON into their native language (C#, Python etc) and vise versa. You can find all available connectors here.

## SSO via OAuth 2.0
Koppeltaal contains an SSO mechanism that makes it unnecessary for applications to implement specific logic for each intervention it needs to work with. Applications therefore do not have to maintain specific configuration for each application that they access via SSO. The SSO mechanism is based on the accepted standard of OAuth 2.0.

Koppeltaal Single Sign-On is based on the OAuth2 standard, and implemented as recommended by the SMART-on-FHIR initiative (see http://docs.smartplatforms.org/)

In the context of OAuth2 two types of clients are defined:

- "Public Client" refers to applications that run entirely on an end-user's device (e.g. JavaScript app in the browser), meaning that the application is unable to protect a "client secret". The Ranj Kick ASS game is an example of a Public Client.
- "Confidential Client" are applications that are able to protect the "client secret", usually because the app has server-side business logic.

The only real difference between the implementation for Public and Confidential clients is in step 6, when the client accesses the Token endpoint, where the Confidential client must pass the client_id and client_secret in a Basic Authentication header. It is configured at the client level if public token requests are allowed.

## Security and privacy
Koppeltaal has some methods to guarantee security of data:

 - Data is nearly always specific to a domain. An application should not republish any received messages in another domain. Any information received through messages in a given domain should only be published within the same domain.
 - 

## Definitions

Within the context of Koppeltaal the terms 'Application', 'Koppeltaal Server' (or just 'Server') and 'Domain' have very specific meanings. Understanding the relation between these three concepts is central to understanding how to integrate via Koppeltaal.

### Koppeltaal Server

The Koppeltaal Server is the central connection point for all connecting parties. It provides a REST API to enable the connecting parties to exchange messages with each other. There is a number of different Koppeltaal Servers; currently each one is intended for use during a specific part of an application's development cycle (see Environments).

### Domain

A domain is the context in which Koppeltaal messages are exchanged. For every domain there is one organization that is owner of the patient data that is exchanged in that domain. The domain is usually named after that organization. Messages are only send within one domain for security reasons. The only exception to this are information messages (currently only 'CreateOrUpdateActivityDefinition', which is only sent by the server itself). The domain is mainly added to the domain model for security reasons.

### Application

An application is an intervention, portal or other E-Health software that will connect with other applications through a Koppeltaal Server. EMHP, KickAss and the Koppeltaal Demo Portal are examples of applications. Each application is part of one or more domains (see *Application instance* below). When an application is added to a domain the resulting combination of application and domain is known as an application instance. A set of credentials is always linked to an application instance, meaning that one set of credentials can only be used to send messages in one domain.

### Message

A message can be published in a domain. Only applications in that domain can receive the message.

### MessageType

Each message has a type. An application will only receive messages of a type they have registered for.

# Messages - MZ

## Principles of message brokers

## Subscribe to message types

## Get messages

### Claim message

Set message status to `success` or ‘failed’

## Send message

## Domains

# How will it work? - nvt

* Development

* Testing

* Acceptation

* Production

* Support

* Contacts

# Starting a Koppeltaal project - MZ

## What do I need?

* Set up

* Users with credentials

* Access to various environments

* A plan

* Stakeholders involved

## What will I do?

