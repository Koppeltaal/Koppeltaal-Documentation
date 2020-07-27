# adapters

## Adapters

The following API calls are available:

| API call | Description | Documentation |
| :--- | ---: | :---: |
| Get next message and claim | Retrieves the first unread message and marks it as claimed. | 5 |
| Search for message id | Gets the message with the given id, regardless of its status. | 12 |
| Updating the Processing Status for a Message | Updates the status of the given message. | 234 |
| Retrieve activity definitions | An activity definition describes an activity that is made available by a Device | 234 |
| Storage Service AP | POST PUT GET & DELETE for item management | 234 |

## The following API calls are available:

| API call | Description | Documentation |
| :--- | ---: | :---: |
| CreateOrUpdateUserMessage | This message represents a text message sent from one user to another. | - |
| CreateOrUpdateCarePlan | This message is sent when a CarePlan or one of its contained activities has been changed. This may also mean that the status of one of the contained activities changed. | - |
| UpdateCarePlanActivityStatus | This message is sent when the status of an activity changes. Note that this message does not include the result of the activity. | - |
| CreateOrUpdateCarePlanActivityResult | This message is sent when a result for a CarePlanActivity becomes available or is changed. | - |
| CreateOrUpdatePatient | This message is sent when a result for a new or updated Patient. | - |
| CreateOrUpdatePractitioner | This message is sent when a result for a new or updated Practitioner. | - |
| CreateOrUpdateRelatedPerson | This message is sent when a result for a new or updated Activity Definition. | - |
| CreateOrUpdateActivityDefinition | This message is sent when a result for a new or updated Practitioner. | - |
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

## Coverage

| Functional item | Coverage | Documentation |
| :--- | ---: | :---: |
| Launch Sequence | - | - |
| Activation Code | - | - |
| Activation Code | - | - |
| Create or Update Care Plan | - | - |
| UpdateCarePlanActivityStatus | - | - |
| CreateOrUpdateCarePlanActivityResult | - | - |
| Activity Definition | - | - |
| User Message | - | - |
| Create or Update Patient | - | - |
| Create or Update Practitioner | - | - |
| Create or Update RelatedPerson | - | - |
| Storage API | - | - |

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

## Usage:

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

  > **Tip:** **Extesnion** details including :
  >
  > * FHIR Library inclusion
  > * Extended Atom reosurces

