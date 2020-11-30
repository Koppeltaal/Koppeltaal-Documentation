---
description: >-
  Koppeltaal 1.3.x maakt gebruik van adapters voor zorgcommunicatie in FHIR
  tussen applicaties via de Koppeltaal server (v1.3.x).
---

# Releases

## Koppeltaal server

Huidige release : **1.3.8.**  Geplande release **1.3.9** in 2021.

Release 1.3.8 is een herstelversie van 1.3.5.

Hierin zijn de volgende punten opgenomen:

| Ticket | Type | Omschrijving |
| :--- | :--- | :--- |
| ICE-654 | Bug | Dubbele punt in wachtwoord waardoor authenticatie faalt. |
| ICE-647 | Change Request | Het '&' teken in ActivityDefinition zorgt voor foutmelding. |
| ICE-630 | Bug | Syntax fout in wachtwoord. Beleidsregels aanzetten voor wachtwoord. |
| ICE-599 | Bug | Wachtwoord herstel problemen. |
| ICE-598 | BUG | Functionaliteit van verificatiecode werkt niet correct. |
| ICE-183 | Feature Request | Bericht identifier toevoegen in WebHook POST. |

Release 1.3.9 is \(ook\) een herstelversie van 1.3.5.

Hierin zijn, voorlopig,  de volgende punten opgenomen:

| Ticket | Type | Omschrijving |
| :--- | :--- | :--- |
| ICE-716 | Feature Request | Performance issue Integrator queries |
| ICE-715 | Feature Request | Performance issue Koppeltaal queries |
| ICE-697 | Bug | Error on GetNextNextAndClaim |
| ICE-645 | Bug | 2FA - Mobiel nummer kan foutief aangepast worden met verificatie |

**Supported Koppeltaal release:** 1.3.5

## Planning

Release 1.3.5 is by design ontworpen vanuit de behoefte van beheerorganisaties om de migratie van hun applicaties onafhankelijk van elkaar te kunnen doorvoeren. Applicaties die nog op 1.3.3 uitwisselen, kunnen by design uitwisselen met applicaties die al op 1.3.5 communiceren. Alle partijen worden opgeroepen om zo spoedig mogelijk de migratie af te ronden door hun applicatie in productie te voorzien van release 1.3.5 of hoger van Koppeltaal.

Release 1.3.9 is een herstelversie van 1.3.5 en wordt begin 2021 in productie gebracht.

## API specificaties

Informatie in deze sectie is onder regie van: architect Koppeltaal 

Feedback via e-mail: [koppeltaal-architectuur@vzvz.nl](mailto:koppeltaal-architectuur@vzvz.nl)

**Koppeltaal 1.3.x Architectuur**: [Architectuur documentatie](https://vzvz.gitbook.io/koppeltaal-1-3-architectuur/). Status: definitief

## Omgevingen Koppeltaal

Informatie in deze sectie is onder regie van: Koppeltaal testteam

Feedback via e-mail: [koppeltaal-testteam@vzvz.nl](mailto:koppeltaal-testteam@vzvz.nl)  

Voor community leden die nog niet actief zijn in de productiefase van Koppeltaal is het raadzaam om de koppeling met Koppeltaal te ontwikkelen op basis van Koppeltaal 1.3.5. De impact daarvan is relatief beperkt, en je voorkomt extra inspanningen om na ingebruikname alsnog binnen enkele maanden na release op productie alsnog verplicht te moeten upgraden naar Koppeltaal 1.3.5.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Omgeving</th>
      <th style="text-align:left"><b>Environment</b>
      </th>
      <th style="text-align:left"><b>Huidige Koppeltaal versie</b>
      </th>
      <th style="text-align:left">Omschrijving</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Edge</td>
      <td style="text-align:left"> <a href="http://edgekoppeltaal.vhscloud.nl/">Edgekoppeltaal.vhscloud.nl</a>
        <br
        />
      </td>
      <td style="text-align:left">1.3.8</td>
      <td style="text-align:left">Testomgeving van de community, met de nieuwste (deel)release of bug fix.
        Als er een complete release staat, dan wordt door VZVZ Koppeltaal Testteam
        de release geaccepteerd alvorens het naar Acc te laten gaan.</td>
    </tr>
    <tr>
      <td style="text-align:left">Acceptatie</td>
      <td style="text-align:left"><a href="http://acckoppeltaal.vhscloud.nl/">Acckoppeltaal.vhscloud.nl</a>
      </td>
      <td style="text-align:left">1.3.8</td>
      <td style="text-align:left">Ketentestomgeving voor GGZ (toekomstige Koppeltaal Kern release)</td>
    </tr>
    <tr>
      <td style="text-align:left">Productie</td>
      <td style="text-align:left"><a href="https://prd.koppeltaal.nl/">prd.koppeltaal.nl</a>
      </td>
      <td style="text-align:left">1.3.8</td>
      <td style="text-align:left">Live omgeving voor zorgcommunicatie door cli&#xEB;nten en behandelaren
        van GGZ-instellingen via applicaties van IT-deelnemers die met elkaar verbonden
        zijn via Koppeltaal</td>
    </tr>
    <tr>
      <td style="text-align:left">Schaduw productie</td>
      <td style="text-align:left"> <a href="https://prodshadow.vhscloud.nl/">prodshadow.vhscloud.nl</a>
      </td>
      <td style="text-align:left">1.3.8</td>
      <td style="text-align:left">
        <p>Schaduwomgeving van huidig productie voor KT Support. Bevat de KT-server
          met dezelfde versie als prd. KT Support kan tijdelijk toegang verlenen
          voor naspelen van productie incidenten en voor proefmigraties. Partijen
          kunnen dan tijdelijk een domein inrichten.</p>
        <p>Alleen met toestemming van VZVZ Koppeltaalketenregie kunnen IT-deelnemers
          hiervoor een domein laten aanmaken.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Stable</td>
      <td style="text-align:left"><a href="http://stablekoppeltaal.vhscloud.nl/">Stablekoppeltaal.vhscloud.nl</a>
      </td>
      <td style="text-align:left">1.3.8</td>
      <td style="text-align:left">Ketentestomgeving voor GGZ (huidige Koppeltaal Kern release).</td>
    </tr>
    <tr>
      <td style="text-align:left">Demo</td>
      <td style="text-align:left"><a href="http://demokoppeltaal.vhscloud.nl/">Demokoppeltaal.vhscloud.nl</a>
      </td>
      <td style="text-align:left">1.3.8</td>
      <td style="text-align:left">Kan door hele community gebruikt worden voor demo&apos;s</td>
    </tr>
  </tbody>
</table>

## Core applicaties

Informatie in deze sectie is onder regie van: Koppeltaal Testteam

Feedback via e-mail: [koppeltaal-testteam@vzvz.nl](mailto:koppeltaal-testteam@vzvz.nl)  

Onderstaande sectie bevat de informatie naar de meest recente versie.  Nieuwere versies van adapters voor gebruik met KT v1.3.5 zullen worden toegevoegd zodra deze zijn geaccepteerd. Deze nieuwe versies staan altijd in onderstaande folders op Github.

Applicatieontwikkelaars mogen deze adapters inbouwen, testen en uiteindelijk hun applicatie met nieuwe adapter bij het acceptatieteam van Koppeltaal aanbieden voor acceptatie voor gebruik in Koppeltaal v1.3.5.

Voor community ****leden die nog niet actief zijn in de productiefase van Koppeltaal is het raadzaam om de koppeling met Koppeltaal te ontwikkelen op basis van Koppeltaal 1.3.5. De impact daarvan is relatief beperkt, en je voorkomt extra inspanningen om na ingebruikname alsnog binnen enkele maanden na release op productie alsnog verplicht te moeten upgraden naar Koppeltaal 1.3.5. 

_Let op: adapterversies  voor gebruik met KT 1.3.3 en ouder zullen na na  keten brede ingebruikname van KT  1.3.5 in productie niet meer geaccepteerd worden voor gebruik in test-, ontwikkel- en productie-omgevingen van Koppeltaal._

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
| **Regression Test**  | Regression testing for REST API Calls |
| **Test Storage Service** | Storage API test |
| **Load and Performance Test Scripts** | Load and Performance Scripts simulating the Patient, Related person and Caregiver load in a complex environment  |

