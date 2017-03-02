---
title: Activity Definitions
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

# Retrieving and updating activity definitions
An application GETs activity definitions from https://koppeltaal.nl/FHIR/Koppeltaal/Other/_search?code=ActivityDefinition&[includearchived=yes]. All ActivityDefinitions that are available in the application's domain are returned. These ActivityDefinitions can subsequently be assigned as ActivityDefinition in a CarePlan.activity. If the argument 'includearchived' is set to 'yes' any ActivityDefinitions that were archived are also returned.

To create or update an ActivityDefintion, an application should POST or PUT an ActivityDefinition to https://koppeltaal.nl/FHIR/Koppeltaal/Other. Do not send a CreateOrUpdateActivityDefinition back to the Koppeltaal Server, this will not work because the Koppeltaal Server does not do any functional processing of incoming messages.

