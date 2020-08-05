---
title: User Guide - Release Flow
category: User Guides
order: 2
---

# UG-release-flow

## Project test & release flow

There are many parties that are affected when a new version of Koppeltaal is released. Therefor it is very important that there is a rigorous procedure to manage each release cycle. Below is a schematic overview of the flow of tests and releases.

![Release flow](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/Koppeltaal_Test_&_Release_Flow_V2_-_resized.jpg)

## There are three types of parties that are involved in the release of a new Koppeltaal server version:

Koppeltaal server itself. Applications \(clients\) that send and receive messages via the Koppeltaal server. Connectors that the clients use to transform the messages from XML or JSON into their native language \(C\#, Python etc\). In addition to the development cycle of the Koppeltaal server, each client and connector has a development cycle of their own. The Koppeltaal release and test flow aims to test each unit separately and only after its dependencies have passed their own tests. This way, any issues are found as quickly as possible and at their source and time and effort spent to track them down is minimized.

The test flow consists of the stages described below. Each stage is only started after the tests of the stage before it have passed successfully and indicate no more issues.

Koppeltaal Server regression tests

The Koppeltaal Server regression tests are applied to the Koppeltaal Server. This test is designed to verify whether the changes to the software have not caused any unintended changes to the functionality of the server as a whole.

Load and performance test

The Koppeltaal Server load and performance tests are used to safeguard the minimum response time of the Koppeltaal server, as well as to find any issues that arise due to high load. Only after this test suite has been completed the Koppeltaal server software is released for integration tests with connectors and Koppeltaal clients.

Connector test

The development cycle of a connector is the responsibility of the developer of that connector. However, in order to be able to guarantee the correctness of every connector all connectors are required to pass the Koppeltaal connector acceptance tests.

Only after this test is passed, a connector can be released for integration tests with Koppeltaal clients.

Client test

The development cycle of each client application is the responsibility of the developer of that client. Stichting Koppeltaal can provide a domain on a Koppeltaal server to be used for testing the integration between the client and the Koppeltaal server.

In order to verify the correctness of the integration between the clients in a domain the Koppeltaal client acceptance tests are performed. If any issues are found they are fixed, and any component that is changed must be run through all preceding tests for that component again.

## Project release planning

Delivery Team handles the release process, via Support, and verifies the process:

* Announcement of the expected release date  and notes via Slack and Mailing List
* Release version check in GIT HUB \(Koppeltaal repository\)
* Code completion and Code standards
* Unit Test completed

![Delivery flow](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/Delivery.png)

## Handover process to Release Team

* Update from GIT - follow the Deployment document
* Deployment&Configuratiom

  Deployment Guide Koppeltaal  Deployment\_Guide\_Koppeltaal\_XXX

* Validate release documentation: API documentation
* Validate Schemas and profiles
* Preparation Load and Performance Test 
* Execution Load and Performance Test
* Preparation Regression Test
* Execution Regression Test
* Go live acceptance and procedure

## Release planning

When the Koppeltaal core team decides to release a new version, the planning is determined as follows.

| Action | Duration | Performed by |
| :--- | :--- | :--- |
| Decision to release | - | KT Core Team |
| Make release notes | - | Development Team |
| Regression test is run | - | Development Team |
| Perfomance test is run | - | Development Team |
| Concept planning is shared with the community | - | Support |
| Migration to Edge/Test environment | - | Development Team |
| Start ACC tests by community | 2 weeks | Community |
| Final planning is shared with the community | - | Support |
| Rework on issues from ACC tests | 1 week | Development Team |
| Live update preparation | 1 week | Support/hosting teams |

Taken together, this means that after the decision to release, the following milestones occur:

| Item | Date |
| :--- | :--- |
| Start ACC tests | as soon as practical \(rework starts as soon as issues are reported\) |
| End ACC tests | 2 weeks after start |
| End rework | 3 weeks after start |
| Live update | 4 weeks after start |

