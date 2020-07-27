---
title: Messaging Strategy
category: Technical Designs
order: 3
---

# TD-messages

Author: Bart Mehlkop Datum: 03-03-2017 Versie: 0.1

## Version management

| Versie | Datum | Auteur | Aanpassingen |
| :--- | :--- | :--- | :--- |
| 0.1 | 02-12-2016 | Bart Mehlkop | First Draft |

## Table of content

\[\[TOC\]\]

## Messaging

In Koppeltaal, all messages indicate an update to or creation of a resource. Since multiple applications may have an internal copy of a resource, applications must be aware of which version of the resource they are updating. Otherwise they risk overwriting changes made by another application. In order to guard against this type of error Koppeltaal uses a versioning system.

Koppeltaal will override any unprocessed older versions of messages that are still in a queue when a new version is received. This is done to reduce the number of messages an application has to parse.

Note that this means that an application can not rely on receiving any intermediate messages. For example, it is not guaranteed that a client portal receives status updates of an activity for each change from ‘available’ to ‘in progress’ to ‘finished’. If the activity is started and finished before the client portal retrieves its messages, any UpdateCarePlanActivityStatus messages \(as well as any triggered CreateOrUpdateCarePlan messages\) will list the activity status as ‘finished’ instead of ‘in progress’.

## Message definitions

This chapter describes the definitions of all the messages which are available in ‘Koppeltaal’, the ‘language’ of the Koppeltaal Server. All these messages will be based on HL7 FHIR Resources. A Koppeltaal message will always be a bundle of general resources. The first part of this chapter describes the individual resources, the second part describes the messages.

## Guiding principles

Each message must be self-contained; no references will be made to external resources. The primary reason is that a new Application should not need to re-query older messages in order to get up-to-date. At the same time, this way we avoid:

The need to store copies of all data across all applications The use of external links, because this will complicate the architecture All resources that the sending application is owner of should be included in the message bundle. Any resources that the sending application is not owner of \(for example, the ActivityDefinition for each activity in a CreateOrUpdateCarePlan message\) may be referenced by their url \(See FHIR - basic rules\).

## Resource attribute categories

Resource have attributes. Each attribute is in one of the following categories:

Koppeltaal required - Applications that construct a Koppeltaal Message must provide the attributes in this category, and receiving applications must understand these attributes.

Required attributes are marked in the with ‘Koppeltaal required: true’.

Koppeltaal optional - Application that send and receive Koppeltaal messages should try to fill and must understand these attributes.

Optional attributes are all attributes defined in this document that are not marked as required.

Available in FHIR - All other attributes that are in defined in the FHIR Resource definitions

All other attributes that are available in FHIR can be found in the FHIR resource definitions: [http://www.hl7.org/implement/standards/fhir/resourcelist.html](http://www.hl7.org/implement/standards/fhir/resourcelist.html).

FHIR Extensions - Additional attributes that are added through the FHIR Extension mechanism.

## Publishing a message

The application POSTs a message bundle to [https://koppeltaal.nl/FHIR/Koppeltaal/Mailbox](https://koppeltaal.nl/FHIR/Koppeltaal/Mailbox). See General FHIR Resources for details about the content of a message.

## Sending a message

Each message received by the Koppeltaal is given a version. Any other applications that sends the same type of message for a resource must subscribe to that type of message in order to keep the internally stored resource up to date.

Each message must specify what version is the latest known to the sending application. The Koppeltaal will check this version against the latest version that is has received and reject a message if the versions do not match. This is known as a concurrent modification error.

## Obtaining the current version number

An application must provide the version of the resource that the update was based on when sending a message. There are two ways to obtain this number, each for a different situation.

When sending a message, the Koppeltaal Server will return the generated version number as part of the reply. The application may store the returned version number to re-use later.

If there are multiple applications that may send messages with the same focal resource, each will have to subscribe to the message type in order to receive updates \(and their version numbers\) from the other applications.

When a resource is updated for the first time the sending application should specify no version number. When a resource is first created the sending application does not yet know a version. In that case the sending application should not specify the version number and the Koppeltaal will generate the first version. If another version is already known the Koppeltaal will reject the message in the same way as if an out-of-date version was given.

## Retrieving messages

There are 3 supported interactions:

[https://koppeltaal.nl/FHIR/Koppeltaal/MessageHeader/\_search?\_query=MessageHeader.GetNextNewAndClaim](https://koppeltaal.nl/FHIR/Koppeltaal/MessageHeader/_search?_query=MessageHeader.GetNextNewAndClaim) - This will find the next message with ProcessingStatus= “New”, set its ProcessingStatus to “Claimed”, and returns the complete Bundle for that Message. This must always be followed by an update of the Message status. [https://koppeltaal.nl/FHIR/Koppeltaal/MessageHeader/\_search?\_summary=true&\_count=\[X](https://koppeltaal.nl/FHIR/Koppeltaal/MessageHeader/_search?_summary=true&_count=[X)\] - This will return a Bundle of MessageHeaders, allowing an application to browse the available messages. A pagesize can be specified in the \_count parameter, up to a maximum of 1000. [https://koppeltaal.nl/FHIR/Koppeltaal/MessageHeader/\_search?\_id=\[id](https://koppeltaal.nl/FHIR/Koppeltaal/MessageHeader/_search?_id=[id)\] - This can be used to fetch the complete Bundle for a single Message for which the MessageHeader was retrieved through the previous action. The following additional query parameters can be specified:

Patient: Filters on the Patient dossier this message belongs event: Filters on the message type ProcessingStatus: Filters on the ProcessingStatus \(New\|Claimed\|Success\|Failed\). This query parameter cannot be passed to the named query used in interaction 1.

## Updating the ProcessingStatus for a Message

After a message has been successfully processed, the application must update its ProcessingStatus to “Success” on URL [https://koppeltaal.nl/FHIR/Koppeltaal/MessageHeader/\[id](https://koppeltaal.nl/FHIR/Koppeltaal/MessageHeader/[id)\] \(that is, the URL returned as id link in the for the MessageHeader in the bundle.\) In case of a transient failure, the message should be put back to ProcessingStatus=“New”, allowing it to be reprocessed later. In case of a permanent failure \(e.g. message content was incorrect\), the ProcessingStatus should be updated to “Failed”, and an Exception description must be passed.

## Subscribing to receive messages

Not part of the scope for phase 1 The application POSTs a Subscription resource to [https://koppeltaal.nl/FHIR/Koppeltaal/Subscription](https://koppeltaal.nl/FHIR/Koppeltaal/Subscription). When an application publishes a message the Koppeltaal Server will check the message against the existing subscriptions. The message will then be made available for retrieval by the applications that are subscribed to it.

