---
title: Subscription Model
category: Technical Designs
order: 3
---

# TD-subscription-model

Author: Bart Mehlkop Datum: 03-03-2017 Versie: 0.1

## Version management

| Versie | Datum | Auteur | Aanpassingen |
| :--- | :--- | :--- | :--- |
| 0.1 | 02-12-2016 | Bart Mehlkop | First Draft |

## Table of content

\[\[TOC\]\]

## Receiving a notification when a new message becomes available

The Koppeltaal Server offers a SignalR/Web hooks hub that sends a notification when a new message becomes available.

To connect:

* Create a HubConnection to the Koppeltaal Server. The server URL can be used as the hub URL, i.e. [https://edgekoppeltaal.vhscloud.nl](https://edgekoppeltaal.vhscloud.nl). Both basic and token authentication can be used.
* Create a HubProxy for the hub named 'KoppeltaalHub'.
* Subscribe to the 'NewMessage' event.
* Send event 'StartPush' to the hub to begin receiving new message notifications.

The event only informs the application that there is a new message, the message must be retrieved using the existing GetNextAndClaim functionality.

