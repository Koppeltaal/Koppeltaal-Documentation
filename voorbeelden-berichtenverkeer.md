---
description: >-
  Koppeltaal is in de loop der tijd doorontwikkeld tot v1.3.x. Met de
  introductie van resource versionering is de implementatie lastig voor de
  IT-deelnemers. Hiervoor hebben we voorbeelden toegevoegd.
---

# Voorbeelden Koppeltaal berichten

## Aanmaken van een CarePlan

Een behandelaar maakt via een portaal, een nieuw behandelplan aan. Hiervoor wordt een FHIR bericht verstuurd naar de Koppeltaal server. Dit bericht kan als XML of JSON content aangeboden worden. Elke nieuwe interactie begint met een MessageHeader met daarin een `extension.valueResource.reference` naar een Patient en een `data.reference` naar de focal resource. De aangeboden focal resource heeft op dat moment geen versie, die moet door de Koppeltaal server uitgegeven worden.

Volgende voorbeeld is de MessageHeader in XML formaat.

```markup
<feed xmlns="http://www.w3.org/2005/Atom">
   <id>urn:uuid:97b7a1e2-ca51-415e-b06c-fc8564a979fa</id>
   <category term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#PythonAdapterTesting" label="PythonAdapterTesting" scheme="http://hl7.org/fhir/tag/security" />
   <category term="http://hl7.org/fhir/tag/message" scheme="http://hl7.org/fhir/tag" />
   <entry>
      <id>http://127.0.0.1:37527/app/fhir/Koppeltaal/MessageHeader/139882808154208</id>
      <content type="text/xml">
         <MessageHeader xmlns="http://hl7.org/fhir" id="ref002">
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient">
               <valueResource>
                  <reference value="http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203" />
               </valueResource>
            </extension>
            <identifier value="3f03e865-e87c-4337-922c-5be69dbcd243" />
            <timestamp value="2020-08-13T02:30:41+00:00" />
            <event>
               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents" />
               <code value="CreateOrUpdateCarePlan" />
               <display value="CreateOrUpdateCarePlan" />
            </event>
            <source id="ref001">
               <name value="New integration for 'app.None'" />
               <software value="Koppeltaal Adapter" />
               <version value="1.3.x" />
               <endpoint value="http://127.0.0.1:37527/app/fhir/Koppeltaal" />
            </source>
            <data>
               <reference value="http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212" />
            </data>
         </MessageHeader>
      </content>
   </entry>
   ...
```

Dezelfde MessageHeader in JSON formaat.

```javascript
{
  "resourceType": "Bundle",
  "id": "urn:uuid:97b7a1e2-ca51-415e-b06c-fc8564a979fa<",
  "category": [
    {
      "term": "http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#PythonAdapterTesting",
      "label": "PythonAdapterTesting",
      "scheme": "http://hl7.org/fhir/tag/security"
    },
    {
      "term": "http://hl7.org/fhir/tag/message",
      "scheme": "http://hl7.org/fhir/tag"
    }
  ],
  "entry": [
    {
      "content": {
        "id": "ref002",
        "extension": [
          {
            "url": "http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient",
            "valueResource": {
              "reference": "http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203"
            }
          }
        ],
        "identifier": "3f03e865-e87c-4337-922c-5be69dbcd243",
        "timestamp": "2020-08-13T02:30:41+00:00",
        "data": [
          {
            "reference": "http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212"
          }
        ],
        "event": {
          "code": "CreateOrUpdateCarePlan",
          "system": "http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents",
          "display": "CreateOrUpdateCarePlan"
        },
        "source": {
          "id": "ref001",
          "name": "New integration for 'app.None'",
          "software": "Koppeltaal Adapter",
          "version": "1.3.x",
          "endpoint": "http://127.0.0.1:37527/app/fhir/Koppeltaal"
        },
        "resourceType": "MessageHeader"
      },
      "id": "http://127.0.0.1:37527/app/fhir/Koppeltaal/MessageHeader/139882808154208"
    },
    ...
```

Alle resources die met dit bericht meekomen, hebben een selflink, zonder versie in de `link href`

Voorbeeld van resources in XML formaat.

```markup
  <entry>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212" />
      <content type="text/xml">
         <CarePlan xmlns="http://hl7.org/fhir" id="ref006">
            ...
         </CarePlan>
      </content>
   </entry>
   <entry>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203" />
      <content type="text/xml">
         <Patient xmlns="http://hl7.org/fhir" id="ref009">
            ...
         </Patient>
      </content>
   </entry>
   <entry>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/Practitioner/751512208" />
      <content type="text/xml">
         <Practitioner xmlns="http://hl7.org/fhir" id="ref012">
            ...
         </Practitioner>
      </content>
   </entry>
</feed>
```

Voorbeeld van resources in JSON formaat.

```javascript
{
      "content": {
        "id": "ref006",
        ...
        "resourceType": "CarePlan"
      },
      "id": "http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212",
      "link": [
        {
          "rel": "self",
          "href": "http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212"
        }
      ]
    },
      "content": {
        "id": "ref009",
        ...
        "resourceType": "Patient"
      },
      "id": "http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203",
      "link": [
        {
          "rel": "self",
          "href": "http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203"
        }
      ]
    },
      "content": {
        "id": "ref012",
        ...
        "resourceType": "Practitioner"
      },
      "id": "http://127.0.0.1:37527/app/fhir/Koppeltaal/Practitioner/751512208",
      "link": [
        {
          "rel": "self",
          "href": "http://127.0.0.1:37527/app/fhir/Koppeltaal/Practitioner/751512208"
        }
      ]
    }
  ]
}
```

Koppeltaal server beantwoordt het binnenkomend bericht, en verstuurd een antwoord naar de verzender waarin staat wat de versies zijn van de verschillende resources.

```markup
<feed
    xmlns="http://www.w3.org/2005/Atom">
    <id>urn:uuid:5931e3dc-243b-4f29-9200-78c238df9771</id>
    <category term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#Dev" label="Dev" scheme="http://hl7.org/fhir/tag/security"/>
    <category term="http://hl7.org/fhir/tag/message" scheme="http://hl7.org/fhir/tag"/>
    <entry>
        <id>urn:uuid:cab1c156-125c-49d2-9765-cab3e9fddff2</id>
        <content type="text/xml">
            <MessageHeader
                xmlns="http://hl7.org/fhir">
                <identifier value="3f03e865-e87c-4337-922c-5be69dbcd243"/>
                <timestamp value="2020-08-15T09:33:55+02:00"/>
                <event>
                    <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents"/>
                    <code value="CreateOrUpdateCarePlan"/>
                    <display value="CreateOrUpdateCarePlan"/>
                </event>
                <response>
                    <identifier value="03e2edd0-ef69-49ed-97e9-b075a45a118a"/>
                    <code value="ok"/>
                </response>
                <source>
                    <name value=""/>
                    <software value=""/>
                    <version value=""/>
                    <endpoint value="https://demo.koppeltaal.nl/FHIR/Koppeltaal/Mailbox"/>
                </source>
                <data>
                    <reference value="http://demo.koppeltaal.nl/CarePlan/751512212/_history/2020-08-15T07:33:55:708.2583"/>
                </data>
                <data>
                    <reference value="http://demo.koppeltaal.nl/Patient/751512203/_history/2020-08-15T07:33:55:708.2583"/>
                </data>
                <data>
                    <reference value="http://demo.koppeltaal.nl/Practitioner/751512208/_history/2020-08-15T07:33:55:708.2583"/>
                </data>
            </MessageHeader>
        </content>
    </entry>
</feed>
```

De verzender moet de versie van de resources in zijn eigen administratie bijhouden zodat de verzender later mutaties op de resources kan uitvoeren. Mutaties mogen alleen op de meest recente versie van resources uitgevoerd worden.

Applicaties die geabonneerd zijn op de `CreateOrUpdateCarePlan` krijgen een verrijkt bericht binnen waar de versies van de resources zijn toegevoegd.

```markup
  <feed xmlns="http://www.w3.org/2005/Atom">
   <id>urn:uuid:97b7a1e2-ca51-415e-b06c-fc8564a979fa</id>
   <updated>2020-08-13T02:30:41Z</updated>
   <category term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#PythonAdapterTesting" label="PythonAdapterTesting" scheme="http://hl7.org/fhir/tag/security" />
   <category term="http://hl7.org/fhir/tag/message" scheme="http://hl7.org/fhir/tag" />
   <entry>
      <id>http://127.0.0.1:37527/app/fhir/Koppeltaal/MessageHeader/139882808154208</id>
      <updated>2020-08-13T02:30:44+00:00</updated>
      <content type="text/xml">
         <MessageHeader xmlns="http://hl7.org/fhir" id="ref002">
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient">
               <valueResource>
                  <reference value="http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203" />
               </valueResource>
            </extension>
            <identifier value="3f03e865-e87c-4337-922c-5be69dbcd243" />
            <timestamp value="2020-08-13T02:30:41+00:00" />
            <event>
               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents" />
               <code value="CreateOrUpdateCarePlan" />
               <display value="CreateOrUpdateCarePlan" />
            </event>
            <source id="ref001">
               <name value="New integration for 'app.None'" />
               <software value="Koppeltaal Adapter" />
               <version value="1.3.x" />
               <endpoint value="http://127.0.0.1:37527/app/fhir/Koppeltaal" />
            </source>
            <data>
               <reference value="http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212/_history/2020-08-15T07:33:55:708.2583" />
            </data>
         </MessageHeader>
      </content>
   </entry>
   <entry>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212/_history/2020-08-15T07:33:55:708.2583" />
      <content type="text/xml">
         <CarePlan xmlns="http://hl7.org/fhir" id="ref006">
            ...
         </CarePlan>
      </content>
   </entry>
   <entry>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203/_history/2020-08-15T07:33:55:708.2583" />
      <content type="text/xml">
         <Patient xmlns="http://hl7.org/fhir" id="ref009">
            ...
         </Patient>
      </content>
   </entry>
   <entry>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/Practitioner/751512208/_history/2020-08-15T07:33:55:708.2583" />
      <content type="text/xml">
         <Practitioner xmlns="http://hl7.org/fhir" id="ref012">
            ...
         </Practitioner>
      </content>
   </entry>
</feed>
```

## Updaten van een CarePlan

Bij het aanpassen van een CarePlan moet men de juiste versies van de resources gebruiken om een mutatie doorgevoerd te krijgen door de Koppeltaal server.

```markup
<feed xmlns="http://www.w3.org/2005/Atom">
   <id>urn:uuid:97b7a1e2-ca51-415e-b06c-fc8564a959f3</id>
   <category term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#PythonAdapterTesting" label="PythonAdapterTesting" scheme="http://hl7.org/fhir/tag/security" />
   <category term="http://hl7.org/fhir/tag/message" scheme="http://hl7.org/fhir/tag" />
   <entry>
      <id>http://127.0.0.1:37527/app/fhir/Koppeltaal/MessageHeader/139442808158532</id>
      <content type="text/xml">
         <MessageHeader xmlns="http://hl7.org/fhir" id="ref002">
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient">
               <valueResource>
                  <reference value="http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203" />
               </valueResource>
            </extension>
            <identifier value="3f03e865-e87c-4337-922d-5ba69dbc3412" />
            <timestamp value="2020-08-15T02:30:41+00:00" />
            <event>
               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents" />
               <code value="CreateOrUpdateCarePlan" />
               <display value="CreateOrUpdateCarePlan" />
            </event>
            <source id="ref001">
               <name value="New integration for 'app.None'" />
               <software value="Koppeltaal Adapter" />
               <version value="1.3.x" />
               <endpoint value="http://127.0.0.1:37527/app/fhir/Koppeltaal" />
            </source>
            <data>
               <reference value="http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212/_history/2020-08-15T07:33:55:708.2583" />
            </data>
         </MessageHeader>
      </content>
   </entry>
    <entry>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212/_history/2020-08-15T07:33:55:708.2583" />
      <content type="text/xml">
         <CarePlan xmlns="http://hl7.org/fhir" id="ref006">
            ...
         </CarePlan>
      </content>
   </entry>
   <entry>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203/_history/2020-08-15T07:33:55:708.2583" />
      <content type="text/xml">
         <Patient xmlns="http://hl7.org/fhir" id="ref009">
            ...
         </Patient>
      </content>
   </entry>
   <entry>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/Practitioner/751512208/_history/2020-08-15T07:33:55:708.2583" />
      <content type="text/xml">
         <Practitioner xmlns="http://hl7.org/fhir" id="ref012">
            ...
         </Practitioner>
      </content>
   </entry>
</feed>
```

## Verkeerde resource versie

Als er aan een Koppeltaal versie 1.3.5 of een hogere compatibele applicatie een 409 HTTP statuscode wordt teruggegeven, omdat één of meer verkeerde resource versies zijn meegestuurd, worden hierin de resources teruggegeven waarvan de verkeerde versie was meegestuurd. Dit gebeurt in de volgende response:

```markup
<OperationOutcome xmlns="http://hl7.org/fhir">
    <text>
        <status value="generated"/>
        <div xmlns="http://www.w3.org/1999/xhtml">
            <p xmlns=""/>
        </div>
    </text>
    <issue>
        <severity value="error"/>
        <type>
            <system value="http://hl7.org/fhir/issue-type"/>
            <code value="conflict"/>
        </type>
        <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/OperationOutcome#IssueResource">
            <valueResource>
                <reference value="http://demo.koppeltaal.nl/fhir/Patient/751512203" />
            </valueResource>
        </extension>
        <details value="The specified resource version is not correct."/>
    </issue>
    <issue>
        <severity value="error"/>
        <type>
            <system value="http://hl7.org/fhir/issue-type"/>
            <code value="conflict"/>
        </type>
        <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/OperationOutcome#IssueResource">
            <valueResource>
                <reference value="http://demo.koppeltaal.nl/fhir/Practitioner/751512208" />
            </valueResource>
        </extension>
        <details value="The specified resource version is not correct."/>
    </issue>
</OperationOutcome>
```

## Onbekende resource

Als er een bericht verstuurd wordt naar de Koppeltaal Server met daarin een resource die Koppeltaal niet ondersteunt \(in dit voorbeeld ‘Condition’\), wordt de volgende respons geretourneerd:

```markup
<OperationOutcome xmlns="http://hl7.org/fhir">
    <text>
        <status value="generated"/>
        <div xmlns="http://www.w3.org/1999/xhtml">
            <p xmlns="">
                at IExtOnFHIR FHIRExceptionAction.Run(ActionInput, Input, ActionOutputRequest, RequestedOutputs) ...
            </p>
        </div>
    </text>
    <issue>
        <severity value="error"/>
        <details value="The resource type 'Condition' is not supported"/>
    </issue>
</OperationOutcome>
```

## Interacties

### CreateOrUpdateCarePlan

Deze interactie is opgebouwd uit een update van het CarePlan, Organization, Patient, Practitioner en CareTeam.

```markup
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
   <id>urn:uuid:e9b3a989-9765-4340-9591-515e7697feb6</id>
   <category term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#VZVZTest" label="VZVZTest" scheme="http://hl7.org/fhir/tag/security" />
   <category term="http://hl7.org/fhir/tag/message" scheme="http://hl7.org/fhir/tag" />
   <entry>
      <id>https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/MessageHeader/90e4b6d1-66f1-4281-9c36-11cd635a387f</id>
      <content type="text/xml">
         <MessageHeader xmlns="http://hl7.org/fhir" id="90e4b6d1-66f1-4281-9c36-11cd635a387f">
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient">
               <valueResource>
                  <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Patient/d4849156-d961-45bb-a16c-e929209c2dc5" />
               </valueResource>
            </extension>
            <identifier value="90e4b6d1-66f1-4281-9c36-11cd635a387f" />
            <timestamp value="2020-10-12T11:34:52+02:00" />
            <event>
               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents" />
               <code value="CreateOrUpdateCarePlan" />
               <display value="CreateOrUpdateCarePlan" />
            </event>
            <source>
               <name value="VZVZ_FunctTest" />
               <software value="VZVZ_FunctTest" />
               <version value="1.x" />
               <endpoint value="https://testprovidemb.vitalhealthsoftware.com/" />
            </source>
            <data>
               <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/CarePlan/7d676a2f-edec-4dc4-8f9b-910474663bbb" />
            </data>
         </MessageHeader>
      </content>
   </entry>
   <entry>
      <id>https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/CarePlan/7d676a2f-edec-4dc4-8f9b-910474663bbb</id>
      <link rel="self" href="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/CarePlan/7d676a2f-edec-4dc4-8f9b-910474663bbb" />
      <content type="text/xml">
         <CarePlan xmlns="http://hl7.org/fhir">
            <patient>
               <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Patient/d4849156-d961-45bb-a16c-e929209c2dc5" />
            </patient>
            <status value="active" />
            <participant>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ParticipantCareTeam">
                  <valueResource>
                     <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/CareTeam/e9ff45d9-d3f5-4d24-ac45-ef7755829ed3" />
                  </valueResource>
               </extension>
               <role>
                  <coding>
                     <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanParticipantRole" />
                     <code value="Caregiver" />
                     <display value="Caregiver" />
                  </coding>
               </role>
               <member>
                  <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Practitioner/1cd70739-175b-4672-8f22-1542d00ee847" />
               </member>
            </participant>
            <activity id="743e986d-1519-4be5-871f-bd434009d7ee">
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityIdentifier">
                  <valueString value="743e986d-1519-4be5-871f-bd434009d7ee" />
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityDefinition">
                  <valueString value="MHC-SF" />
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityStatus">
                  <valueCoding>
                     <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus" />
                     <code value="Available" />
                     <display value="Available" />
                  </valueCoding>
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityKind">
                  <valueCoding>
                     <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityKind" />
                     <code value="Questionnaire" />
                     <display value="Questionnaire" />
                  </valueCoding>
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#StartDate">
                  <valueDateTime value="2020-10-12T00:00:00+02:00" />
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivity">
                  <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivityIdentifier">
                     <valueString value="f83e4e57-fcdf-440e-b568-f8a9dad690ca" />
                  </extension>
                  <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivityStatus">
                     <valueCoding>
                        <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus" />
                        <code value="Available" />
                        <display value="Available" />
                     </valueCoding>
                  </extension>
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#Participant">
                  <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ParticipantMember">
                     <valueResource>
                        <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Practitioner/1cd70739-175b-4672-8f22-1542d00ee847" />
                     </valueResource>
                  </extension>
                  <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ParticipantRole">
                     <valueCodeableConcept>
                        <coding>
                           <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanParticipantRole" />
                           <code value="Requester" />
                           <display value="Requester" />
                        </coding>
                     </valueCodeableConcept>
                  </extension>
                  <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ParticipantCareTeam">
                     <valueResource>
                        <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/CareTeam/e9ff45d9-d3f5-4d24-ac45-ef7755829ed3" />
                     </valueResource>
                  </extension>
               </extension>
               <prohibited value="false" />
               <simple>
                  <category value="procedure" />
                  <performer>
                     <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Patient/d4849156-d961-45bb-a16c-e929209c2dc5" />
                  </performer>
               </simple>
            </activity>
         </CarePlan>
      </content>
   </entry>
   <entry>
      <id>https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Organization/24f8aa66-35ae-45af-bbb0-44b411b4114e</id>
      <link rel="self" href="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Organization/24f8aa66-35ae-45af-bbb0-44b411b4114e/_history/2020-04-10T07:55:31:023.6237" />
      <content type="text/xml">
         <Organization xmlns="http://hl7.org/fhir">
            <identifier>
               <system value="http://fhir.nl/fhir/NamingSystem/EMHPCustomerClinicCode" />
               <value value="73732403_933" />
            </identifier>
            <name value="Mentaal Beter Test" />
         </Organization>
      </content>
   </entry>
   <entry>
      <id>https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Patient/d4849156-d961-45bb-a16c-e929209c2dc5</id>
      <link rel="self" href="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Patient/d4849156-d961-45bb-a16c-e929209c2dc5/_history/2020-10-09T12:00:18:024.9293" />
      <content type="text/xml">
         <Patient xmlns="http://hl7.org/fhir">
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Patient#Age">
               <valueInteger value="22" />
            </extension>
            <identifier>
               <use value="official" />
               <system value="http://fhir.nl/fhir/NamingSystem/bsn" />
               <value value="247196101" />
               <period>
                  <start value="2020-10-06T09:04:16+02:00" />
               </period>
            </identifier>
            <name>
               <use value="official" />
               <family value="N. Testrelease" />
               <given value="N." />
               <period>
                  <start value="2020-10-09T08:57:07+02:00" />
               </period>
            </name>
            <telecom>
               <system value="email" />
               <value value="testreleasenina@mailinator.com" />
               <use value="home" />
               <period>
                  <start value="2020-10-09T08:57:07+02:00" />
               </period>
            </telecom>
            <telecom>
               <system value="phone" />
               <value value="0624288089" />
               <use value="mobile" />
               <period>
                  <start value="2020-10-09T08:57:12+02:00" />
               </period>
            </telecom>
            <gender>
               <coding>
                  <system value="http://hl7.org/fhir/v3/AdministrativeGender" />
                  <code value="UN" />
               </coding>
               <text value="Undetermined" />
            </gender>
            <birthDate value="1997-10-20T00:00:00+02:00" />
            <address>
               <use value="home" />
               <period>
                  <start value="2020-10-09T08:57:07+02:00" />
               </period>
            </address>
            <managingOrganization>
               <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Organization/24f8aa66-35ae-45af-bbb0-44b411b4114e" />
               <display value="Mentaal Beter Test" />
            </managingOrganization>
            <active value="true" />
         </Patient>
      </content>
   </entry>
   <entry>
      <id>https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Practitioner/1cd70739-175b-4672-8f22-1542d00ee847</id>
      <link rel="self" href="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Practitioner/1cd70739-175b-4672-8f22-1542d00ee847" />
      <content type="text/xml">
         <Practitioner xmlns="http://hl7.org/fhir">
            <identifier>
               <use value="secondary" />
               <label value="Medicore external caregiver number" />
               <system value="http://fhir.nl/fhir/NamingSystem/ExternCaregiverNumber" />
               <value value="06010002_releasetest" />
            </identifier>
            <name>
               <family value="Releasetest" />
               <given value="Nina" />
            </name>
            <telecom>
               <system value="email" />
               <value value="ninareleasetest@mailinator.com" />
               <use value="work" />
            </telecom>
            <gender>
               <coding>
                  <system value="http://hl7.org/fhir/v3/AdministrativeGender" />
                  <code value="F" />
               </coding>
               <text value="Female" />
            </gender>
         </Practitioner>
      </content>
   </entry>
   <entry>
      <id>https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/CareTeam/e9ff45d9-d3f5-4d24-ac45-ef7755829ed3</id>
      <link rel="self" href="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/CareTeam/e9ff45d9-d3f5-4d24-ac45-ef7755829ed3/_history/2020-10-06T12:19:20:645.9909" />
      <content type="text/xml">
         <Other xmlns="http://hl7.org/fhir">
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CareTeam#Subject">
               <valueResource>
                  <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Patient/d4849156-d961-45bb-a16c-e929209c2dc5" />
               </valueResource>
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CareTeam#Name">
               <valueString value="Engage" />
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CareTeam#Status">
               <valueCoding>
                  <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CareTeamStatus" />
                  <code value="active" />
                  <display value="Active" />
               </valueCoding>
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CareTeam#Period">
               <valuePeriod>
                  <start value="2020-10-06T12:19:12+02:00" />
               </valuePeriod>
            </extension>
            <code>
               <coding>
                  <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/OtherResourceUsage" />
                  <code value="CareTeam" />
                  <display value="CareTeam" />
               </coding>
            </code>
         </Other>
      </content>
   </entry>
</feed>
```

### CreateOrUpdatePatient

Update van een Patiënt.

```markup
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
   <id>5edf704a-175e-4ba6-ae35-e044aebdb653</id>
   <category term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#TestConnector" label="TestConnector" scheme="http://hl7.org/fhir/tag/security" />
   <category term="http://hl7.org/fhir/tag/message" scheme="http://hl7.org/fhir/tag" />
   <entry>
      <id>5ce95052-e8df-45bb-840d-672ecec205b3</id>
      <content type="text/xml">
         <MessageHeader xmlns="http://hl7.org/fhir">
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient">
               <valueResource>
                  <reference value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Patient/3db7ce43-cb49-4c18-bcd9-8adc37ffd657" />
                  <display value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Patient/3db7ce43-cb49-4c18-bcd9-8adc37ffd657" />
               </valueResource>
            </extension>
            <identifier value="5ce95052-e8df-45bb-840d-672ecec205b3" />
            <timestamp value="2020-10-08T09:24:50+02:00" />
            <event>
               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents" />
               <code value="CreateOrUpdatePatient" />
               <display value="CreateOrUpdatePatient" />
            </event>
            <source>
               <endpoint value="" />
            </source>
            <data>
               <reference value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Patient/3db7ce43-cb49-4c18-bcd9-8adc37ffd657/_history/2020-10-08T07:24:51:765.1551" />
            </data>
         </MessageHeader>
      </content>
   </entry>
   <entry>
      <id>http://ggz.koppeltaal.nl/fhir/Koppeltaal/Patient/3db7ce43-cb49-4c18-bcd9-8adc37ffd657</id>
      <link rel="self" href="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Patient/3db7ce43-cb49-4c18-bcd9-8adc37ffd657/_history/2020-10-08T07:24:51:765.1551" />
      <content type="text/xml">
         <Patient xmlns="http://hl7.org/fhir">
            <name>
               <use value="official" />
               <text value="Jan Blaas van der Groen" />
               <family value="Groen" />
               <given value="Jan" />
               <given value="Blaas" />
               <prefix value="van" />
               <prefix value="der" />
               <period>
                  <start value="1980-12-11T00:00:00+01:00" />
                  <end value="2020-10-08T09:24:50.580+02:00" />
               </period>
            </name>
            <name>
               <use value="nickname" />
               <text value="Jantje Groen MD" />
               <family value="Groen" />
               <given value="Jantje" />
               <suffix value="MD" />
               <period>
                  <start value="1980-12-11T00:00:00+01:00" />
                  <end value="2020-10-08T09:24:50.580+02:00" />
               </period>
            </name>
         </Patient>
      </content>
   </entry>
</feed>
```

### CreateOrUpdateActivityDefinition

Een wijziging in de activiteiten definities. 

```markup
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
   <id>urn:uuid:054cc87d-a437-44f6-b884-b06806405593</id>
   <category term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#TestConnector" label="TestConnector" scheme="http://hl7.org/fhir/tag/security" />
   <category term="http://hl7.org/fhir/tag/message" scheme="http://hl7.org/fhir/tag" />
   <entry>
      <content type="text/xml">
         <MessageHeader xmlns="http://hl7.org/fhir" id="6340c63d-1b10-4a39-a7d9-c629b8e86cd8">
            <identifier value="6340c63d-1b10-4a39-a7d9-c629b8e86cd8" />
            <timestamp value="2020-10-09T16:49:55+02:00" />
            <event>
               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents" />
               <code value="CreateOrUpdateActivityDefinition" />
               <display value="CreateOrUpdateActivityDefinition" />
            </event>
            <source>
               <software value="Koppeltaal" />
               <version value="v1.3.x" />
               <endpoint value="not used" />
            </source>
            <data>
               <reference value="https://edgekoppeltaal.vhscloud.nl/FHIR/Koppeltaal/Other/ActivityDefinition:8722/_history/2020-10-09T14:49:54:803.8390" />
            </data>
         </MessageHeader>
      </content>
   </entry>
   <entry>
      <link rel="self" href="https://edgekoppeltaal.vhscloud.nl/FHIR/Koppeltaal/Other/ActivityDefinition:8722/_history/2020-10-09T14:49:54:803.8390" />
      <content type="text/xml">
         <Other xmlns="http://hl7.org/fhir" id="8722">
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#Application">
               <valueResource>
                  <reference value="https://edgekoppeltaal.vhscloud.nl/FHIR/Koppeltaal/Device/8" />
                  <display value="javaadapter" />
               </valueResource>
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#ActivityName">
               <valueString value="name from unit test" />
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#ActivityDefinitionIdentifier">
               <valueString value="8b3861e8-4ebd-48fc-965c-9cb0590a7648" />
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#ActivityDescription">
               <valueString value="description from unit test" />
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#ActivityKind">
               <valueCoding>
                  <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityKind" />
                  <code value="ELearning" />
                  <display value="ELearning" />
               </valueCoding>
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#DefaultPerformer">
               <valueCoding>
                  <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityPerformer" />
                  <code value="Patient" />
                  <display value="Patient" />
               </valueCoding>
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#IsActive">
               <valueBoolean value="true" />
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#IsDomainSpecific">
               <valueBoolean value="true" />
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#LaunchType">
               <valueCode value="Web" />
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#SubActivity">
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#SubActivityName">
                  <valueString value="sad name from test 1" />
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#SubActivityIdentifier">
                  <valueString value="sad identifier from test 1" />
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#SubActivityDescription">
                  <valueString value="sad description from test 1" />
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#SubActivityIsActive">
                  <valueBoolean value="true" />
               </extension>
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#SubActivity">
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#SubActivityName">
                  <valueString value="sad name from test 2" />
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#SubActivityIdentifier">
                  <valueString value="sad identifier from test 2" />
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#SubActivityDescription">
                  <valueString value="sad description from test 2" />
               </extension>
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#SubActivityIsActive">
                  <valueBoolean value="true" />
               </extension>
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityDefinition#IsArchived">
               <valueBoolean value="false" />
            </extension>
            <identifier>
               <use value="official" />
               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Profile/ActivityDefinition#ActivityDefinitionIdentifier" />
               <value value="8b3861e8-4ebd-48fc-965c-9cb0590a7648" />
            </identifier>
            <code>
               <coding>
                  <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/OtherResourceUsage" />
                  <code value="ActivityDefinition" />
                  <display value="ActivityDefinition" />
               </coding>
            </code>
         </Other>
      </content>
   </entry>
</feed>
```

### UpdateCarePlanActivityStatus

Status update doorgeven.

```markup
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
   <id>urn:uuid:eaecb96b-03da-48c7-b455-8ca1dff57dc9</id>
   <category term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#EngageTest" label="EngageTest" scheme="http://hl7.org/fhir/tag/security" />
   <category term="http://hl7.org/fhir/tag/message" scheme="http://hl7.org/fhir/tag" />
   <entry>
      <id>https://testqm1koppeltaal/MessageHeader/2fdfd952-3204-4c66-b98b-dcdc76586531</id>
      <content type="text/xml">
         <MessageHeader xmlns="http://hl7.org/fhir" id="2fdfd952-3204-4c66-b98b-dcdc76586531">
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient">
               <valueResource>
                  <reference value="https://testprovidemb.vitalhealthsoftware.com/Koppeltaal/Patient/d4849156-d961-45bb-a16c-e929209c2dc5" />
               </valueResource>
            </extension>
            <identifier value="2fdfd952-3204-4c66-b98b-dcdc76586531" />
            <timestamp value="2020-10-12T11:36:21+02:00" />
            <event>
               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents" />
               <code value="UpdateCarePlanActivityStatus" />
               <display value="UpdateCarePlanActivityStatus" />
            </event>
            <source>
               <name value="TestTool" />
               <software value="TestTool" />
               <version value="1.3.x" />
               <endpoint value="https://testkoppeltaal.vitalhealthsoftware.com/" />
            </source>
            <data>
               <reference value="https://testqm1koppeltaal/CarePlanActivityStatus/718/_history/2020-10-12T09:35:58:902.5449" />
            </data>
         </MessageHeader>
      </content>
   </entry>
   <entry>
      <id>https://testqm1koppeltaal/CarePlanActivityStatus/718</id>
      <link rel="self" href="https://testqm1koppeltaal/CarePlanActivityStatus/718/_history/2020-10-12T09:35:58:902.5449" />
      <content type="text/xml">
         <Other xmlns="http://hl7.org/fhir">
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus#Activity">
               <valueString value="743e986d-1519-4be5-871f-bd434009d7ee" />
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus#ActivityStatus">
               <valueCoding>
                  <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus" />
                  <code value="Completed" />
                  <display value="Completed" />
               </valueCoding>
            </extension>
            <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus#PercentageCompleted">
               <valueInteger value="0" />
            </extension>
            <code>
               <coding>
                  <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/OtherResourceUsage" />
                  <code value="CarePlanActivityStatus" />
                  <display value="CarePlanActivityStatus" />
               </coding>
            </code>
         </Other>
      </content>
   </entry>
</feed>
```

