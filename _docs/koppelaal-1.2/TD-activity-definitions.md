---
title: FHIR recources
category: Technical Designs
order: 3
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

# FHIR - basic rules
Every Application must define a unique FHIR Base URL, which is the basis on which resource URLs are created, for example https://xxx.jouwomgeving.nl/fhir .

Every resource added to a message must have a unique Url, which is constructed as follows:

FHIR Base Url + “/” + Resource Type + “/” + id + “/_history/” + version id

Bijvoorbeeld https://xxx.jouwomgeving.nl/fhir/Patient/32324/_history/812909

The version id can be an automatically incremented number, but this is not required.

Koppeltaal FHIR profiles

Koppeltaal will define a FHIR Profile for each defined message event, where the verb-part is left out. In other words, the profile for CreateOrUpdatecarePlan will have as identifier http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/CarePlan. Furthermore, a profile will be defined for common parts like MessageHeader, Patient, Practictioner and Relatedperson, since these are reused over multiple messages. This leads to the following list of profiles for Koppeltaal:

[[#|]][[#|]]

|Resource	|Profile |identifiers
--------|---------|--------------|
| ActivityDefinition	 | http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/|ActivityDefinition
| Device	| http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/Application |
| MessageHeader	| http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/|MessageHeader
| Patient	| http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/Patient|
| Practitioner	| http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/ |Practitioner
| RelatedPerson	| http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/|RelatedPerson
| Person	| http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/Person |
| CarePlan	| http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/CarePlan |
| CarePlanActivityStatus	| http://ggz.koppeltaal.nl/fhir/Koppeltaal/ |Profile/CarePlanActivityStatus
| CarePlanActivityResult |	http://ggz.koppeltaal.nl/fhir/Koppeltaal/ |Profile/CarePlanActivityResult
| UserMessage	| http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/ |UserMessage

Normally, FHIR requires clients to indicate which profile is intended to be used. for Koppeltaal, the Koppeltaal Server will validate messages against the profiles defined here independent of the profiles a resource is tagged with.

