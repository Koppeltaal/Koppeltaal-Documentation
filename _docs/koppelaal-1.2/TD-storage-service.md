---
title: Storage Service
category: Technical Designs
order: 1
---

Author: Bart Mehlkop
Datum: 03-03-2017
Versie: 0.1

# Version management

<table>
<tr>
<td>Versie</td>
<td>Datum</td>
<td>Auteur</td>
<td>Aanpassingen</td>
</tr>
<tr>
<td>0.1</td>
<td>02-12-2016</td>
<td>Bart Mehlkop</td>
<td>First Draft</td>
</tr>

</table>

# Table of content

[[TOC]]

# Storing data in the storage service
If an application does not have its own back end and database it can use the Storage Service that has been configured for the domain it is in. To store or retrieve, the endpoint https://koppeltaal.nl/FHIR/Koppeltaal/Other?code=StorageItem can be used.

This endpoint supports the following operations:

POST [Koppeltaal Server]/FHIR/Koppeltaal/Other?code=StorageItem 
Stores a new item. The body of the request must contain a StorageItem resource.
PUT [Koppeltaal Server]/FHIR/Koppeltaal/Other/[id]?code=StorageItem 
Updates an existing entry. The argument 'id' must be the server-generated id of the stored item. The body of the request must contain a StorageItem resource.
GET [Koppeltaal Server]/FHIR/Koppeltaal/Other/{[id]}?code=StorageItem&patient=[patient-id]{&search-arguments} 
Gets any stored items that match the given id or the search arguments.
The following arguments are supported:

_id (system assigned ID) - is equal to
Object Type - is equal to
Object Key - is equal to / starts with / contains
LastUpdated (filter) - is equal to / is greater than / is greater than or equal / is less than / is less than or equal
LastUpdated (sort ascending or descending)
DELETE [Koppeltaal Server]/FHIR/Koppeltaal/Other/StorageItem:{[id]} 
Deletes any stored items that match the given id.
