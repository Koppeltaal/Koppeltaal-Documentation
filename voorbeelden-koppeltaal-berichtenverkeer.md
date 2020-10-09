---
description: >-
  Koppeltaal is in de loop der tijd doorontwikkeld tot v1.3.x. Met de
  introductie van resource versionering is de implementatie lastig voor de
  IT-deelnemers. Hiervoor hebben we voorbeelden toegevoegd.
---

# Voorbeelden Koppeltaal berichtenverkeer

## Aanmken van een CarePlan

Een behandelaar maakt via een portaal, een nieuw behandelplan aan. Hiervoor wordt een FHIR bericht verstuurd naar de Koppeltaal server. Elke nieuwe interactie begint met een MessageHeader met daarin een `extension.valueResource.reference` naar een Patient en een `data.reference` naar de focal resource. De aangeboden focal resource heeft op dat moment geen versie, die moet door de Koppeltaal server uitgegeven worden

```markup
<feed xmlns="http://www.w3.org/2005/Atom">
   <id>urn:uuid:97b7a1e2-ca51-415e-b06c-fc8564a979fa</id>
   <updated>2020-08-13T02:30:41Z</updated>
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

Alle resources die met dit bericht meekomen, hebben een selflink, zonder versie in de `entry.link@href`

```markup
  <entry>
      <id>http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212</id>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/CarePlan/751512212" />
      <content type="text/xml">
         <CarePlan xmlns="http://hl7.org/fhir" id="ref006">
            ...
         </CarePlan>
      </content>
   </entry>
   <entry>
      <id>http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203</id>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/Patient/751512203" />
      <content type="text/xml">
         <Patient xmlns="http://hl7.org/fhir" id="ref009">
            ...
         </Patient>
      </content>
   </entry>
   <entry>
      <id>http://127.0.0.1:37527/app/fhir/Koppeltaal/Practitioner/751512208</id>
      <link rel="self" href="http://127.0.0.1:37527/app/fhir/Koppeltaal/Practitioner/751512208/_history/2020-08-13T02:30:41:965.6822" />
      <content type="text/xml">
         <Practitioner xmlns="http://hl7.org/fhir" id="ref012">
            ...
         </Practitioner>
      </content>
   </entry>
</feed>
```





Once you're strong enough, save the world:

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}



