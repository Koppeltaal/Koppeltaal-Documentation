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

| Server | URL | Omschrijving | KT Versie |
| :--- | :--- | :--- | :--- |
| **Edge** | [https://edgekoppeltaal.vhscloud.nl](https://edgekoppeltaal.vhscloud.nl) | Testomgeving van de community, met de nieuwste \(deel\)release of bugfix. Als er een complete release staat, dan wordt door VZVZ Koppeltaal Testteam de release geaccepteerd alvorens het naar **Acceptatie** te laten gaan. | 1.3.9 |
| **Stable** | [https://stablekoppeltaal.vhscloud.nl](https://stablekoppeltaal.vhscloud.nl) | Ketentestomgeving voor GGZ \(_huidige_ Koppeltaal Kern release\). | 1.3.9 |
| **Demo** | [https://demokoppeltaal.vhscloud.nl](https://demokoppeltaal.vhscloud.nl) | Kan door hele community gebruikt worden voor demo's. | 1.3.8 |
| **Acceptatie** | [https://acckoppeltaal.vhscloud.nl](https://acckoppeltaal.vhscloud.nl) | Ketentestomgeving voor GGZ \(_toekomstige_ Koppeltaal Kern release\). | 1.3.9 |
| **Productie** | Opvraagbaar bij VZVZ | Live omgeving voor zorgcommunicatie door cliënten en behandelaren van GGZ-instellingen via applicaties van IT-deelnemers die met elkaar verbonden zijn via Koppeltaal. | 1.3.8 |

#### Core applicaties

Informatie van deze paragraaf valt onder de regie van: Koppeltaal Testteam

Feedback via e-mail: [koppeltaal-testteam@vzvz.nl](mailto:koppeltaal-testteam@vzvz.nl)

Nieuwere versies van adapters voor gebruik met KT v1.3.x zullen worden toegevoegd zodra deze zijn geaccepteerd. Deze nieuwe versies staan altijd in onderstaande folders op Github.

Applicatieontwikkelaars mogen deze adapters inbouwen, testen en uiteindelijk hun applicatie met nieuwe adapter bij het acceptatieteam van Koppeltaal aanbieden voor acceptatie voor gebruik in Koppeltaal v1.3.x.

Voor community leden die nog niet actief zijn in de productiefase van Koppeltaal is het raadzaam om de koppeling met Koppeltaal te ontwikkelen op basis van Koppeltaal 1.3.5. De impact daarvan is relatief beperkt, en je voorkomt extra inspanningen om na ingebruikname alsnog binnen enkele maanden na release op productie alsnog verplicht te moeten upgraden naar Koppeltaal 1.3.5.

_Let op: adapterversies voor gebruik met KT 1.3.3 en ouder zullen na keten brede ingebruikname van KT 1.3.5 in productie niet meer geaccepteerd worden voor gebruik in test-, ontwikkel- en productie-omgevingen van Koppeltaal._

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left">Objectomschrijving</th>
      <th style="text-align:left">Locatie adapter</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>JavaScript connector</b>
      </td>
      <td style="text-align:left">JavaScript connector for Koppeltaal Server</td>
      <td style="text-align:left">
        <p>Community members only</p>
        <p><a href="https://github.com/Koppeltaal/Koppeltaal-JS-Connector">https://github.com/Koppeltaal/Koppeltaal-JS-Connector</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Android Connector</b>
      </td>
      <td style="text-align:left">Android connector for Koppeltaal Server</td>
      <td style="text-align:left">
        <p>Community members only</p>
        <p> <a href="https://github.com/Koppeltaal/Koppeltaal-Android-Connector">https://github.com/Koppeltaal/Koppeltaal-Android-Connector</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iOS Connector</b>
      </td>
      <td style="text-align:left">iOS connector for Koppeltaal Server</td>
      <td style="text-align:left">
        <p>Community members only</p>
        <p><a href="https://github.com/Koppeltaal/Koppeltaal-iOS-Adapter">https://github.com/Koppeltaal/Koppeltaal-iOS-Adapter</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Java Connector</b>
      </td>
      <td style="text-align:left">Java connector for Koppeltaal Server</td>
      <td style="text-align:left">
        <p>Community members only</p>
        <p><a href="https://github.com/Koppeltaal/Koppeltaal-Java-Connector">https://github.com/Koppeltaal/Koppeltaal-Java-Connector</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>C# Connector</b>
      </td>
      <td style="text-align:left">C# connector for Koppeltaal Server</td>
      <td style="text-align:left">
        <p>Community members only</p>
        <p><a href="https://github.com/Koppeltaal/Koppeltaal-C-Sharp-Connector">https://github.com/Koppeltaal/Koppeltaal-C-Sharp-Connector</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Python Connector</b>
      </td>
      <td style="text-align:left">Python connector for Koppeltaal Server</td>
      <td style="text-align:left">
        <p>Community members only</p>
        <p><a href="https://github.com/Koppeltaal/Koppeltaal-Python-Connector">https://github.com/Koppeltaal/Koppeltaal-Python-Connector</a>
        </p>
        <p>Voor meer informatie over het gebruik van het Python package, zie sectie
          &quot;Additionele informatie over packages van adapters&quot;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>PHP Connector</b>
      </td>
      <td style="text-align:left">PHP connector for Koppeltaal Server</td>
      <td style="text-align:left">
        <p>Community members only</p>
        <p><a href="https://github.com/Koppeltaal/Koppeltaal-PHP-Connector">https://github.com/Koppeltaal/Koppeltaal-PHP-Connector</a>
        </p>
      </td>
    </tr>
  </tbody>
</table>

## Test tools

Informatie in deze sectie is onder regie van: Koppeltaal Testteam

Feedback via e-mail: [koppeltaal-testteam@vzvz.nl](mailto:koppeltaal-testteam@vzvz.nl)

Onderstaande testtooling is buiten scope van de transitie naar Koppeltaal 1.3.5.

Meer weten? Neem aub contact op met het testteam, [koppeltaal-testteam@vzvz.nl](mailto:koppeltaal-testteam@vzvz.nl)

| **Tool** | Description |
| :--- | :--- |
| **Test Portal** | Portal tool to be used when testing interventions |
| **Test Client** | Client test simulating the intervention |
| **Regression Test** | Regression testing for REST API Calls |
| **Test Storage Service** | Storage API test |
| **Load and Performance Test Scripts** | Load and Performance Scripts simulating the Patient, Related person and Caregiver load in a complex environment |

