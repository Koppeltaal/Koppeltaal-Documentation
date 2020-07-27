---
title: Frequently Asked Questions
category: How-to
order: 4
---

# FAQ

Q: What can I use Koppletaal for?

A: Please follow functional example. There is more information available inside the documentation package... [Functional example](https://koppeltaal.github.io/documentation/templates/Koppeltaal%20FuncFlow.pdf)

Q: How can one start work with Koppeltaal?

A: Please follow the "How to start" documentation [working with Koppeltaal](https://www.koppeltaal.nl/homepage/how-to-start)

Q: How long does the Koppeltaal Server keep the messages that are sent through it?

A: The default behaviour of is for any messages to be removed after all recipients have retrieved the message from their queues or after 31 days, whichever comes first. Depending on specific application settings, specific message types may be stored indefinitely. This is only the case for messages of type CreateOrUpdateCarePlan in domains that use the KickASS game. It is also possible to configure the server a shorter maximum retainment period for specific message types a domain.

Q: What are the Organizational roles recognised in Koppeltaal

A:

* Visitor
* Interested party/person
* Customer
* Consumer
* Governor
* Network promotor
* Contract manager
* Service provider
* Infrastructure operator
* Technology developer
* Organization developer
* Supplier

These roles may distinguish specific subroles to improve the precision of the performance and collaboration of koppeltaal activities.

Q: How can I register a Domain at Koppeltaal?

A: If you are new please read the [https://www.koppeltaal.nl/homepage/how-to-start](https://www.koppeltaal.nl/homepage/how-to-start) in order to proceed.

To create a new Domain: A new domain request \(please send an email to support\(at\)koppeltaal.nl\) requires a domain name and a contact person. As a Domain is a legal entity we will take this request in our process and define a project for it. Then Support will try to complete the process by getting all the required information from the contact person given in the request.

Q: How can I start testing within a new domain?

A:

Koppeltaal offers a suite of tools to help testing a domain interaction:

* Regression tests: using SOAPUI project \(available inside the GIT/Server/Tests\) one can emulate a full REST flow
* Test Game: A basic JS test game is availabe and can be coupled in a domain upon a request to support
* Test Portal: A basic Test Portal \(to simmulate Care plans and launches\) can be integrated in a domain upon a request to support
* Adapter test cases: each adapter offers a suite of test cases. Please see Koppletaal GIT for more details.

