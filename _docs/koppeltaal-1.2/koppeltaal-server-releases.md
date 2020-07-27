---
title: Koppeltaal Server Releases
category: Releases
order: 1
---

# koppeltaal-server-releases

## 2.0.0

Released: TBA

* Feature: STU3

## 1.3.2

Released: 03/01/2017

* Bugfix: Application Admin can only edit their own details
* Bugfix: Changing login is no longer possible
* Bugfix: Issue '500 server error when updating an activity definition' \(NQVO-ZOKN-SQGD\)
* Bugfix: Issue 'veel foutmeldingen bij aanmaken domein' \(QCWC-AIOF-RRBA\).
* Bugfix: Attachments are now disabled.
* Bugfix: Issue 'PRD Url werkt niet' \(KXPR-DWQX-EUXN\)
* Bugfix: Issue 'foutmeldingen' \(BCHK-MFRY-EALQ\)
* Bugfix: Issue 'Missing source attribute in message header for CreateOrUpdateActivityDefinition events' \(WMUK-EUDC-NKGB\)
* Bugfix: Issue 'Monitoring file rapport fails on RequestStatistic' \(FOWT-KXKM-TNUZ\)
* Bugfix: Issue '500 error is the log files' \(PHUS-WUUG-KUML\)
* Bugfix: Issue 'Wrong height in message types details view' \(ADIW-TTMP-JWTQ\)
* Pivotal​ ​story:​ ​As Koppeltaal​ ​Product Owner​ ​I​ ​want​ ​to​ ​restrict each​ ​field​ ​on​ ​the allowed​ ​characters​ ​for that​ ​field​ ​so​ ​that​ ​it​ ​is​ ​not possible​ ​to​ ​influence​ ​the application​ ​behaviour with​ ​special​ ​characters \(\#152146659\)

## 1.3.1

Released: 21/09/2017

* Bugfix: ticket 'Niet mogelijk om URL voor SSO binnen domein toe te voegen' \(PBBV-SWIX-MAUD\)
* Bugfix: ticket 'Bug in connectie-aanvraag: form fields greyed out' \(IXGN-OQRC-WHUR\)
* Bugfix: ticket 'Aanvragen van domein op prd.koppeltaal.nl werkt niet' \(DZXF-KEGS-MPAI\)
  * Application admin can now change the default application instance user name, for example to correct an auto-generated name that is too long.
* Bugfix: ticket 'Bug “ontvangen aanvragen” openen' \(CUUL-ULKR-LBUO\)

## 1.3.0

Released 29/06/2017

* Feature: Support API: [Technical Design](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/TD-support-api/README.md)
* Feature: Improved administrator options : [User Guide](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/UG-application-admin.md)
* Feature: Additional statistics: Additional information is now available to the system adminstrator to be used for usage reporting.
* Issue: [Story 'As a Koppeltaal application administrator I can see the processing status set by the recipients of my message so that I can see which applications have successfully retrieved the message.'](https://www.pivotaltracker.com/story/show/136548869)

## 1.2.0

* Feature:    Application    admin can now request a connection to a domain
* Feature:    Storage    Service
* Feature:    Activity end date
* Feature:    Dynamic    activity definitions
* Feature:    Option to archive old ActivityDefinitions
* Improvement: Various small improvements for ApplicationAdministrator portal
* Improvement: Performance improvement
* Platform: Various changes to support the Storage Server
* Platform: Changes in the Conformance \(dealing with date times, enabled caching\)
* Platform: Better    handling for the Accept header

## 1.1.0

* When I send an update ActivityDefinition with less SubActivities to the the Koppeltaal Server, the one no longer existing are not actually deleted or marked as no longer active, causing the Koppeltaal Server to be out-of-date.
* As a Koppeltaal customer I want to be able to create an Organization and link Practitioners to it, and link the CarePlan to the Organization instead of the individual Practitioners, this way creating more stability in the data exchanged.
* When 2 application instances, send an ActivityDefinition that are Domain-specific with the same Identifier in their own domain, the second one gets a duplicate key failure. The same happens when you try to do that through the management portal. Bottom line, the Identifier cannot be defined as a unique key across all domains.
* As a Koppeltaal Application, I want to use a refresh token to secure my authentication, and no longer allow an Authorization Request to be used more than one time.
* As a Koppeltaal customer I want to be able to search for MessageHeaders using the MessageHeader identifier instead of having to parse the ID from the selflink.
* As a koppeltaal customer I want to be able to register the Demo portal for a specific server and domain
* As a Koppeltaal customer I want to have the possibility to get a activation code for a mobile client in the Practitioner/Patient portal

## 1.0.1

* As a Koppeltaal customer I want ActivityDefinition to have the attributes DefaultSubmitter with options Patient, RelatedPerson and Practitioner and a boolean indicating if the ActivityDefinition still active.
* As a Koppeltaal customer I want to be able to publish \(changes in\) the activity definitions that are available. \(Implementation\)
* As a Koppeltaal customer I want to be able to send the CreateOrUpdatePractitioner messages via the VH Koppeltaal Client.
* As a Koppeltaal customer I want to be able to send the CreateOrUpdateRelatedPerson messages via the VH Koppeltaal Client.
* As a Koppeltaal customer I want to be able to send the CreateOrUpdatePatient messages via the VH Koppeltaal Client.

## 1.0.0

Koppeltaal 1.0 is the first official release. It adds the following messages and functionality.

