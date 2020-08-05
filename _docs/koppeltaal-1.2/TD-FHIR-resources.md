---
title: Activity Definitions
category: Technical Designs
order: 3
---

# TD-FHIR-resources

Author: Bart Mehlkop Datum: 03-03-2017 Versie: 0.1

## Version management

| Versie | Datum | Auteur | Aanpassingen |
| :--- | :--- | :--- | :--- |
| 0.1 | 02-12-2016 | Bart Mehlkop | First Draft |

## Table of content

\[\[TOC\]\]

## Retrieving and updating activity definitions

An application GETs activity definitions from [https://koppeltaal.nl/FHIR/Koppeltaal/Other/\_search?code=ActivityDefinition&\[includearchived=yes](https://koppeltaal.nl/FHIR/Koppeltaal/Other/_search?code=ActivityDefinition&[includearchived=yes)\]. All ActivityDefinitions that are available in the application's domain are returned. These ActivityDefinitions can subsequently be assigned as ActivityDefinition in a CarePlan.activity. If the argument 'includearchived' is set to 'yes' any ActivityDefinitions that were archived are also returned.

To create or update an ActivityDefintion, an application should POST or PUT an ActivityDefinition to [https://koppeltaal.nl/FHIR/Koppeltaal/Other](https://koppeltaal.nl/FHIR/Koppeltaal/Other). Do not send a CreateOrUpdateActivityDefinition back to the Koppeltaal Server, this will not work because the Koppeltaal Server does not do any functional processing of incoming messages.

