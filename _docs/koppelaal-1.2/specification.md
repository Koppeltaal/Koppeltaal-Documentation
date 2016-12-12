---
title: Koppeltaal 1.2
category: Specification
order: 1
---

# Introduction

This technical design has been written to describe the technical scope of Koppeltaal 1.2.

The concept of the Koppeltaal Server is created to support the interaction between portals and e-interventions via a standard protocol.

The Koppeltaal Server is a system that works like a mailbox. All the registered applications (e-interventions and portals) can drop messages in the mailbox. The Koppeltaal Server routes the message to the subscribed application queues. The subscribed applications can take the messages for their own use.

# Ontology

Koppeltaal talks about information on two levels. On the higher level, Koppeltaal defines entities in health care, describing the content of the messages that are sent through the Koppeltaal Server. This level is described in the [message content ontology](#message-content-ontology).

On the lower level, Koppeltaal defines an infrastructure for exchanging messages between the various connected applications. This level is described in the [infrastructure ontology](#infrastructure-ontology).

## Message content ontology

The information that is sent through the Koppeltaal Server can be broken down in so-called resources. Each resource contains a structured set of data that describes a concept or entity about which information needs to be exchanged.

Resources are described using the FHIR standard. FHIR is a specification of entities often used in healthcare and a protocol to exchange information about these entities between systems. Read more about FHIR at [<http://www.hl7.org/implement/standards/fhir/index.html>](http://www.hl7.org/implement/standards/fhir/index.html).

The table below shows the mapping from the entities described in the functional ontology to the available FHIR resources.

Koppeltaal entity | FHIR resource
---------------------|--------------
Activity | `Other` (CarePlanActivity)
ActivityProvider | _Not mapped. Any application can provide activities. This is specified by the ActivityDefinitions an application makes available._
Application | `Device`
Caregiver | `Practitioner`
Carepath | `CarePlan`
Client | `Patient`
Intervention | _Not mapped. An intervention is a type of activity._
Person | _Not mapped. Information about people is sent as one of the specific_ roles: `Patient`, `Practitioner` or `RelatedPerson`.
Portal | _Not mapped. A portal is kind of application._
Related person | `RelatedPerson`
Result | DiagnosticResport (but significantly extended. See <a href="#h.9vq3ttcw353y" title="wikilink">CarePlanActivityResult</a>)
Role | _Not mapped. A person’s role is implied by the type of resource used. I.e., a person acting in the role of caregiver will be sent as a resource of type Practitioner._
ROM | _Not mapped. A ROM is a kind of activity._
Screener | _Not mapped. A screener is a kind of activity._
Treatment | _Not mapped. The treatment is implicit in the CarePlans assigned to a Patient._

Note that in the ontology below some concepts from the full functional ontology have been omitted because they are implicit. In particular, the different types of activity that are known have been abstracted into ‘ActivityDefinition’. This allows the Koppeltaal Server to relay information about any type of activity, including any future activity types.

## Infrastructure ontology

The Koppeltaal Server acts only as a message router and filter. This means that the domain model can be very simple.

![](image02.png)

There are four entities in the ontology:

-   Application
    -   A party that wishes to communicate through the Koppeltaal Server.
-   Domain
    -   Each application is part of one or more domains. The domain is mainly added to the domain model for security reasons. This is explained in the paragraph ‘[Security](#Security "wikilink")’
-   Message
    -   A message can be published in a domain. Only applications in that domain can receive the message.
-   MessageType
    -   Each message has a type. An application will not receive messages of a type they have not registered for.


`​``html
<html>
<a href="#">Hello world</a>
</html>
`​``

`​``python
def helloworld():
    print("hello world")
`​``
