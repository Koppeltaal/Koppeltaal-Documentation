---
description: >-
  Koppeltaal is in de loop der tijd doorontwikkeld tot v1.3.x. Met de
  introductie van resource versionering is de implementatie lastig voor de
  IT-deelnemers. Hiervoor hebben we voorbeelden toegevoegd.
---

# Voorbeelden berichtenverkeer

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

