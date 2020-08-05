---
title: Support API
category: Technical Designs
order: 4
---

# TD-support-api

Author: Bart Mehlkop Datum: 2-11-2016 Versie: 0.1

## Version management

| Versie | Datum | Auteur | Aanpassingen |
| :--- | :--- | :--- | :--- |
| 0.1 | 22-11-2016 | Bart Mehlkop | First Draft |

## Table of content

\[\[TOC\]\]

## Introduction

In the context of the proposed Koppeltaal Administration Portal it is necessary that the central support portal can connect to the various Koppeltaal Server installations. Each Koppeltaal Server installation exposes an API that can be used to retrieve debugging and performance information. The Koppeltaal Server also accepts new configuration for applications and domains via the API.

There are a number of requirement the administration API must fulfill:

* Allow all operations that an application admin has access to via the application administration portal on the Koppeltaal Server itself.
* Provide debugging information, including
* Version information
* Information about sent messages
  * Sender
  * Receiver
  * Timestamp
  * Domain
  * Status
* The API must be versioned, so that the central administration portal can communicate with the different versions of the Koppeltaal Server

## Domain model

The domain model of the administration portal obviously mirrors the domain model of the Koppeltaal Server.

![Domain model](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/Domain%20model.png)

| ActivityDefinition | A type of activity that is offered by an Application. |
| :--- | :--- |
| Application | A software package installed on a server that offers its functionality through Koppeltaal. |
| ApplicationAdministrator | A user responsible for the configuration of one or more Applications. |
| ApplicationInstance | A connection between an Application and a Domain. |
| ApplicationInstanceUser | The identity/credentials used by an Application to connect to a specific Domain. |
| Authorization | Describes the allowed launch properties. |
| Domain | The context in which patient data is exchanged. Usually a health care institution. |
| DomainAdministrator | A user responsible for the configuration of one or more Domains. Mainly involves configuring which applications are connected to that domain. |
| DomainConnectionRequest | A request for an application to be connected to the specified domain. |
| NewApplicationRequest | A request for a new application to be added to the server. |
| RegisteredClient | Describes the OAuth details of the application |
| Server | An instance of the Koppeltaal Server |
| SubActivity | The subactivities of an ActivityDefinition. |
| SubscriptionsPerApplication | The subscribed message types per application. |

## Responsibilities

Each type of role has a specific responsibility.

| Role | Responsibilities |
| :--- | :--- |
| System administrator | Manages system-wide configuration, such as the Conformance Statement. Additionally, accepts request for administrator accounts, new applications and domains. |
| Application administrator | Manages one or more applications, such as configuring Single Sign-on settings and Activity Definitions. |
| Domain administrator | Manages one or more domains, such as accepting connection requests from applications. |

## API

The Koppeltaal Server exposes a REST API, accepting and sending JSON data. The API is based on the object described in the domain model above. The endpoint of the API is:

```text
<Koppeltaal Server URL>/jsonapi/Koppeltaal
```

Each resource can be accessed via the URL

```text
<endpoint>/<resourcename>.
```

For example, application information for an application on Koppeltaal Edge can be accessed at

```text
https://edgekoppeltaal.vhscloud.nl/jsonapi/Koppeltaal/Application
```

Note that not every type supports all operations. Some types disallow updating of specific fields after the resource has been created. This is done in the case that a change in the value of the field would cause related data to become invalid. For example, changing either the domain or application of an application instance would corrupt existing data and as such is not allowed.

| Type \ Operation | POST | PATCH | GET | DELETE |
| :--- | :--- | :--- | :--- | :--- |
| ActivityDefinition | Supported | Supported | Supported | Not supported\(1\) |
| Application | Not supported\(2\) | Supported | Supported | Not supported |
| ApplicationAdministrator | Supported | Supported | Supported | Supported |
| ApplicationInstance | Not supported\(3\) | Supported | Supported | Not supported |
| ApplicationInstanceUser | Supported | Supported | Supported | Not supported\(1\) |
| Authorization | Supported | Supported | Supported | Not supported\(4\) |
| Domain | Not supported\(5\) | Not supported | Supported | Not supported |
| DomainAdministrator | Supported | Supported | Supported | Supported |
| DomainConnectionRequest | Supported | Supported | Supported | Supported |
| NewApplicationRequest | Supported | Not supported | Not supported | Not supported |
| RegisteredClient | Supported | Supported | Supported | Not supported |
| Server | Not supported | Not supported | Supported | Not supported |
| SubActivityDefinition | Supported | Supported | Supported | Not supported\(1\) |
| SubscriptionsPerApplication | Supported | Not supported | Supported | Supported |

1: Update the record with IsActive set to ‘false’ instead.

2: Insert a NewApplicationRequest to request a new application instead.

3: Insert a DomainConnectionRequest to request a new application instance instead.

4: Update the record with GrantStatus set to ‘Revoked’ instead.

5: Insert a DomainRequest to request a new domain instead.

## Flow

Below is a diagram visualizing the different process for which the Support API is intended. The dotted connections indicate parts of the process that can be performed using the descriped REST operation.

Requesting a new application administrator account:

![Process Flow: Request new application administrator account](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/Process%20flow%20-%20New%20Application%20Admin.png)

Registering a new application:

![Process Flow: Register new application](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/Process%20flow%20-%20New%20Application.png)

Requesting a new domain:

![Process Flow: Request new domain](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/Process%20flow%20-%20New%20Application.png)

Requesting a connection to a domain for an application:

![Process Flow: Request new application connection](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/Process%20flow%20-%20New%20Application%20Connection.png)

## Data format

The JSON API specification specifies a document structure that is used to send data from the server to the client and vice versa. There are basically three types of top level documents:

* The response document: sent from the server to the client when data needs to be send to the client
* The error response document: sent from the server to the client and includes error information
* The request document: sent from the client to the server to create or update resources

### The response document

The response document contains all data requested by the client. The response can look like:

```text
{
    "data":…,
    "jsonapi":{
        "version": "1.0"
    },
    "meta":{…},
    "links":{…},
    "included":[…]
}
```

The data property can contain a single Resource objects, null, a collection of Resource objects or an empty collection. The link property can contain the following members:

* self: The url that can be used to get the current response document
* related: A related resource link when the data represents a resource relationship \(more about this can be read in "Fetching relationships"\)
* first, prev, next, last: The pagination links, pointing to a specific page.

The 'included' property is an array of Resource Objects, but can also be empty when there are no resources to include.

### The error response document

An error response document will be returned whenever a problem occurs in the JSON Rest API. If possible, multiple errors will be returned, this will be the case when requests are validated. When multiple errors are returned, the status code of the response will be set to 400 by default, when just one error is returned, the status code of the response will be the same as the status code of the error.

```text
{
    "errors":[
        {"status": "404", "title": "Resource not found"}
    ],
    "jsonapi":{
        "version": "1.0"
    }
}
```

### The request document

A request document can only contain a data member, which can contain a Resource object, null, a collection of Resource objects or an empty collection.

### Resource objects

Resource objects contain all the data of a resource, including relationships. They are used to send data from the server to the client, but the client uses them as well to create or update resources. Resource objects are also used to identify relationships, for this only the type and id members are used.

| Member | Description |
| :--- | :--- |
| type | The type of the resource. |
| id | The IID of the resource, should be omitted when the resource is used to create a new resource. |
| attributes | The data of the resource |
| meta | Additional information like the version of the resource. |
| links | The links related to this resource, can be omitted the resource is send to the server. |

For example:

```text
{
    "type": "Patients",
    "id": "1",
    "attributes: {
        "Name": "Mr. Smith",
        "Age": 50
    },
    "links": {
        "self": "https://petrel/TestProject/Patients/1"
    }
}
```

### Creating resources

A resource is Created bij POSTing a resource to the endpoint of the resource. The request should NOT include an id member. For example:

```text
POST https://petrel/jsonapi/TestProject/Patients
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
    "data":{
        "type": "Patients",
        "attributes":{
            "Name": "Miss. Smith",
            "Age": 47
        }
    }
}
```

### Updating resources

Resources are updated using a PATCH request. This request contains only the attributes of the type that are to be changed. Attributes that are not present will not be updated, so to clear an existing attribute the value ‘null’ should be sent.

```text
PATCH https://petrel/jsonapi/TestProject/Patients/2
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
    "data":{
        "type": "Patients",
        "id": "2", 
        "attributes":{
            "Name": "Mrs. Smith"
        },
        "meta": {
            "version": "2016-10-11T14:02:37:846.6426"
        }
    }
}
```

### Deleting resources

A resource can be deleted by sending a DELETE request to the URL of the resource.

```text
DELETE https://petrel/jsonapi/TestProject/Patients/2
```

### Retreiving resources

Fetching a collection of resources, for example to show patients in a list, can be done by using the following request:

```text
GET https://petrel/jsonapi/TestProject/Patients
```

This will return the first 15 patients in the following document:

```text
{
    "data":[
        …
    ],
    "jsonapi":{
        "version": "1.0"
    },
    "meta":{
        "page":{
            "number": 1,
            "size": 15,
            "total-records": 20
        }
    },
    "links":{
        "self": "https://petrel/jsonapi/TestProject/Patients?page[number]=1&page[size]=15",
        "next": "https://petrel/jsonapi/TestProject/Patients?page[number]=2&page[size]=15",
        "last": "https://petrel/jsonapi/TestProject/Patients?page[number]=2&page[size]=15"
    }
}
```

Note: The given URLs are normally URL encoded, but are changed here for readability

#### Retrieving a single resource

In order to fetch a single resource, for example to show the details of a patient, the IID of the resource should be added to the URL:

```text
GET https://petrel/jsonapi/TestProject/Patients/1
```

Which will give the following result:

```text
{
    "data":{
        "type": "Patients",
        "id": "1",
        "attributes":{…},
        "relationships":{…},
        "links":{
            "self": "https://petrel/jsonapi/TestProject/Patients/1"
        },
        "meta": {
            "version": "2016-10-11T14:02:37:846.6426"
        }
    },
    "jsonapi":{
        "version": "1.0"
    },
    "links":{
        "self": "https://petrel/jsonapi/TestProject/Patients/1",
    }
}
```

#### Pagination

The JSON Rest API applies pagination by default to limit the number of resources that are send to the client. Pagination can be controlled by setting the following query parameters:

* page\[number\]: the page that the client wants, default: 1
* page\[size\]: the number of records per page, default: 15

In the response document, the following links are added when they are available:

* first: the first page of data
* prev: the previous page of data
* next: the next page of data
* last: the last page of data

In the meta object of the document, information about the pagination is added:

* page.number: the current page
* page.size: the current page size
* page.total-records: the total number of records for this type

```text
{
    "meta": {
        "page": {
            "number": 2,
            "size": 10,
            "total-records": 30
        }
    }
}
```

#### Filtering

In order to filter the result, the filter query parameter can be used. The following examples shows the basic usage of filters:

```text
GET https://petrel/jsonapi/TestProject/Patients?filter[Name]="Jansen"
```

By default equals is used for filtering, but other search operators are also supported. To specify the search operator, an extra parameter should be added to the filter query parameter. The following example shows how to do this:

```text
GET https://petrel/jsonapi/TestProject/Patients?filter[Name][eq]=Jansen
```

The following search operators are supported:

| search operator | Description | Example |
| :--- | :--- | :--- |
| eq | Equals | /Patients?filter\[Name\]\[eq\]=Jansen |
| in | Same as Equals | /Patients?filter\[Name\]\[eq\]=Jansen |
| ne | Not equal | /Patients?filter\[Name\]\[ne\]=Jansen |
| not | Same as Not equal | /Patients?filter\[Name\]\[not\]=Jansen |
| gt | Greater than | /Patients?filter\[Age\]\[gt\]=18 |
| ge | Greater than or equal to | /Patients?filter\[Age\]\[ge\]=18 |
| lt | Less than | /Patients?filter\[Age\]\[lt\]=18 |
| le | Less than or equal to | /Patients?filter\[Age\]\[le\]=18 |
| contains | Contains | /Patients?filter\[Name\]\[contains\]=ans |
| startswith | Starts with | /Patients?filter\[Name\]\[startswith\]=J |

The operator for Equals and Not equals support multiple values and are handled as OR. This is shown in the following example:

```text
GET https://petrel/jsonapi/TestProject/Patients?filter[Name][eq]=Jansen,Janssen
```

Besides filtering on attributes of the selected backend type, attributes of related resources can also be filtered:

```text
GET https://petrel/jsonapi/TestProject/Patients?filter[Caregiver.Name][eq]=Docter John
```

Combining multiple filters is also supported.

```text
GET https://petrel/jsonapi/TestProject/Patients?filter[Caregiver]=1&filter[CaregiverName]=Jansen
```

Combining multiple filters that are exactly the same, are handled as an OR as well. The following two examples are handled the same:

```text
GET https://petrel/jsonapi/TestProject/Patients?filter[Name][eq]=Jansen&filter[Name][eq]=Janssen
```

```text
GET https://petrel/jsonapi/TestProject/Patients?filter[Name][eq]=Jansen,Janssen
```

#### Full text query

The "search" query parameter may be used to pass a full text query. Only a single, argumentless search parameter is allowed.

```text
GET https://petrel/jsonapi/TestProject/Patients?search=Janssen
```

It is possible to combine the full text query with additional filters:

```text
GET https://petrel/jsonapi/TestProject/Patients?search=Janssen&filter[Caregiver]=1
```

The full text query will be handled by the full text search mechanism that is enabled on the type.

