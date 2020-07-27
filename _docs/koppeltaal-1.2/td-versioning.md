---
title: Versioning
category: Technical Designs
order: 3
---

# TD-versioning

Author: Bart Mehlkop Datum: 03-03-2017 Versie: 0.1

## Version management

| Versie | Datum | Auteur | Aanpassingen |
| :--- | :--- | :--- | :--- |
| 0.1 | 02-12-2016 | Bart Mehlkop | First Draft |

## Table of content

\[\[TOC\]\]

## Versioning

In Koppeltaal, all messages indicate an update to or creation of a resource. Since multiple applications may have an internal copy of a resource, applications must be aware of which version of the resource they are updating. Otherwise they risk overwriting changes made by another application. In order to guard against this type of error Koppeltaal uses a versioning system.

Koppeltaal will override any unprocessed older versions of messages that are still in a queue when a new version is received. This is done to reduce the number of messages an application has to parse.

Note that this means that an application can not rely on receiving any intermediate messages. For example, it is not guaranteed that a client portal receives status updates of an activity for each change from ‘available’ to ‘in progress’ to ‘finished’. If the activity is started and finished before the client portal retrieves its messages, any UpdateCarePlanActivityStatus messages \(as well as any triggered CreateOrUpdateCarePlan messages\) will list the activity status as ‘finished’ instead of ‘in progress’.

## Sending a message

Each message received by the Koppeltaal is given a version. Any other applications that sends the same type of message for a resource must subscribe to that type of message in order to keep the internally stored resource up to date.

Each message must specify what version is the latest known to the sending application. The Koppeltaal will check this version against the latest version that is has received and reject a message if the versions do not match. This is known as a concurrent modification error.

## Obtaining the current version number

An application must provide the version of the resource that the update was based on when sending a message. There are two ways to obtain this number, each for a different situation.

When sending a message, the Koppeltaal Server will return the generated version number as part of the reply. The application may store the returned version number to re-use later.

If there are multiple applications that may send messages with the same focal resource, each will have to subscribe to the message type in order to receive updates \(and their version numbers\) from the other applications.

When a resource is updated for the first time the sending application should specify no version number. When a resource is first created the sending application does not yet know a version. In that case the sending application should not specify the version number and the Koppeltaal will generate the first version. If another version is already known the Koppeltaal will reject the message in the same way as if an out-of-date version was given.

