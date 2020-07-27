---
title: Introduction
category: Integrator
order: 1
---

# integrator-introduction

Koppeltaal is a foundation in which mental healthcare organisations and IT suppliers take place. Koppeltaal offers two main propositions:

* **Koppeltaal** - a community supported information standard based on HL7 FHIR used for defining a current set of messages
* **Koppeltaal Server** - a message platform with a REST API

Using these it is possible to develop reliable, portable integrations between two ehealth applications. Koppeltaal will not define exactly how to build a feature, but it will provide a basis to design the interfaces, the process and the data involved. It will also provide the infrastructure to develop, test, accept the integration and eventually ramp up to production.

When planning an integration \(_koppeling_\) IT suppliers may choose to use Koppeltaal to

* Increase the portability of integrations between customers
* Decrease dependency of implementation specifics of other IT suppliers
* Tailor to the needs of a customer that is planning to or already using Koppeltaal
* Increase the quality of a software solution from using a well known standard \(FHIR and Koppeltaal\)

Healthcare organisations may choose to use Koppeltaal to:

* Reduce IT problems with integration, and associated costs
* Increase choice
* Cost reduction
* Improve quality of care

### Use cases

So what can be achieved using Koppeltaal? Koppeltaal is being extended to support increasingly more use cases. Each extension is made available through a new Koppeltaal version. These versions are published on @@@

Current use cases are:

* Allow clinicians to provision patients with a Mobile Game via an eHealth platform
* Allow patients to see and access their ROM questionnaires through a patient portal
* Allow patients to access modules from various providers in a patient portal.

### Why Koppeltaal?

Mental healthcare in the Netherlands is comprised of approximately 140 large and medium sized organisations \(_source: Koppeltaal GGZ \(IT meeting\) presentation, 2014\)_. Most of these organisations use one or more of a smaller group of eHealth products or services. EHealth products or services comprised of mobile apps, personal health records, patient portals and other platforms offering online \(web based\) eHealth in the form of treatments, measurements, monitoring etc.

Reasons for healthcare organisations and professionals to adopt ehealth are:

* Governments and insurance companies have long stimulated financially
* Budget costs lead to new way of organising care more efficiently
* Patients expect online healthcare
* Technology drive leads to more possibilities

This leads to the emergence of many eHealth products and services. Naturally, there is a desire for these products and services to be integrated in the IT landscape of healthcare organisations. This tendency results in a large number of permutations, this calls for standardisation.

Koppeltaal uses FHIR, their Koppeltaal community and a domain driven design process to evolve the _Koppeltaal_ and the _Koppeltaal Server_ implement the supported use cases.

## Reading guide

The Koppeltaal documentation will explain how to deal with Koppeltaal as an IT supplier, be it a software developer or a product, project or sales manager. It could also be useful for functional application managers or IT-professionals from the care provision side.

### Documentation structure

We have structured the documentation to be iteratively detailed, such that reading it linearly will take you from being completely new to being an expert developer. You may of course start and stop wherever you like. The sections are as follows:

1. An introduction to provide a quick overview of the various facets relevant in a Koppeltaal project. You will likely read this only once, if at all.
   1. A general project brief
   2. A more detailed decomposition of the anatomy of a Koppeltaal
   3. A similar decomposition of a Koppeltaal project.
2. Technical documentation necessary when building an adapter
   1. ...
3. Technical documentation necessary when using an adapter
   1. ...

### I need to know...

* Who do I need to contact when starting a project, Go to chapter 1
* Why am I receiving empty JSON, go to chapter 3
* Where to start when doing regression tests, go to chapter 2
* Who defines what I can and can’t do with Koppeltaal.
* ...

