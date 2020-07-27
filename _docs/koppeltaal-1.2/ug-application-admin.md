---
title: User Guide - Application Administrator portal
category: User Guides
order: 2
---

# UG-application-admin

## Overview

An application administrator is responsible for managing the working of one or more applications. Typically this role is fulfilled by a functional administrator employed by the organisation that owns the application\(s\).

## Table of contents

[Requesting an application administrator account](ug-application-admin.md#ApplicationAministratorRequest)

[Registering an application](ug-application-admin.md#ApplicationRegistration)

[Requesting a domain](ug-application-admin.md#DomainRegistration)

[Linking an application to a domain](ug-application-admin.md#DomainConnection)

[Configure SSO OAuth2 settings](ug-application-admin.md#OAuth2)

[Configure automatic cleanup settings](ug-application-admin.md#AutomaticCleanup)

## Requesting an application administrator account

In order to log in to the Koppeltaal Server an account is required. To request an account with the application administrator role navigate to the following portal on the Koppeltaal Server of your choice.

\[Server URL\]/backend/main.html?project=Koppeltaal&main-view=ApplicationAdministratorRegistrationPortal.

You will be asked to enter your name, an email address and the desired user name.

![Application administrator registration portal](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/Portal-ApplicationAdministratorRegistrationPortal.png)

It is important to note that a user name that must be personal. The user name 'p.dekorte@company.nl' is fine. The user name 'support@company.nl' is not. This is because any actions taken by a user can be logged and must be tracable to a specific person.

After you have sent your request a Koppeltaal system administrator will review it. If there are any further questions you will be contacted via either the listed email address or other means of communication, if known.

When the request is accepted you will receive credentials for your account via mail, allowing you to log in to the Koppeltaal Server.

## Registering an application

In order to register a new application to a Koppeltaal Server, first make sure that you are logged in to the Application Administrator portal. If you do not have an application administrator account, see [Requesting an application administrator account](ug-application-admin.md#ApplicationAministratorRequest).

After logging in you will be presented with the list of applications. Alternatively, select 'Applications' in the left-hand menu.

![Application administrator - Applications](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/ApplicationAdmin-Applications.png)

In the list titled 'My applications', press the button labeled 'Request new application'. The following window will pop up:

![Application administrator registration portal](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/ApplicationAdmin-RequestNewApplication.png)

In this window, please fill out the following fields:

* Name: the name of the new application
* Identifier: a unique shorthand for this application
* Application roles: the roles that this application can act as
* Name contact person: the name of the person to be contacted for any technical or functional questions related to this application
* Contact emailaddress: the email address at which the contact person can be reached
* SSOUrl: the URL to be used when the applicatiokn is launched via the Koppeltaal single sign-on launch sequence. \(TBD: link to details of the SSO launch sequence\)

After filling in the fields, press the save button on the top left, in the toolbar. Your request will be saved and appear in your list of requested applications. A Koppeltaal system administrator will be notified and review your request. If there are any questions regarding your request you will be contacted, otherwise the request will be accepted. When the request is accepted you will be notified via email and the application will appear under 'My applications'.

## Registering a domain

In order to register a new domain on a Koppeltaal Server, first make sure that you are logged in to the Application Administrator portal. If you do not have an application administrator account, see [Requesting an application administrator account](ug-application-admin.md#ApplicationAministratorRequest).

After logging in to the Koppeltaal Server select 'Domains' from the left-hand menu.

![Application administrator registration portal](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/ApplicationAdmin-Domains.png)

In the list titled 'My domains', press the button labeled 'Request new domain'. The following window will pop up:

![Application administrator registration portal](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/ApplicationAdmin-RequestNewDomain.png)

In this window, please fill out the following fields:

* Name: the name of the new domain
* DTAP phase: the type of activity that will place in this domain: development, testing, acceptance tests or production. This information is used by the Koppeltaal system administrator as a check that the domain is appropriate for a given Koppeltaal Server
* Will be used for: a short description of the purpose of the domain
* Data storage service: the storage server for the domain \(if any\)
* Requesting application: the application that wishes to use this new domain. This application will be linked to the new domain automatically when it is created
* Health care organization: the organization responsible for the data in the domain
* Contact person at health care organization: the name of the person to be contacted for any questions regarding this domain
* Health care organization phone number: the phone number at which the contact person can be reached
* Health care organization email address: the email address at which the contact person can be reached
* Email address domain administrator: the email addres of the person that will be managing this domain
* Name of domain administrator: the name of the person that will be managing this domain

After filling in the fields, press the save button on the top left, in the toolbar. Your request will be saved and appear in your list of requested domains. A Koppeltaal system administrator will be notified and review your request. If there are any questions regarding your request you will be contacted, otherwise the request will be accepted. When the request is accepted you will be notified via email and the domain will appear under 'My domains'. The requesting application will automatically be linked to the new domain.

## Linking an application to a domain

In order to link an existing application to a domain on a Koppeltaal Server, first make sure that you are logged in to the Application Administrator portal. If you do not have an application administrator account, see [Requesting an application administrator account](ug-application-admin.md#ApplicationAministratorRequest).

After logging in you will be presented with the list of applications. Alternatively, select 'Applications' in the left-hand menu.

![Application administrator registration portal](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/ApplicationAdmin-Applications.png)

Find the application you wish to create a connection for in the list, then double-click the record to open its details.

![Application administrator registration portal](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/ApplicationAdmin-ApplicationDetails.png)

The tab 'Application instances' shows the application instances that already exist for the selected application and the domains that are available to connect to. Click the button labeled 'Request connection' to initiate a request to have your application be requested. You will be asked to check the details of the request.

![New domain request](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/ApplicationAdmin-RequestNewDomainConnection.png)

The popup shows an overview of the domain and the application that will be linked. Under header 'Application instance settings' you can edit domain-specific settings. The application instance user name is automatically suggested. Care should be taken that the length of the user name does not exceed 50 characters.

The checkbox 'Application can be started via OAuth', when checked, enables you to enter the details of the SSO launch for this application instance.

After filling in the fields, press the save button on the top left, in the toolbar. Your request will be saved and appear in your list of requested domain connections. A domain administrator will be notified and review your request. If there are any questions regarding your request you will be contacted, otherwise the request will be accepted. When the request is accepted you will be notified via email and your application will be linked to the selected domain. The credentials for the domain will be sent to you in a separate email.

## Configure SSO OAuth2 settings

TBD

## Configure automatic cleanup settings

An application administrator can specify that messages of a specific type are always retained, regardless of maximum message age. This should only be used in the case that the application cannot function if messages of this type are expired.

See [the TD for topic Automatic Data Removal](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/TD-automatic-data-removal/README.md) for further details.

![Applications &amp;gt; Cleanup settings](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/CleanupSettings-Application.png)

