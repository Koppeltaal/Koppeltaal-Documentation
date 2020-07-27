---
title: User Guide - Registration to Test Environment
category: User Guides
order: 2
---

# Overview

The Koppeltaal test server can be used to test an application. The domain 'Koppeltaal Samples' is available as a 'general use' domain. It is also possible to request the creation of another domain to perform application specific tests.

To request access to one or more domains on the Koppeltaal test server, send an email to support@koppeltaal.nl containing the information below.

* The name of your application
* The name of the domain\(s\) you wish to have access to
* The email address to which the credentials should be sent If your application is not yet registered at the Koppeltaal test server you will have to provide the following data.
  * The role\(s\) your application acts in \(only used for information\):
  * Practitioner Portal
  * Patient Portal
  * Related Person Portal
  * Game
  * E-Learning
  * ROM
  * The name of the contact person for the application
  * The email address of the contact person
  * The message types the application should receive
  * CreateOrUpdateCarePlan
  * CreateOrUpdateCarePlanActivityResult
  * CreateOrUpdateUserMessage
  * UpdateCarePlanActivityStatus

If the application is launched via SSO then provide the following:

* Url voor single sign-on

If this is an intervention then provide the Activity Definitions:

* Activity Name
* Activity Identifier
* Sub-activities \(only if present\)

Not yet in scope

Security information \(certificates, domain application code, Oauth Secret\)

Example:

_Application name: MyApplication_ Domain: Koppeltaal Samples, MyApplicationTestDomain _Email: support@myapplication.com_ Roles: Practitioner Portal, Patient Portal \*Contact person: John Smith \(j.smit@myapplication.com\)

You will receive one email per requested domain that will contain your credentials for that domain. You will need to provide these when sending or retrieving messages to/from the server.

Every application also receives an application admin account. With this account you have access to the Koppeltaal test server's application admin portal. From this portal you can see and edit the details of your application\(s\), see information about other applications in your domain and view all messages that have been sent in your domain. The Koppeltaal server login page can be found at [https://testconnectors.vhscloud.nl//](https://testconnectors.vhscloud.nl//)

![image alt text](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/UG-regustration-test-env1.png)

