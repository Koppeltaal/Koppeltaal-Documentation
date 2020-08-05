---
title: Environments
category: How-to
order: 4
---

# Environments

Koppeltaal Server InternalThese environments are part of the Koppeltaal Server development process. They are not accessible for third parties.

## Test

URL: [https://testkoppeltaal.vhscloud.nl](https://testkoppeltaal.vhscloud.nl)

Used for the Koppeltaal Server regression tests.

## Acceptance

URL: [https://acckoppeltaal.vhscloud.nl](https://acckoppeltaal.vhscloud.nl)

Used for the Koppeltaal Server load and performance tests.

## Third party development

Edge\[edit\] URL: [https://edgekoppeltaal.vhscloud.nl](https://edgekoppeltaal.vhscloud.nl)

The latest stable build of the Koppeltaal Server. Connecting applications can preview the latest features and bugfixes here.

## Next

URL: [https://nextkoppeltaal.vhscloud.nl](https://nextkoppeltaal.vhscloud.nl)

The upcoming Koppeltaal Server version. This will generally be the version of Koppeltaal Server that is undergoing acceptance tests. If there is currently no new version being accepted this version will be identical to the production version.

S\# table URL: [https://stablekoppeltaal.vhscloud.nl](https://stablekoppeltaal.vhscloud.nl)

The version of the Koppeltaal Server currently in production.

## Third party acceptance

These environments are used to accept connectors and clients before a Koppeltaal Server release.

## Connectors

URL: [https://connectorskoppeltaal.vhscloud.nl](https://connectorskoppeltaal.vhscloud.nl)

Used to perform the Koppeltaal connector acceptance tests.

## Clients

URL: [http://accclients.vhscloud.nl](http://accclients.vhscloud.nl)

Used to perform the Koppeltaal client acceptance tests.

## Production

URL: [https://prd.koppeltaal.nl](https://prd.koppeltaal.nl)

The live environment.

## Demo

URL: TBA

A sandbox environment, using the same version as the production environment.

## Versions per environment

The version of Koppeltaal Server that each environment is running will vary. Depending on the progress of the next Koppeltaal Release some environments may have been updated to the latest version. In general, no environment will be more than one minor version behind. No environment will run an older version than the production environment. For more details on the test and release flow, see Project Test & release flow.

A typical distribution of versions may look like this:

NOTE: these are not the actual, current versions.

Environment Version Description Koppeltaal Server Test 1.1 \(revision 401\) The Koppeltaal Server development team is developing version 1.1 Koppeltaal Server Edge 1.1 \(revision 400\) Revision 401 did not pass the regression tests and so Edge was not updated. Koppeltaal Server Acceptance 1.0.1 \(revision 350\) Version 1.0.1 has passed acceptance tests and moved on to the third party acceptance stage. Koppeltaal Server Next 1.0.1 \(revision 350\) Version 1.0.1 is undergoing tests and is expected to be released soon. Connectors Acceptance 1.0.1 \(revision 350\) A new revision of 1.0.1 is undergoing connector acceptance tests. Apparently a bug was discovered somewhere during the client acceptance tests. Clients Acceptance 1.0.1 \(revision 345\) The revised version of 1.0.1 has not passed connector tests yet, so the clients acceptance environment has not yet been updated. Koppeltaal Server Production 1.0 The production environment is running the last stable version. It will only be updated after 1.0.1 passes both connector and client tests. Koppeltaal Server Stable 1.0 The Stable environment will always mirror the version of Koppeltaal Server Production.

