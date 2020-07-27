---
title: Adapter specifications
category: User Guides
order: 2
---

# adapters

## Adapters

\[\[TOC\]\]

Adapters are main building blocks of the Koppeltaal architecture. As the main protocol is FHIR/Koppeltaal the adapters induces an abstraction layer that helps quick development. Each adapter is build for a specific programming language \(C\#, Python, PHP, Java, Android, iOS, JS\) and moves the Koppeltaal FHIR REST API into specific implementation language.

Questions and answers:

1. What can an Adapter offer as added value?  implementing the REST API Calls and Koppeltaal specific protocol into a dedicated programming language library.
2. What do I need to do to get an adapter for my need? A subscription to Koppeltaal and access to Koppeltaal GIT. 

   3 What is maturity level of the adapters? Adapters are community projects so the level of maturity depends on their usage. An adapter that is largely used has more functionality then an adapter that is less used. A maturity matrix is provided here. 

The following message types are available as part of the Adapter implementation.

| API call | Description | Documentation |
| :--- | ---: | :---: |
| Get next message and claim | Retrieves the first unread message and marks it as claimed. |  |
| Search for message id | Gets the message with the given id, regardless of its status. |  |
| Updating the Processing Status for a Message | Updates the status of the given message. |  |
| Retrieve activity definitions | An activity definition describes an activity that is made available by a Device |  |
| Storage Service AP | POST PUT GET & DELETE for item management |  |

## Main API calls

| API call | Description | Documentation |
| :--- | ---: | :---: |
| CreateOrUpdateUserMessage | This message represents a text message sent from one user to another. | - |
| CreateOrUpdateCarePlan | This message is sent when a CarePlan or one of its contained activities has been changed. This may also mean that the status of one of the contained activities changed. | - |
| UpdateCarePlanActivityStatus | This message is sent when the status of an activity changes. Note that this message does not include the result of the activity. | - |
| CreateOrUpdateCarePlanActivityResult | This message is sent when a result for a CarePlanActivity becomes available or is changed. | - |
| CreateOrUpdatePatient | This message is sent when a result for a new or updated Patient. | - |
| CreateOrUpdatePractitioner | This message is sent for a new or updated Practitioner. | - |
| CreateOrUpdateRelatedPerson | This message is sent for a new or updated Activity Definition. | - |
| CreateOrUpdateActivityDefinition | This message is sent for a new or updated Practitioner. | - |
| POST \[Koppeltaal Server\]/FHIR/Koppeltaal/Binary | Stores a new item. The body of the request must contain a Binary resource. | - |
| PUT \[Koppeltaal Server\]/FHIR/Koppeltaal/Binary/\[id\] | Updates an existing entry. | - |
| GET \[Koppeltaal Server\]/FHIR/Koppeltaal/Binary/{\[id\]}?patient=\[patient-id\]{&search-arguments} | Gets any stored items that match the given id or the search arguments. | - |
| DELETE \[Koppeltaal Server\]/FHIR/Koppeltaal/Binary/{\[id\]}?patient=\[patient-id\]{&search-arguments} | Deletes any stored items that match the given id or the search arguments. | - |

## Functionality

| Functional item | Description | Documentation |
| :--- | ---: | :---: |
| Launch sequence | Koppeltaal Single Sign-On is based on the OAuth2 standard, and implemented as recommended by the SMART-on-FHIR initiative. | - |
| Server metadata | The conformance statement gives general information about the Koppeltaal Server. | - |

## Support for Mobility

| Functional item | Description | Documentation |
| :--- | ---: | :---: |
| Activation code sequence | Distributed authentication - for supporting mobile clients. | - |
| Refresh Token | Security improvement for mobile integration. | - |

## Support  for Storage

| Functional item | Description | Documentation |
| :--- | ---: | :---: |
| Storage Service API | To support applications that do not have their own backend structure the Koppeltaal Server provides an API to store and retrieve data. | - |

## Coverage/Maturity Matrix

| Functional item | C\# | Java | Android \(Java\) | Python 2.7/3.6 |
| :---: | :---: | :---: | :---: | :---: |
| Launch Sequence | YES | YES | YES | YES |
| Activation Code | NA | NA | YES | NA |
| Conformance Statement | YES | YES | YES | YES |
| Create or Update Care Plan | YES | YES | YES | YES |
| UpdateCarePlanActivityStatus | YES | YES | YES | YES |
| CreateOrUpdateCarePlanActivityResult | YES | NO | NO | YES |
| Activity Definition | YES | YES | YES | YES |
| User Message | YES | NO | NO | NO |
| Create or Update Patient | YES | YES | YES | YES |
| Create or Update Practitioner | YES | YES | YES | YES |
| Create or Update RelatedPerson | YES | YES | YES | NO |
| Storage API | YES | NO | NO | NO |

## Development \(ReadMe File Template\)

* Language support
* e.g. Java

  > **Tip:** Provide here input for **language** of choice with the expected level of details:
  >
  > * version XXX
  > * special libraries used

* Code Structure

  ```text
    e.g.
    -    SRC
    -    TEST
  ```

  > **Tip:** Provide here input for **code structure** chosen with the expected level of details:
  >
  > * SRC - &gt; lib's etc

* Version Support:
  * TESTed on Java X and Android Y 

> **Tip:** **Version support** details including where can it be compiled and executed:
>
> * SRC - &gt; lib's etc

## Usage requirements

* Build: how to build …

  > **Tip:** **BUILD DETAILS** details on creating the library - what you need to use to be able to build this project?

* Configure:

> **Tip:** **Configuration** details including :
>
> * How to configure the connection with the Koppeltaal server
>   * How to configure the compiled library

* Test: how to test

  > **Tip:** **Test** details including :
  >
  > * How to test the connection with/without the Koppeltaal server
  >   * How to configure the compiled library

* Example of integration 

  > **Tip:** **Complete Integration** details including :
  >
  > * How to include the library in a solution
  >   * How to embed in the solution in a given context

* Test: how to extend the libary 

  > **Tip:** **Extension** details including :
  >
  > * FHIR Library inclusion
  > * Extended Atom reosurces

