---
title: Koppeltaal Automatic Data Removal
category: Technical Designs
order: 3
---

# TD-automatic-data-removal

Author: Bart Mehlkop Datum: 02-12-2016 Versie: 0.1

## Version management

| Versie | Datum | Auteur | Aanpassingen |
| :--- | :--- | :--- | :--- |
| 0.1 | 02-12-2016 | Bart Mehlkop | First Draft |
| 1.0 | 07-12-2016 | Bart Mehlkop | Finalized TD |
| 1.1 | 23-01-2017 | Bart Mehlkop | Maximum message timeout set to 56 days after community review |

## Table of content

\[\[TOC\]\]

## Introduction

In order to protect client confidentiality and conform to regulations regarding privacy it is not desirable to store data that is no longer needed for correct functionality of the software. Any data that is not present on the server can obviously not be leaked by it.

This document lists the sensitive data that is present on the Koppeltaal Server, the requirements the automatic cleanup must fulfill and describes the technical changes required to automatically clean up old data.

## Sensitive data on the Koppeltaal Server

The main source of sensitive data on the Koppeltaal Server are the FHIR messages that are exchanged between applications. These messages may contain all sorts of patient data, including name, BSN and address information.

There are a number of related sets of data that contain patient information as a side effect of their function. Specificially, the table ‘IntegrationMessageLogs’ logs all API-calls, including those for posting new FHIR messages, and includes the content of the call.

The ‘IntegrationMessageLogs’ table is already being cleaned automatically, with calls that completed successfully being cleaned after 7 days and failed calls after 14 days. These records are useful when debugging any issues that occur on the Koppeltaal Server.

## Requirements

The main reference point of the automatic cleanup is that messages should not be allowed to exist on the Koppeltaal Server for more than 56 days and that preferably messages are cleaned up as soon as all recipients have successfully retrieved the message.

Unfortunately, due to technical reasons one specific application requires CreateOrUpdateCarePlan messages to remain on the Koppeltaal Server indefinitely.

This leads to the following requirements:

* By default, all messages are cleaned up as soon as all recipients have successfully retrieved the message or 56 days after they have been sent, whichever comes first.

A Koppeltaal administrator can configure exceptions to this rule:

* A Koppeltaal administrator can specify a default maximum message age per message type per domain. This maximum age cannot be greater than 56 days.
* A Koppeltaal administrator can specify per domain whether or not a specific message type is cleaned up as soon as all recipients have successfully retrieved the message.
* A Koppeltaal administrator can specify that for a specific application a specific message type may not be cleaned up. This means that in any domains that the specified application is part of the specified message type is never cleaned up, unless a manual cleanup is triggered.

It is important that messages to not simply disappear from the Koppeltaal Server without a trace, since this will cause confusion and possibly data corruption in the connected applications. This leads to the addition of one more requirement:

* If a message has been deleted it must be possible for any connected applications to determine that the message existed previously but is no longer available. This information can be used by the connected application to inform the patient and/or caregiver about the status of the message.

## Technical implementation

To support future changes to the legal requirements the global maximum message age is configured as a setting in the application config.xml:

```markup
<setting name="global-maximum-message-age" value="56" />
```

The data structure relevant to the requirements listed in the previous section is summarized in the diagram below.

![image alt text](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/image_0.png)

For technical reasons a Koppeltaal message’s body is stored separately from the message’s metadata \(sender, domain, etc\). The body is stored in MessageBodies, while the metadata is stored in the table Messages.

In addition, for each recipient of a message a record is created in the ApplicationMessages table. This table contains the processing status, which indicates whether or not the message was retrieved and if so, whether the message was successfully processed or not.

When the processing status of an ApplicationMessage changes, the following procedure triggers to determine whether or not the message should be cleaned up:

* If there is at least one recipient of this message that has not yet successfully retrieved the message, do nothing.
* If there is an application in this domain for which this type must be retained, do nothing.
* If there exists a record in DomainMessageSettings for this domain and this message type with ‘RetainOnSuccessfulRetrieval’ set to ‘true’, do nothing.
* Delete MessageBody and mark all related ApplicationMessages as being ‘expired’.

In addition, a background process runs daily that performs the following check per Message:

* If there is an application in this domain for which this type must be retained, do nothing.
* If there exists a record in DomainMessageSettings for this domain and messages type and the message is older than the maximum age specified in that message, delete MessageBody and mark all related ApplicationMessages as being ‘expired’.
* If the message is older than the age specified by the ‘default-maximum-message-age’ setting, delete MessageBody and and mark all related ApplicationMessages as being ‘expired’.

An additional attribute is added to the MessageHeader definition to indicate that a message has expired:

| MessageHeader.isExpired |  |
| :--- | :--- |
| Definition | Whether or not the message has expired |
| Control | 0..1 |
| Type | boolean |
| Extension | http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/MessageHeader\#IsExpired |

If an application tries to retrieve a message that has expired they are informed that the message is no longer available. There are two ways for an application to retrieve a message, each requiring a different method of handling messages that have expired.

* Using the GetNextAndClaim functionality.
  * A call to GetNextAndClaim will by default not return any expired MessageHeaders for messages that have expired. Only if the query argument ‘include-expired’ is set to ‘yes’ expired messages will be included.
* Searching on MessageHeader.
  * By default expired messages will not be returned. Only if the query argument ‘include-expired’ is set to ‘yes’ expired messages will be included.

Currently when the Koppeltaal Server returns a Message this message is parsed from the message body. This body includes the MessageHeader. When a message is expired the message body is removed, making the original MessageHeader unavailable.

This means that when an expired message is retrieved the Koppeltaal Server must reconstruct the MessageHeader based on the information in the Message table. This table contains all relevant data, except the ‘software’ details. These details are not used by Koppeltaal applications, so can be replaced by dummy values.

