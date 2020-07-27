---
title: Koppeltaal Design
category: Technical Designs
order: 3
---

# specification

## Introduction

This Technical Design has been written to describe the technical scope of Koppeltaal 1.2.

The concept of the Koppeltaal Server is created to support the interaction between portals and e-interventions via a standard protocol.

The Koppeltaal Server is a system that works like a mailbox. All the registered applications \(e-interventions and portals\) can drop messages in the mailbox. The Koppeltaal Server routes the message to the subscribed application queues. The subscribed applications can take the messages for their own use.

## Ontology

Koppeltaal talks about information on two levels. On the higher level, Koppeltaal defines entities in health care, describing the content of the messages that are sent through the Koppeltaal Server. This level is described in the [message content ontology](specification.md#message-content-ontology).

On the lower level, Koppeltaal defines an infrastructure for exchanging messages between the various connected applications. This level is described in the [infrastructure ontology](specification.md#infrastructure-ontology).

### Message content ontology

The information that is sent through the Koppeltaal Server can be broken down in so-called resources. Each resource contains a structured set of data that describes a concept or entity about which information needs to be exchanged.

Resources are described using the FHIR standard. FHIR is a specification of entities often used in healthcare and a protocol to exchange information about these entities between systems. Read more about FHIR at [&lt;http://www.hl7.org/implement/standards/fhir/index.html&gt;](http://www.hl7.org/implement/standards/fhir/index.html).

The table below shows the mapping from the entities described in the functional ontology to the available FHIR resources.

| Koppeltaal entity | FHIR resource |
| :--- | :--- |
| Activity | `Other` \(CarePlanActivity\) |
| ActivityProvider | _Not mapped. Any application can provide activities. This is specified by the ActivityDefinitions an application makes available._ |
| Application | `Device` |
| Caregiver | `Practitioner` |
| Carepath | `CarePlan` |
| Client | `Patient` |
| Intervention | _Not mapped. An intervention is a type of activity._ |
| Person | _Not mapped. Information about people is sent as one of the specific_ roles: `Patient`, `Practitioner` or `RelatedPerson`. |
| Portal | _Not mapped. A portal is kind of application._ |
| Related person | `RelatedPerson` |
| Result | DiagnosticResport \(but significantly extended. See [CarePlanActivityResult](specification.md#h.9vq3ttcw353y)\) |
| Role | _Not mapped. A person’s role is implied by the type of resource used. I.e., a person acting in the role of caregiver will be sent as a resource of type Practitioner._ |
| ROM | _Not mapped. A ROM is a kind of activity._ |
| Screener | _Not mapped. A screener is a kind of activity._ |
| Treatment | _Not mapped. The treatment is implicit in the CarePlans assigned to a Patient._ |

Note that in the ontology below some concepts from the full functional ontology have been omitted because they are implicit. In particular, the different types of activity that are known have been abstracted into ‘ActivityDefinition’. This allows the Koppeltaal Server to relay information about any type of activity, including any future activity types.

### Infrastructure ontology

The Koppeltaal Server acts only as a message router and filter. This means that the domain model can be very simple.

![](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/image02.png)

There are four entities in the ontology:

* Application
  * A party that wishes to communicate through the Koppeltaal Server.
* Domain
  * Each application is part of one or more domains. The domain is mainly added to the domain model for security reasons. This is explained in the paragraph ‘[Security](specification.md#Security)’
* Message
  * A message can be published in a domain. Only applications in that domain can receive the message.
* MessageType
  * Each message has a type. An application will not receive messages of a type they have not registered for.

```markup
<html>
  <body>
    <a href="#">Hello world</a>
  </body>
</html>
```

```markup
<html>
  <body>
    <a href="#">Hello world</a>
  </body>
</html>
```

```javascript
 {
     "access_token": "f3d421f4-d036-468a-b9aa-de9c777ede95",
     "token_type": "Bearer",
     "expires_in": 900,
     "refresh_token": "e54a2533-df44-4e32-bc4d-820c05b2aed0",
     "scope": "patient/*.*",
     "patient": "https://ggz.example.com/Patient/72308",
     "resource": "https://ggz.example.com/RelatedPerson/452"
 }
```

```python
def helloworld():
    print("hello world")
```

```text
def helloworld():
    print("hello world")
```

```csharp
int i = 1;
switch (i) {
  case 1:
    Console.WriteLine("One");
    break;
  case 2:
    Console.WriteLine("Two"); Console.WriteLine("Two");
    break;
  default:
    Console.WriteLine("Other");
    break;
}
```

## Interface description

At the most basic level, applications communicate with the Koppeltaal Server using a REST interface. The interaction between applications and the Koppeltaal Server is described in the diagram below.

![](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/image01.png)

The interface consists of the following operations:

### Retrieving the conformance statement

The conformance statement of the Koppeltaal Server is retrieved through a GET request to \[Koppeltaal Server\]/FHIR/Koppeltaal/metadata.

General information about the FHIR conformance statement can be found at [the FHIR website](https://www.hl7.org/fhir/conformance.html).

The conformance statement of the Koppeltaal Server contains information required for the OAuth2 implementation for the single sign on. See [this page](http://docs.smarthealthit.org/authorization/conformance-statement/) for more information. This list of endpoints has been extended with a Launch Endpoint. This is the complete overview of used extensions that Koppeltaal uses for OAuth2:

| Extension URI | Description |
| :--- | :--- |
| [http://fhir.vitalhealthsoftware.com/Profile/Conformance\#Launch](http://fhir.vitalhealthsoftware.com/Profile/Conformance#Launch) | Identifies the OAuth2 "launch" endpoint for the server. |
| [http://fhir-registry.smarthealthit.org/Profile/oauth-uris\#authorize](http://fhir-registry.smarthealthit.org/Profile/oauth-uris#authorize) | Identifies the OAuth2 "authorize" endpoint for the server. |
| [http://fhir-registry.smarthealthit.org/Profile/oauth-uris\#token](http://fhir-registry.smarthealthit.org/Profile/oauth-uris#token) | Identifies the OAuth2 "token" endpoint for the server. |

In addition, the Koppeltaal Server defines 4 extensions that control validation of requests and replies:

| Extension URI | Type | Description |
| :--- | :--- | :--- |
| [http://fhir.vitalhealthsoftware.com/Profile/Conformance\#ValidateRequestsAgainstSchema](http://fhir.vitalhealthsoftware.com/Profile/Conformance#ValidateRequestsAgainstSchema) | Boolean | If true, tells the server to validate requests against the XML Schema |
| [http://fhir.vitalhealthsoftware.com/Profile/Conformance\#ValidateRepliesAgainstSchema](http://fhir.vitalhealthsoftware.com/Profile/Conformance#ValidateRepliesAgainstSchema) | Boolean | If true, tells the server to validate replies against the XML Schema |
| [http://fhir.vitalhealthsoftware.com/Profile/Conformance\#ValidateRequestsAgainstProfile](http://fhir.vitalhealthsoftware.com/Profile/Conformance#ValidateRequestsAgainstProfile) | Boolean | If true, tells the server to validate requests against the FHIR Profile |
| [http://fhir.vitalhealthsoftware.com/Profile/Conformance\#ValidateRepliesAgainstProfile](http://fhir.vitalhealthsoftware.com/Profile/Conformance#ValidateRepliesAgainstProfile) | Boolean | If true, tells the server to validate replies against the FHIR Profile |

