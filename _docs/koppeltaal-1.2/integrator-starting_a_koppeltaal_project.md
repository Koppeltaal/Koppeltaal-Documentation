---
title: Starting a Koppeltaal project
category: Integrator
order: 1
---

# Starting a Koppeltaal project

In order to start with a Koppeltaal project, the following things need to be present:

* Two or more IT suppliers
* Two or more applications
* At least one healthcare provider
* Koppeltaal Domain
* One or more use cases
* Koppeltaal supplier access
* Koppeltaal Server development and/or test environments

Whether explicitly in a project document or implicitly in an agile development setting, the following development phases will be followed:

1. **Definition of Scope** - the first step is ascertaining what exactly needs to be realised. This phase should be conducted by all parties involved.
2. **Design: Integration** - Design of the integration will done mainly by the IT suppliers and possibly Koppeltaal or the Koppeltaal community. The result of this phase will be a feasible design that will facilitate technical parties involved to create their own respective application designs. Roughly speaking this phase will yield:
3. Functional Design
   * Domain model
4. Technical Design of Integration
   * Stakeholders
   * Systems
   * Sequence Diagram
   * Messages/Data
   * Selection of Koppeltaal Version
5. **Make or "Buy" decision Adapter/Connector** - Based on the available connectors \([https://github.com/Koppeltaal](https://github.com/Koppeltaal)\) a decision should be made whether to use an existing connector or create a new one.
6. **Design: Applications** - Koppeltaal will facilitate only in communication, and each IT supplier will need to design their respective applications as to create value for the users. This phase will yield:
7. Functional Design
8. Technical Design
9. User Interface Design
10. **Development and/or configuration: Application** - Koppeltaal will facilitate only in communication, and each IT supplier will need to extend or configure their respective applications as to create value for the users. This phase will generally comprise of:
11. Integrating Connector
12. Software development process
13. Configuration process
14. **Testing: applications** - Each IT supplier should go about their own testing procedures
15. **Testing: integration** - In order to ensure the properly functioning integration as a whole, this phase should be conducted. For both applications and Koppeltaal server, the correct environments should be selected, based on Koppeltaal version.
16. **Acceptation** - After the IT suppliers have ascertained proper functioning of the integration, all other stakeholders should be involved for acceptation of the integration. It is important to have a clear distinction between integration aspects and application aspects.
17. **Deployment of applications** - both applications deploy their respective versions and communicate about progress.
18. **Configuration of Koppeltaal** - Koppeltaal domain on Koppeltaal Server production environment should be configured appropriately.
19. **Integration Ramp Up** - When all parties involved provide a green light, the Koppeltaal messages can be exchanged!

