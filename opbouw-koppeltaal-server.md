---
description: >-
  Koppeltaal is een informatie- en integratiestandaard waarmee zorgaanbieders
  hun informatiesystemen met elkaar kunnen integreren.
---

# Opbouw Koppeltaal Server

Koppeltaal stelt GGZ-instellingen in staat behandelaren en hun clienten vanuit behandelaar- of clientenportaal toegang te geven tot en informatie uit te wisselen tussen eHealth-modules, ROM en EPD met gebruik van standaard-koppelingen.

Koppeltaal GGZ is niet alleen een "communicatie-server", voor het uitwisselen van gegevens tussen systemen. Koppeltaal is een technische oplossing, maar haar toegevoegde waarde gaat verder: Koppeltaal is een infrastructuur voor data, zodat data uit verschillende bronsystemen met elkaar verbonden kunnen worden.

De opbouw van de Koppeltaal Server bestaat uit de volgende lagen:

* Software-laag, bestaande uit:
  * Software Koppeltaal Server \(versie 1.3.x\)
  * Ontwikkeld en draaiend op Philips VitalHealth Platform \(ontwikkeling en onderhoud gebeurt door een van de R&D-afdeling van Philips EMR & Care Management\)
* Infrastructuur-laag, met als kenmerken:
  * Ondergebracht bij de hosting provider Open Line
  * Productieomgeving:
    * separaat netwerksegment
    * applicatieserver
    * databasecluster, bestaande uit databaseservers op twee fysiek gescheiden locaties \(Landgraaf en Maastricht\); hierbij vindt real-time datasynchronisatie plaats
  * Test-/acceptatieomgevingen \(_Edge_, _Stable, Demo_ en _Acceptatie_ \), met als kenmerken:
    * shared netwerksegment
    * applicatieserver
    * databaseserver

#### Koppeltaal omgeving URL's

| Server | URL | KT Versie |
| :--- | :--- | :--- |
| **Edge** | [https://edgekoppeltaal.vhscloud.nl](https://edgekoppeltaal.vhscloud.nl) | 1.3.9 |
| **Stable** | [https://stablekoppeltaal.vhscloud.nl](https://stablekoppeltaal.vhscloud.nl) | 1.3.9 |
| **Demo** | [https://demokoppeltaal.vhscloud.nl](https://demokoppeltaal.vhscloud.nl) | 1.3.8 |
| **Acceptatie** | [https://acckoppeltaal.vhscloud.nl](https://acckoppeltaal.vhscloud.nl) | 1.3.9 |
| **Productie** | Opvraagbaar bij VZVZ | 1.3.8 |

#### 

#### 

