# Informatiesystemen architectuur

## Koppeltaal

### Domein en Applicatie

In de doelstelling van stichting Koppeltaal is middels het woord ‘interne’ een beperking voor de gegevensuitwisseling opgenomen. Met deze beperking wordt bedoeld dat de gegevensuitwisseling altijd plaatsvindt onder de verantwoordelijkheid van één **zorgaanbieder.** In de Koppeltaal architectuur is daarom gekozen voor het concept **domein.** Een domein, in Koppeltaal, is synoniem aan een zorgaanbieder, en beperkt de gegevensuitwisseling tot _interne gegevensuitwisseling_ onder verantwoordelijkheid van de betreffende zorgaanbieder.

De gegevensuitwisseling vindt plaats tussen applicaties. In Koppeltaal staat het begrip **applicatie** voor alle vormen van eHealth platformen en informatiesystemen \(zoals portalen, interventie- en bronsystemen\) die voor de zorgaanbieder relevant zijn om gegevens tussen uit te wisselen, in de context van blended care behandelingen.

![Koppeltaal applicaties](.gitbook/assets/2%20%281%29.jpeg)

De volgende type applicaties onderscheiden we waarmee zorgaanbieders hun informatiesystemen naadloos op elkaar willen aansluiten binnen Koppeltaal.

Een **eHealth platform** is een \(elektronisch\) platform waar participanten \(betrokkenen\) in de zorg op een veilige en efficiënte manier informatie \(inclusief persoonsgegevens\) ‘_over’_ een behandeling kunnen uitwisselen en interventies kunnen gebruiken en uit kunnen voeren voor gebruik ‘_in’_ een \(blended care\) behandeling.

Een **portaal** is een toegangspoort of vertrekpunt voor verder navigatie tot geselecteerde bronnen die over een bepaald onderwerp gaan. Binnen Koppeltaal kunnen cliënten \(_patiënten_\), _behandelaars_, en _derden_ toegang krijgen tot functionaliteiten ‘over’ een behandeling en interventies voor gebruik ‘in’ een behandeling. Dit zijn tevens de drie verschillende typen portalen.

Een **interventie** \(systeem\) is een doelbewuste ingreep of een ondersteunend systeem bij een bepaalde behandeling. Het is op meerdere gebieden van toepassing en het hangt dan ook sterk af van de context waarin het wordt geplaatst. Binnen Koppeltaal hebben we 3 soorten interventies gedefinieerd, namelijk: ‘Game’, ‘E-Learning’ en ‘ROM’. Deze interventies zijn zelfstandige applicaties die onderdeel kunnen zijn van een behandeling.

Een **bronsysteem** is het systeem waar gegevens voor de eerste keer \(en eenmalig\) wordt vastgelegd en is in een automatiseringsproces altijd leidend. Dat betekent dat als de informatie in het bronsysteem niet juist is, dat deze informatie in de rest van de omgeving ook niet juist kan zijn. Een goed uitgewerkt en uitgedacht functioneel proces is hierbij heel belangrijk. We maken in Koppeltaal gebruik van de volgende brongegevens: patiëntgegevens \(_**EPD**_\) en gegevens over de zorgaanbieders, zoals de betrokken zorgverleners. Het EPD voor de Praktijk Ondersteuner Huisarts \(POH\) voor de GGZ \(POH-GGZ\), is het Keteninformatiesysteem \(_**KIS**_\). Ook deze applicaties worden via Koppeltaal geïntegreerd met eHealthplatforms en interventies.

Naast de beschreven applicaties, gebruiken GGZ-instellingen nog een veelheid aan andere type applicaties, waaronder Elektronische Voorschrijfsystemen \(EVS\), Kantoorautomatisering, etc. Deze applicaties vallen buiten de scope van Koppeltaal.

eHealth platformen en de verschillende informatiesystemen, zoals hierboven beschreven, worden geleverd door verschillende \(ICT\) **leveranciers.** Deze leveranciers gebruiken Koppeltaal om verschillende zorginhoudelijke processen te ondersteunen rond het inzetten van digitale interventies en gegevens uit te wisselen via interacties onder de verantwoordelijkheid van een zorgaanbieder.

**Koppeltaal** zorgt voor een collectief applicatiegedrag uitgevoerd door onderling samenwerking tussen applicaties, onafhankelijk van de gekozen leveranciers, zodat deze ingezet kunnen worden voor blended care behandelingen. Koppeltaal biedt hierbij een uitwisselingsmogelijkheden doormiddel van FHIR basis resources die met behulp van profielen uitgebreid en specifieker gemaakt worden voor een specifieke toepassing.

Dienstverleners zullen onderling nadere afspraken moeten maken over de gebruikte profielen, onder de regie van Koppeltaal. Verder biedt Koppeltaal een platform aan, waar interventies gelanceerd kunnen worden. Koppeltaal is niet strikt gebonden aan één specifieke werkwijze van de zorgverlener.

### Actoren en rollen

Zoals in paragraaf 2.2 Domein en Applicatie beschreven is, zijn er verschillende type applicaties betrokken ter ondersteuning van een interactief zorgproces. Bij het inrichten van deze zorgprocessen is de verdeling van verantwoordelijkheden van belang. Hierbij maken we onderscheid tussen actoren en rollen. Actoren vertegenwoordigen personen of organisatorische eenheden, rollen vertegenwoordigen verantwoordelijkheden. Verschillende rollen kunnen worden toegekend aan een actor.

Elk type applicatie kan één of meerdere \(applicatie\) functie rollen vervullen in de context van blended care.

![Actoren en rollen binnen Koppeltaal](.gitbook/assets/3%20%281%29.jpeg)

De actoren die in de verschillende use-cases \(zie paragraaf 3 Use-cases\) ter sprake komen zijn:

* Beheerder – Een persoon die wijzigingen kan aanbrengen die van invloed zijn op andere gebruikers van een systeem.
* Patiënt – Een persoon aan wie medische hulp wordt verleend.
* Behandelaar – Een persoon die medische handelingen of activiteiten verricht.
* Derde – Een persoon die een bepaalde relatie met een Patiënt heeft ter ondersteuning van een medische behandeling.

We onderscheiden de volgende rollen \(functionele verantwoordelijkheden\).

Aan de kant van de zorgverlener voor het behandelaar/zorgteam portaal hebben we de rol: **Practitioner Portal**

Aan de kant van de cliënt in het zorgproces hebben we de rollen: **Patient Portal** en **RelatedPerson Portal**

Bij de Interventies \(zelfstandige applicaties\) die onderdeel uitmaken van een behandeling hebben we drie rollen: **Game**, **E-Learning** en **ROM**

Bij bronsystemen hebben we de rol: **EPD**

Zowel interventies als bronsystemen kunnen in andere applicatie typen \(zie Portal types\) geïntegreerd worden, als onderdeel van een blended care behandelplan.

Voor het beheer, zoals de registratie en configuratie van de portalen, interventies en bronsystemen, hebben we de rol: **Koppeltaal Support**.

## Use-cases

![Koppeltaal use-cases](.gitbook/assets/4%20%281%29.jpeg)

### UC-KT-01 Applicatie registreren

Er zijn verschillende type applicaties betrokken ter ondersteuning van een interactief zorgproces en deze zullen geregistreerd moeten worden en hiermee geïntegreerd in een Koppeltaal domein.

1. Applicaties worden door de beheerder \(Koppeltaal Support\) geregistreerd.
2. Portalen, interventies en bronsystemen worden geregistreerd binnen een Koppeltaal domein in een daarvoor bestemde Application Register.
3. Elke applicatie krijgt een Applicatie Identifier en naam.
4. Een applicatie van het type “interventie” heeft:
   1. een \(unieke\) locatie waar de interventie te vinden is \(URL\)
   2. Een overeengekomen beveiligingslocatie waar eenmalig geverifieerd wordt dat de aanroepende partij een bekende \(en geregistreerde\) partij is die kan worden vertrouwd \(Single Sign-On\) in een gegeven domein.
5. Elk geregistreerde applicatie krijgt één of meerdere functionele \(applicatie\) rollen in de context van blended care \(zie Figuur 3. Actoren en rollen\).

### UC-KT-02 \(Sub\)activiteit registreren

Alleen geregistreerde applicaties van het type “interventie” kunnen \(sub\)activiteiten registreren op basis van aandoening en behoeften van een patiënt.

1. Een interventie bevat een \(sub\)activiteiten definitie lijst met minimaal 1 activiteitsdefinitite, wat de interventie voor de patiënt te bieden heeft.
2. Elk \(sub\)activiteit is uniek identificeerbaar en heeft een beschrijving
3. De definities en omschrijvingen van \(sub\)activiteiten kunnen dynamisch gewijzigd worden. Dit resulteert niet in nieuwe activiteiten.

### UC-KT-03 Behandelplan opzetten

Na een intake van een patiënt wordt er een behandelplan opgesteld. Dit behandelplan draagt bij voor een geïntegreerd beeld van de behandeling tussen zorgverlener en patiënt.

1. In een behandelplan staan de doelen en de wijze waarop de patiënt en de behandelaar deze doelen willen bereiken.
2. Een behandelplan wordt geïnitieerd door een behandelaar voor een patiënt en is verantwoordelijk voor het behandelplan. De patiënt is standaard de uitvoerder van het behandelplan en kan aanpassingen doen op het behandelplan.
3. Een behandelplan bevat geselecteerde activiteiten die door de patiënt kunnen worden uitgevoerd.
4. Elke activiteit krijgt een start- en einddatum wanneer de activiteit wordt uitgevoerd
5. Zowel op niveau van het behandelplan als op het niveau van een activiteit, kunnen behandelaars- en derden gegevens als participanten zijn gelinkt aan het behandelplan.
6. Als een behandelplan aan een patiënt is toegewezen zijn alle geselecteerde activiteiten direct toegankelijk voor deze patiënt.
7. De behandelrelatie tussen de patiënt en behandelaar is gemaakt via het behandelplan \(en impliciet via de activiteiten daarin\).

### UC-KT-04 \(Sub\)activiteiten selecteren

Toevoegen van activiteiten vindt plaats in overleg met de patiënt op basis van gezamenlijke besluitvorming. In de keuze van activiteiten wordt rekening gehouden met de aard van de behandeling en patiënten voorkeur.

### UC-KT-05 \(Sub\)activiteit lanceren

Na het aanmaken van een behandelplan met één of meer activiteiten door een behandelaar voor een patiënt, kan de patiënt deze activiteiten in zijn portaal \(eigen omgeving binnen de context van een zorginstelling\) starten door een interventie te lanceren. Koppeltaal biedt hiermee een scala aan eHealth interventies beschikbaar.

1. Een patiënten portaal ontvangt via Koppeltaal een \(unieke\) locatie waar de interventie te vinden is \(URL\).
2. De patiënt zal via Koppeltaal deze URL openen en stuurt de volgende informatie \(context\) op om de interventie met de daarbij behorende activiteit\(en\) te kunnen lanceren:
   1. Applicatie Identifier \(gekoppeld aan een interventie\) – noodzakelijk voor Koppeltaal om de geregistreerde interventie en zijn URL op te kunnen zoeken.
   2. Activiteit Identifier. Wordt gebruikt om de juiste activiteit te identificeren.
   3. Patiënt Identifier. Wordt gebruikt om de patiënt te identificeren door de lancerende interventie.
   4. Gebruikers Identifier. Welke rol binnen een activiteit gebruikt wordt.
   5. Optionele aanvullende informatie.
   6. Authenticatie token zodat Koppeltaal kan verifiëren dat de interventie een bekende \(en geregistreerde\) applicatie is die kan worden vertrouwd.
3. Als een activiteit gestart wordt, wordt de status van de activiteit ‘in uitvoering’ gezet. Bij wijziging van de status van een activiteit, worden geabonneerden \(applicaties\) geïnformeerd \(genotificeerd\) over de status wijziging.

### UC-KT-06 \(Sub\)activiteit monitoren

Tijdens het starten en uitvoering van een activiteit door een participant, wordt de status van een activiteit geactualiseerd en doorgegeven aan Koppeltaal. Koppeltaal informeert geïnteresseerden applicaties over de geactualiseerde activiteit. Hiermee kan Koppeltaal de directe werkomgeving van de zorgverlener ondersteunen.

1. Wanneer een participant begint met het uitvoeren van een activiteit, verandert de status van ‘beschikbaar’ in ‘in uitvoering’.
2. Tijdens de uitvoering van een activiteit wordt de status up-to-date gehouden binnen de context van een behandeling.
3. Bij wijziging van de status van een activiteit, worden geabonneerden \(applicaties\) geïnformeerd \(genotificeerd\) over de status wijziging.

De geïnformeerde \(applicatie\) haalt en verwerkt de status van een activiteit voor eigen doeleinden. Hierdoor wordt bijvoorbeeld de eigenaar van een behandelplan op de hoogte gehouden van de verandering in status en kan de eigenaar van het behandelplan op zijn beurt geïnteresseerden in het behandelplan op de hoogte stellen van de wijziging.

### UC-KT-07 \(Sub\)activiteit evalueren

Aan het eind of tijdens een activiteit door een participant, kan een uitkomst van een activiteit doorgegeven worden aan Koppeltaal. Koppeltaal ondersteunt hiermee het evaluatie proces tussen cliënt en zorgaanbieder.

1. Tijdens een activiteit kan een uitkomst of de tot dusver behaalde resultaten van bijvoorbeeld een voltooide sub-sectie ingevulde vragenlijst doorgegeven worden.
2. Geabonneerden \(applicaties\) worden geïnformeerd \(genotificeerd\) over de uitkomst\(en\) of behaalde resultaten.

De geïnformeerde \(applicatie\) haalt en verwerkt de uitkomst\(en\) of behaalde resultaten van een activiteit voor eigen doeleinden.

### UC-KT-08 Participant opvoeren

Bij elke behandelplan, moeten de gebruikers of participanten: patiënt, behandelaar\(s\) en derden geregistreerd zijn binnen Koppeltaal.

1. Na de intake wordt een behandelaar of behandelteam toegewezen aan een patiënt, waarmee de behandelrelatie wordt vastgelegd.
2. Derden kunnen later toegevoegd worden. Derden worden aan een cliënt gerelateerd.
3. Koppeltaal draagt bij aan het verkrijgen van een “geïntegreerd cliëntbeeld” voor zorgverlener en patiënt. Dat wil zeggen dat Koppeltaal ervoor zorgt dat alle geïnteresseerde applicaties gesynchroniseerd worden om de identificatie van gebruikers gelijk te houden binnen een domein.
4. Een participant moet uniek identificeerbaar zijn, ook buiten Koppeltaal om. Dit om meervoudige registratie en duplicaten van participanten in een domein te voorkomen.

### UC-KT-09 Inlogverzoek naar participant

Nadat de activiteiten in een behandelplan vastgelegd zijn, kan de behandelaar een inlogverzoek versturen naar de patiënt, zodat deze aan de slag kan met de activiteiten. De patiënt ontvangt hiervoor via Koppeltaal een \(unieke\) locatie waar de interventie te vinden is \(URL\).

### UC-KT-10 Derden toegevoegd signalering

In samenspraak met de patiënt kunnen derden ingeschakeld worden bij een behandeling. Zodra de patiënt gerelateerde \(derden\) heeft ingeschakeld, wordt de behandelaar hierover geïnformeerd.

### UC-KT-11 Algemene informatie uitwisselen

Tijdens een behandeling kunnen participanten eenvoudige ongestructureerde informatie uitwisselen. Koppeltaal biedt de participanten hiermee een communicatie kanaal aan.

1. Informatie berichten bevatten alleen tekst.
2. Wanneer een participant informatie wil uitwisselen met een ander \(geregistreerd\) participant binnen de context van een behandeling, kan de participant een bericht sturen alleen naar een ander participant die bij de behandeling betrokken is.
3. Informatie berichten worden niet als notificatie berichten gebruikt.

## Gegevensmodel

De gegevensuitwisseling gebeurt via berichtenuitwisseling en is gebaseerd op een aantal standaarden: met name HTTP, **HL7 FHIR DSTU 1\(v0.0.82\)** en relevante onderdelen van de HL7 standaard.

De kern van FHIR wordt gevormd door herbruikbare bouwstenen, de zogenaamde **FHIR resources**, waarmee oplossingen voor _uitwisseling van_ zorginhoudelijke _gegevens_ kunnen worden gebouwd. Elk bericht heeft een \(interactie\) type en hiermee kan bepaalde functionaliteit gerealiseerd worden binnen Koppeltaal \(zie paragraaf 5 [Interacties](https://confluence.vzvz.nl/display/AK/Interacties)\).

Koppeltaal heeft een set berichten gedefinieerd waarmee de Koppeltaal use-cases kunnen worden afgedekt. Logische voorwaarde is dat de betrokken applicaties de benodigde berichten ondersteunen \(d.w.z. de structuur van de berichten kennen en de inhoud volledig kunnen interpreteren\). In de praktijk zien we dat verschillende applicaties, zoals portalen, interventies, platformen en EPD’s in Koppeltaal gecombineerd worden.

Omdat Koppeltaal gebruik maakt van FHIR DSTU1 zijn er bepaalde \(Koppeltaal\) resource concepten die niet gedefinieerd zijn voor FHIR of die buiten het interessegebied van HL7 liggen. Hiervoor gebruiken we de _Other_ resource, zodat we ook met specifieke Koppeltaal resources kunnen omgaan.

![Koppeltaal FHIR Resource DSTU1](.gitbook/assets/5%20%282%29.jpeg)

### MessageHeader

Koppeltaal v1.3.x is gebaseerd op FHIR messaging. Dat wil zeggen dat elk verzoek bericht verzonden wordt van een bron naar een bestemming, wanneer er een gebeurtenis \(event\) plaatsvindt. Het verzoekbericht bestaat uit een bundel die wordt geïdentificeerd door het type "bericht", waarbij de eerste resource in de bundel altijd een **MessageHeader** resource is. De MessageHeader bron heeft een code - interactie - die de aard van het verzoekbericht identificeert, en het draagt ​​ook aanvullende metagegevens van het verzoek mee.

De ontvanger van het bericht verwerkt het verzoek en retourneert eventueel een antwoordbericht met het resultaat van de verwerking van het bericht en eventuele aanvullende response resources die hierbij nodig zijn.

### CarePlan

Het **CarePlan** is \(nu\) de meest gebruikte resource, binnen Koppeltaal 1.3.x. Het CarePlan wordt als raamwerk gebruikt \(en is een extractie of een vertaling van een behandelplan\) om een blended care behandeling op te starten en te volgen. Hierin worden activiteiten, die in het kader van de zorg, aan één patiënt toegewezen. Verder worden de betrokkenen \(participanten\) bij de behandeling in het CarePlan vastgelegd.

### Participant

Participanten betrokken bij een behandeling, kunnen verschillende rollen hebben. Verder kunnen participanten uit meerdere disciplines bestaan die in een behandelteam zijn gegroepeerd. De volgende participanten onderscheiden we:

* **Patient** \(patiënt\) die de zorg ontvangt of krijgt door de activiteiten uit te voeren, dat onderdeel is van een behandeling.
* **Practitioner** \(Behandelaar\) die direct of indirect betrokken is bij de behandeling en het behandelplan opstelt. De behandelaar vertegenwoordigt een organisatie \(**Organization**\).
* **RelatedPerson** is familie, vrienden of ervaringsdeskundigen die zijn uitgenodigd om mee te denken over de inhoud van de behandeling.
* **CareTeam** \(behandelteam\) is een groep deskundigen en/of behandelaars die uit meerdere disciplines bestaan en die ingezet kunnen worden bij een behandeling. Het Careteam vertegenwoordigt een organisatie \(**Organization**\).

### ActivityDefinition

ActivityDefinition maakt het mogelijk aan de hand van een bepaalde activiteit definitie deze uit te kunnen gaan voeren, onafhankelijk van de uitvoercontext van een bepaalde patiënt of behandelaar. Elke activiteit is gekoppeld aan één **Application** \(**Device**\) en een applicatie kan één of meerdere activiteiten ondersteunen.

### CarePlanActivityStatus

**CarePlanActivityStatus** beschrijft in detail de status en voortgang van een activiteit.

### CarePlanActivityResult

**CarePlanActivityResult** beschrijft de uitkomst van een activiteit, inclusief gegeven antwoorden en berekende scores. Het verzamelt en groepeert observaties en kan verwijzingen maken naar vragenlijsten die de antwoorden bevatten op vragen die zijn ingevoerd door een participant.

### UserMessage

**UserMessage** wordt gebruikt om informatieberichten uit te kunnen wisselen tussen participanten.

## Interacties

In deze paragraaf worden de verschillende interacties beschreven tussen de verschillende applicaties. Het doel van deze paragraaf is de toepassing van Koppeltaal voor de verschillende use-cases weer te geven, alsmede de vereisten en aanpassingen in Koppeltaal toe te lichten.

Er zijn verschillende applicatie leveranciers betrokken ter ondersteuning van een interactief zorgproces en deze zullen gecertificeerd en geregistreerd moeten worden. Het registratie proces, welke applicaties gebruik willen maken van Koppeltaal, is een \(handmatig\) configuratie proces. Indien betrokken applicatie leveranciers onderling informatie willen uitwisselen, zullen ze in hetzelfde domein aangemeld en geregistreerd moeten worden. Dit registratie proces worden door Koppeltaal Support uitgevoerd.

Na het registratie proces kan begonnen worden met de uitwisseling van informatie \(FHIR resources\), dit gebeurt via voor gedefinieerde interacties tussen de geregistreerde applicaties. Elke interactie \(tussen applicaties\) bestaat uit een FHIR MessageHeader, gevolgd door andere FHIR resources \(zie paragraaf 4 Gegevensmodel\). Een codering in de MessageHeader geeft aan om wat voor soort interactie het gaat. Per type applicatie zijn er verschillende interacties beschikbaar.

In de interactie laag wordt er niet meet over een cliënt gesproken maar hanteren we de term patiënt.

![Interacties gegroepeerd](.gitbook/assets/6%20%281%29.jpeg)

### Informatie zoeken en ophalen

Koppeltaal heeft voor elke applicatie een bestemmingsqueue waarin de gegevens \(tijdelijk\) worden opgeslagen, die nog niet door de betreffende applicatie is opgehaald en verwerkt. Hierdoor hoeven applicaties niet continue en direct in verbinding te staan met andere applicaties. Elke geregistreerde applicatie kan op elk moment Koppeltaal bevragen met de specifieke GET \(opvragen\) API aanroep \(HTTP operatie\) of er berichten klaar staan met een bepaalde MessageHeader code, status of patiënt dossier \(de GetMessageHeaders interactie\). Koppeltaal stuurt op deze specifieke aanvraag een bundel met MessageHeaders terug naar de betreffende applicatie die matchen met het verzoek. Vervolgens kan de berichtinhoud aan de hand van de MessageHeader.Id opgehaald worden \(de GetMessage interactie\). Bij deze interactie wordt er geen gebruik gemaakt van een MessageHeader omdat er geen communicatie is tussen applicaties.

![Informatie zoeken en ophalen](.gitbook/assets/7.jpeg)

#### Notificeren

Om het bevragen van Koppeltaal te ontlasten, biedt Koppeltaal een functie aan om notificaties \(notification\) te versturen naar applicaties, binnen een domein. Hiermee halen de applicaties pas gegevens op als de gegevens bij Koppeltaal, in de bestemmingsqueue van de te ontvangen applicatie, klaar staan. Het is aan de applicatie leveranciers de keuze of ze hiervan gebruik willen maken. Tijdens het registratie proces van de applicaties, kan dit per applicatie geconfigureerd worden om een notificatie te willen ontvangen van Koppeltaal. Elke applicatie kan via een abonnement aangeven, in welke interacties hij geïnteresseerd is. Voor Koppeltaal 1.3.x wordt dit door de beheerder van Koppeltaal Support ingevoerd.

### \(Sub\)activiteiten registreren en lezen

Koppeltaal bevat een applicatie register dat de definities registreert van activiteiten van een interventie. Deze worden aangemeld middels de interactie CreateOrUpdateActivityDefinition welke via het certificeringsproces getest zijn op een goede en passende werking binnen Koppeltaal. De structuur van de activiteiten definities wordt gerepresenteerd door een lijst van sub-activiteiten die horen bij deze interventie \(bijv. level in een game, sectie van een ROM-vragenlijst, etc.\). Het proces van het creëren of wijzigen van de activiteiten definities is via een POST \(creëren\) of PUT \(wijzigen\) API voor elke ActivityDefinition aanroep door de interventie \(applicatie instantie\) mogelijk. Het wijzigen van de definities zal niet in nieuwe activiteiten resulteren.

De activiteiten definities kunnen worden opgevraagd met een specifieke GET \(opvragen\) API aanroep. Deze aanroep biedt de Activity Definities aan die beschikbaar worden gesteld door de interventie. Deze Activity Definities kunnen gebruikt worden door een CarePlan \(via CarePlan.activity\).

![Registratie en lezen van activiteiten](.gitbook/assets/8.jpeg)

### Aanmaken CarePlan

Na een intake wordt er een CarePlan aangemaakt. Een CarePlan is een \(FHIR resource\) extractie \(uittreksel\) of een vertaling van een behandelplan. Hierin worden de activiteiten vastgelegd.

Een CarePlan is gemaakt door een behandelaar voor een patiënt. De patiënt is standaard de uitvoerder van het CarePlan. Een CarePlan wordt aangemaakt middels de interactie CreateOrUpdateCarePlan met CarePlan als FocalResource.

Een CarePlan bevat één of meer activiteiten die door de patiënt kunnen worden uitgevoerd. Zowel op niveau van het CarePlan als op het niveau van een Activity \(activiteit\) kunnen Practitioner \(behandelaar\) en RelatedPerson \(derde\) resources zijn gelinkt via het element participant in het CarePlan.

Binnen Koppeltaal 1.3.5.is het CareTeam geïntroduceerd. Het is de verwachting dat Practitioner resources, in toekomstige versies van Koppeltaal, gelinkt zullen worden aan een CareTeam. Deze worden nu aan het CarePlan gelinkt.

Als een CarePlan aan een patiënt is toegewezen zijn alle geselecteerde activiteiten direct toegankelijk voor de patiënt. De relatie tussen de patiënt en behandelaar is gemaakt via het CarePlan \(en impliciet via de activiteiten daarin\).

![CarePlan aanmaken en toewijzen](.gitbook/assets/9.jpeg)

### Participanten opvoeren en uitwisselen

Om de synchronisatie van een Participant bij een behandeling tussen applicaties binnen een domein mogelijk te maken, zijn er de volgende interacties gedefinieerd: CreateOrUpdatePatient met Patient als FocalResource, CreateOrUpdatePractitioner met Practitioner als FocalResource en CreateOrUpdateRelatedPerson met RelatedPerson als FocalResource.

Het doel van deze synchronisatie is om de identificatie van een participant \(patiënt, derde of behandelaar\) gelijk te trekken tussen alle applicaties binnen een domein. De identificatie van de participanten is in Koppeltaal één van de bouwblokken voor het kunnen starten van interventies.

Als voorbeeld, een nieuwe patiënt wordt ingeschreven in het EPD \(bronsysteem\) en zal een set van acties triggeren:

* het maken van een CreateOrUpdatePatient interactie voor de nieuwe patiënt
* het posten van de Patient \(resource\) gegevens
* het notificeren van geabonneerde applicaties
* het ophalen van de Patient \(resource\) gegevens bij Koppeltaal
* de verdere \(lokale\) afhandeling binnen de applicaties \(Portaal, Interventie, etc.\) om een account voor deze gebruiker te kunnen regelen en de gebruiker ID te koppelen

![Participanten synchronisatie](.gitbook/assets/10.jpeg)

### Activiteit monitoren en evalueren

Er kan een set van interacties gebruikt worden om de status van een activiteit binnen een behandelplan actueel te houden en deze vervolgens te kunnen monitoren.

* De [CreateOrUpdateCarePlan ]()interactie: Deze interactie bevat de informatie over het behandelplan en initieert de status van het plan. Als een behandelaar \(Practitioner resource\) een of meerdere activiteiten toewijst aan een patiënt \(Patient resource\), wordt een CarePlan resource gemaakt met de aangegeven activiteiten en de status wordt op ‘Available’ \(beschikbaar\) gezet. Er kunnen daarnaast activiteiten toegewezen worden aan derden \(RelatedPerson resource\).
* De [UpdateCarePlanActivityStatus]() interactie: Deze interactie wordt gebruikt om de status van activiteiten binnen het behandelplan up-to-date te houden met CarePlanActivityStatus als FocalResource. Merk op dat een statuswijziging van één CarePlanActivity een statusverandering in een andere CarePlanActivity kan veroorzaken. Als een CarePlanActivity bijvoorbeeld afhankelijk is van een andere, kan het beëindigen van een CarePlanActivity ertoe leiden dat afhankelijke CarePlanActivities beschikbaar komen. Als er meerdere partijen betrokken zijn bij een behandelplan, zullen er meerdere activiteiten per partij binnen het behandelplan aangemaakt zijn.
* Zodra een CarePlanActivity beschikbaar is, kunnen er resultaten worden gegenereerd en geëvalueerd. Resultaten worden gecommuniceerd met behulp van de [CreateOrUpdateCarePlanActivityResult]() interactie, met CarePlanActivityResult als FocalResource. Resultaten kunnen tussentijdse resultaten zijn en als zodanig onderhevig zijn aan veranderingen.

Wanneer de patiënt of gerelateerde persoon bijvoorbeeld begint met het uitvoeren van een activiteit uit een behandeling \(CarePlanActivity\), verandert zijn status van 'beschikbaar' in 'in uitvoering'.

Vervolgens wordt de interactie UpdateCarePlanActivityStatus verzonden met de CarePlanActivity waarvan de status is gewijzigd. Dit is bedoeld om de applicatie die eigenaar is van het CarePlan op de hoogte te stellen van de verandering in status. De verantwoordelijke toepassing kan vervolgens beurtelings een interactie CreateOrUpdateCarePlan verzenden om alle toepassingen die geïnteresseerd zijn in het CarePlan als geheel \(in plaats van specifieke activiteiten in het CarePlan\) op de hoogte te stellen van de wijziging.

![Activiteiten monitoren](.gitbook/assets/11.jpeg)

### Informatie uitwisselen

Informatie berichten tussen participanten wordt gebruikt om eenvoudige ongestructureerde informatie uit te kunnen uitwisselen. Dit gebeurt via de [CreateOrUpdateUserMessage]() met UserMessage als FocalResource. Deze berichten bevatten alleen tekst.

Merk op dat een user bericht niet als notificatie bericht gebruikt wordt.

Als voorbeeld, een patiënt heeft een specifieke vraag over een behandeling aan een behandelaar. Dit zal de volgende acties triggeren:

* het maken van een CreateOrUpdateUserMessage interactie voor de patiënt
* het posten van de UserMessage \(resource\) gegevens
* het notificeren van geabonneerde informatie systemen \(Practitioner Portaal\)
* het ophalen van de UserMessage \(resource\) gegevens bij Koppeltaal door de behandelaar. Het ophalen van de UserMessage gebeurt via 5.1 Informatie zoeken en ophalen.

![Informatie-uitwisseling](.gitbook/assets/12.jpeg)

### Het lanceren van een interventie

Het lanceren van een interventie gaat volgens de OAuth 2.0 standaard en SMART-on-FHIR voorschriften. Na het aanmaken van een CarePlan met één of meer activiteiten door een behandelaar voor een patiënt, kan de patiënt deze activiteiten in zijn portaal \(eigen omgeving binnen de context van een zorginstelling\) starten door een interventie te lanceren. Hiervoor gebruikt de patiënt een unieke interventie adres \(URL\) die in het portaal wordt klaargezet. Zodra de patiënt deze URL opent wordt de patiënt via Koppeltaal naar de interventie geleidt binnen de context van een behandeling \(zie PostLaunchRequest\). De interventie ontvangt de context van de LaunchRequest en een Autorisatie endpoint waarmee hij om toegang tot de gegevens vraagt bij Koppeltaal. Koppeltaal geeft de interventie vervolgens een access token waarmee de interventie vervolgens Koppeltaal kan updaten over de voortgang van bepaalde activiteiten die door een participant wordt uitgevoerd. Als de acces token verlopen is kan de interventie om een refresh token vragen.

![Interventie lanceren](.gitbook/assets/13.jpeg)

## Use-case versus interacties

In het volgende overzicht ziet men met welke interacties de verschillende use-cases ondersteund. De verschillende interacties realiseren de huidige functionaliteit van Koppeltaal.

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Use-case</b>
      </th>
      <th style="text-align:left"><b>Interactie</b>
      </th>
      <th style="text-align:left"><b>Omschrijving</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>UC-KT-01</p>
        <p>Applicatie registreren</p>
      </td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">Applicatie per zorgbehoefte geregistreerd in het Koppeltaal domein. Hier
        zijn geen interacties tussen systemin voor gedefinieerd maar moet handmatig
        door een beheerder (Koppeltaal Support) geconfigueerd worden.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>UC-KT-02</p>
        <p>(Sub)activiteiten registreren</p>
      </td>
      <td style="text-align:left">CreateOrUpdateActivityDefinition</td>
      <td style="text-align:left">Elke interventie moet tenminste &#xE9;&#xE9;n activiteit hebben geregistreerd
        en kan aangepast danwel uitgebreidt worden</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>UC-KT-03/</p>
        <p>UC-KT-04/</p>
        <p>UC-KT-09</p>
        <p>Behandelplan starten</p>
      </td>
      <td style="text-align:left">CreateOrUpdateCarePlan</td>
      <td style="text-align:left">Na een intake wordt er een behandelplan opgesteld en activiteiten toegekend
        aan een pati&#xEB;nt. Nadat activiteiten toegekend zijn wordt pati&#xEB;nt
        genotificeerd via inlogverzoek. Dit behandelplan draagt bij voor een ge&#xEF;ntegreerd
        pati&#xEB;ntenbeeld tussen zorgverlener en pati&#xEB;nt.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>UC-KT-05</p>
        <p>Interventie lanceren</p>
      </td>
      <td style="text-align:left">PostLaunchRequest</td>
      <td style="text-align:left">OAuth 2.0 standaard en SMART-on-FHIR voorschriften.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>UC-KT-06</p>
        <p>Voortgang monitoren</p>
      </td>
      <td style="text-align:left">UpdateCarePlanActivityStatus</td>
      <td style="text-align:left">Voortgang en status van een activiteit delen en ontvangen van een interventie.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>UC-KT-07</p>
        <p>Activiteit evalueren</p>
      </td>
      <td style="text-align:left">CreateOrUpdateCarePlanActivityResult</td>
      <td style="text-align:left">Uitslagen en resultaten delen en ontvangen van een interventie</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>UC-KT-08/</p>
        <p>UC-KT-10</p>
        <p>Gebruikers aanmaken</p>
      </td>
      <td style="text-align:left">
        <p>CreateOrUpdatePatient</p>
        <p>CreateOrUpdatePractitioner</p>
        <p>CreateOrUpdateRelatedPerson</p>
      </td>
      <td style="text-align:left">Verschillende typen gebruikers kunnen worden aangemaakt. Na opvoeren van
        een gebruiker worden alle ge&#xEF;ntereseerde applicaties gesynchroniseerd
        en kunnen andere applicaties de gegevens aanvullen.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>UC-KT-11</p>
        <p>Informatie uitwisselen</p>
      </td>
      <td style="text-align:left">CreateOrUpdateMessage</td>
      <td style="text-align:left">Algemene informatie delen en ontvangen tussen participanten</td>
    </tr>
  </tbody>
</table>

