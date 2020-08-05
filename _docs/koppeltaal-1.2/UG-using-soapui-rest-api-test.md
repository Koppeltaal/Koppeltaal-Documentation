---
title: User Guide - REST API TEST
category: User Guides
order: 2
---

# Connecting to the Koppeltaal test server using SOAP UI

## Create a SOAP UI project \(SOAP UI version 5.0\)

Download the open available tool to simulate REST api calls =&gt; SOAPUI \(version 5.0 at this moment\)

* [http://soapui.org](http://soapui.org)

The last version of the Koppeltaal SOAP UI project :

* [https://github.com/Koppeltaal/Koppeltaal-Server/tree/master/tests/SoapUI](https://github.com/Koppeltaal/Koppeltaal-Server/tree/master/tests/SoapUI) 

## Define a request to get and claim the next message available in the queue

![image alt text](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/SOAP_UI_CONFIG1.png)

## Test

Once the claim is done a COMMIT action needs to be sent to the Koppeltaal server. The two phases COMMIT takes into acount the resilience of the system at any time \(no loss of messages but duplicates possible\). At the END of the process flow the COMMIT should send: Failed or Success status.

Message CLAIMED - with id 39

```markup
 <feed xmlns="http://www.w3.org/2005/Atom">
  .....
 </feed>
```

This can be done through a PUT to the RESOURCE: MessageHeader/{MessageHeaderID}. \(SOAP NEW RESOURCE!\)

In de request parameters a value for the MessageHeaderID is required. This one could be taken from the original GetNextNewAndClaim that has been executed before \(The ID from the MessageHeader ID\). That should be something like: '[http://testkoppeltaal.vhscloud.nl/FHIR/Koppeltaal/MessageHeader/39](http://testkoppeltaal.vhscloud.nl/FHIR/Koppeltaal/MessageHeader/39)'. At this example '39' the MessageHeaderID.

As content of the request we can simply add the whole MessageHeader node as a copy. In this tag only the status must change from Claimed to Success or Failed.

![image alt text](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/SOAP_UI_CONFIG1.png)

Content to be send back - changing the sate to 'SUCCESS'

Example: GetNextAndClaim with messages in the queue:

```markup
<?xml version="1.0" encoding="utf-8"?> <feed xmlns="http://www.w3.org/2005/Atom">

 <id>urn:uuid:d3b90820-73f4-4b44-a27b-d99c1eb2ec77</id>
 <category term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#MindDistrict Kickass" label="MindDistrict Kickass" scheme="http://hl7.org/fhir/tag/security" />
 <category term="http://hl7.org/fhir/tag/message" scheme="http://hl7.org/fhir/tag" />
 <entry>
   <title type="text">MessageHeader with IID=98</title>
   <id>https://testconnectors.vhscloud.nl/FHIR/Koppeltaal/MessageHeader/98</id>
   <updated>2015-06-18T12:23:32+02:00</updated>
   <link rel="self" href="https://testconnectors.vhscloud.nl/FHIR/Koppeltaal/MessageHeader/98/_history/2015-06-18T12:23:32:271.360" />
   <content type="text/xml">
     <MessageHeader xmlns="http://hl7.org/fhir">
       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient">
         <valueResource>
           <reference value="http://test.mijnapplicatie.nl/fhir/Patient/74" />
         </valueResource>
       </extension>
       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#ProcessingStatus">
         <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#ProcessingStatusStatus">
           <valueCode value="Claimed" />
         </extension>
         <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#ProcessingStatusStatusLastChanged">
           <valueInstant value="2015-06-18T14:23:32+02:00" />
         </extension>
       </extension>
       <identifier value="d3b90820-73f4-4b44-a27b-d99c1eb2ec77" />
       <timestamp value="2015-06-18T12:23:28+00:00" />
       <event>
         <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents" />
         <code value="CreateOrUpdateUserMessage" />
         <display value="CreateOrUpdateUserMessage" />
       </event>
       <source>
         <software value="KoppeltaalRegressionTests" />
         <endpoint value="None" />
       </source>

         <reference value="http://test.mijnapplicatie.nl/fhir/UserMessage/3605/_history/2015-06-18T12:23:29:771.6980" />

     </MessageHeader>
   </content>
 </entry>
 <entry>
   <id>http://test.mijnapplicatie.nl/fhir/UserMessage/3605/_history/2015-06-18T12:23:29:771.6980</id>
   <link rel="self" href="http://test.mijnapplicatie.nl/fhir/UserMessage/3605" />
   <content type="text/xml">
     <Other id="3605" xmlns="http://hl7.org/fhir">
       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/UserMessage#Content">
         <valueString value="This is a message in a bottle" />
       </extension>
       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/UserMessage#SubjectString">
         <valueString value="Dit is een bericht" />
       </extension>
       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/UserMessage#From">
         <valueResource>
           <reference value="http://test.mijnapplicatie.nl/fhir/Patient/3644" />
         </valueResource>
       </extension>
       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/UserMessage#To">
         <valueResource>
           <reference value="http://test.mijnapplicatie.nl/fhir/Practitioner/" />
         </valueResource>
       </extension>

         <coding>
           <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/OtherResourceUsage" />
           <code value="UserMessage" />
           <display value="UserMessage" />
         </coding>

     </Other>
   </content>
 </entry>
</feed>
```

## Id management

```markup
 <feed> Envelope id must be unique ID  for each new request
  e.g. <id>urn:uuid:5147c410-533f-4e4d-bf38-886ff386cec3</id>
 <Entry> Message id must be unique ID  for each new request
        <id>....</id>
       ....
       <MessageHeader>
          ....
          <identifier>...</identifier>
   e.g. <identifier>urn:uuid:8fcced7a-0dea-4a32-9ed5-080ded9abaac</identifier>
```

## Define a request to create a new CarePlan

![image alt text](https://github.com/Koppeltaal/documentation/tree/083ac6eba8108c4b610d5248bb3e68b1bf268684/_docs/koppeltaal-1.2/SimpleCarePlan.png)

Follow the TD to identify the required attributes to be included in the call. The next message identifies a NEW CLEAN CarePlan A new CarePlan has no history \(in the  TAG there is no Version provided but the CarePlan ID must be UNIQUE identifiable \(Message ID's and Date are specific unique generated\)

```markup
<?xml version="1.0" ?>
<feed xmlns="http://www.w3.org/2005/Atom">

   <id>urn:uuid:63843702-d78a-41ae-b58a-505b398d5169</id>
   <category label="MindDistrict Kickass"
       scheme="http://hl7.org/fhir/tag/security" term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#MindDistrict Kickass"/>
   <category scheme="http://hl7.org/fhir/tag" term="http://hl7.org/fhir/tag/message"/>
   <entry>
       <id>urn:uuid:63843702-d78a-41ae-b58a-505b398d5169</id>
       <content type="text/xml">
           <MessageHeader xmlns="http://hl7.org/fhir">
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient">
                   <valueResource>
                       <reference value="http://local.emhp/Patient/2697"/>
                   </valueResource>
               </extension>
               <identifier value="63843702-d78a-41ae-b58a-505b398d5169"/>
               <timestamp value="2015-06-18T09:02:39.751Z"/>
               <event>
                   <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents"/>
                   <code value="CreateOrUpdateCarePlan"/>
                   <display value="CreateOrUpdateCarePlan"/>
               </event>

                   <reference value="http://local.emhp/CarePlan/7553"/>

               <source>
                   <software value="KoppeltaalRegressionTests"/>
                   <endpoint value="None"/>
               </source>
           </MessageHeader>
       </content>
   </entry>
   <entry>
       <link href="http://local.emhp/CarePlan/7553" rel="self"/>
       <content type="text/xml">
           <CarePlan id="7553" xmlns="http://hl7.org/fhir">
               <patient>
                   <reference value="http://local.emhp/Patient/2697"/>
               </patient>
               <status value="active"/>
               <participant>
                   <role>
                       <coding>
                           <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanParticipantRole"/>
                           <code value="Requester"/>
                           <display value="Requester"/>
                       </coding>
                   </role>
                   <member>
                       <reference value="http://local.emhp/Practitioner/4941"/>
                   </member>
               </participant>
               <goal id="3797">
                   <description value="To reduce the amount of time I spend on my cellphone."/>
                   <status value="in progress"/>
                   <notes value="Patient does not want to use smart phones."/>
               </goal>
               <activity id="7704">
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityIdentifier">
                       <valueString value="http://local.emhp/CarePlan/7553#7704"/>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityDefinition">
                       <valueString value="JWG"/>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityKind">
                       <valueCoding>
                           <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityKind"/>
                           <code value="Game"/>
                           <display value="Game"/>
                       </valueCoding>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityDescription">
                       <valueString value="Learn how to deal with Autism."/>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivity">
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivityIdentifier">
                           <valueString value="mission 1"/>
                       </extension>
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivityStatus">
                           <valueCoding>
                               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus"/>
                               <code value="InProgress"/>
                               <display value="InProgress"/>
                           </valueCoding>
                       </extension>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivity">
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivityIdentifier">
                           <valueString value="mission3"/>
                       </extension>
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivityStatus">
                           <valueCoding>
                               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus"/>
                               <code value="Available"/>
                               <display value="Available"/>
                           </valueCoding>
                       </extension>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#Participant">
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ParticipantMember">
                           <valueResource>
                               <reference value="http://local.emhp/Practitioner/4941"/>
                           </valueResource>
                       </extension>
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ParticipantRole">
                           <valueCodeableConcept>
                               <coding>
                                   <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanParticipantRole"/>
                                   <code value="Caregiver"/>
                                   <display value="Caregiver"/>
                               </coding>
                           </valueCodeableConcept>
                       </extension>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#StartDate">
                       <valueDateTime value="2015-06-02T14:13:57+02:00"/>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityStatus">
                       <valueCoding>
                           <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus"/>
                           <code value="Available"/>
                           <display value="Available"/>
                       </valueCoding>
                   </extension>
                   <goal value="3797"/>
                   <prohibited value="false"/>
                   <notes value="Seems to be very difficult for this participant."/>
                   <simple>
                       <category value="procedure"/>
                       <performer>
                           <reference value="http://local.emhp/Patient/2697"/>
                       </performer>
                   </simple>
               </activity>
           </CarePlan>
       </content>
   </entry>
   <entry>
       <link href="http://local.emhp/Patient/2697" rel="self"/>
       <content type="text/xml">
           <Patient id="2697" xmlns="http://hl7.org/fhir">
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Patient#Age">
                   <valueInteger value="43"/>
               </extension>
               <name>
                   <use value="official"/>
                   <family value="Todea"/>
                   <given value="Reli"/>
               </name>
               <gender>
                   <coding>
                       <system value="http://hl7.org/fhir/vs/administrative-gender"/>
                       <code value="M"/>
                       <display value="Male"/>
                   </coding>
               </gender>
               <birthDate value="1972-02-28T00:00:00+01:00"/>
           </Patient>
       </content>
   </entry>
</feed>
```

## Create a Care Plan With Activity

This XML message will be used to add an activity to a careplan:

```markup
   <id>urn:uuid:63843702-d78a-41ae-b58a-505b398d5169</id>
   <category label="MindDistrict Kickass"
       scheme="http://hl7.org/fhir/tag/security" term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#MindDistrict Kickass"/>
   <category scheme="http://hl7.org/fhir/tag" term="http://hl7.org/fhir/tag/message"/>
   <entry>
       <id>urn:uuid:63843702-d78a-41ae-b58a-505b398d5169</id>
       <content type="text/xml">
           <MessageHeader xmlns="http://hl7.org/fhir">
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient">
                   <valueResource>
                       <reference value="http://local.emhp/Patient/2697"/>
                   </valueResource>
               </extension>
               <identifier value="63843702-d78a-41ae-b58a-505b398d5169"/>
               <timestamp value="2015-06-18T09:02:39.751Z"/>
               <event>
                   <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents"/>
                   <code value="CreateOrUpdateCarePlan"/>
                   <display value="CreateOrUpdateCarePlan"/>
               </event>

                   <reference value="http://local.emhp/CarePlan/7553"/>

               <source>
                   <software value="KoppeltaalRegressionTests"/>
                   <endpoint value="None"/>
               </source>
           </MessageHeader>
       </content>
   </entry>
   <entry>
       <link href="http://local.emhp/CarePlan/7553" rel="self"/>
       <content type="text/xml">
           <CarePlan id="7553" xmlns="http://hl7.org/fhir">
               <patient>
                   <reference value="http://local.emhp/Patient/2697"/>
               </patient>
               <status value="active"/>
               <participant>
                   <role>
                       <coding>
                           <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanParticipantRole"/>
                           <code value="Requester"/>
                           <display value="Requester"/>
                       </coding>
                   </role>
                   <member>
                       <reference value="http://local.emhp/Practitioner/4941"/>
                   </member>
               </participant>
               <goal id="3797">
                   <description value="To reduce the amount of time I spend on my cellphone."/>
                   <status value="in progress"/>
                   <notes value="Patient does not want to use smart phones."/>
               </goal>
               <activity id="7704">
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityIdentifier">
                       <valueString value="http://local.emhp/CarePlan/7553#7704"/>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityDefinition">
                       <valueString value="JWG"/>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityKind">
                       <valueCoding>
                           <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/ActivityKind"/>
                           <code value="Game"/>
                           <display value="Game"/>
                       </valueCoding>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityDescription">
                       <valueString value="Learn how to deal with Autism."/>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivity">
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivityIdentifier">
                           <valueString value="mission 1"/>
                       </extension>
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivityStatus">
                           <valueCoding>
                               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus"/>
                               <code value="InProgress"/>
                               <display value="InProgress"/>
                           </valueCoding>
                       </extension>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivity">
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivityIdentifier">
                           <valueString value="mission3"/>
                       </extension>
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#SubActivityStatus">
                           <valueCoding>
                               <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus"/>
                               <code value="Available"/>
                               <display value="Available"/>
                           </valueCoding>
                       </extension>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#Participant">
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ParticipantMember">
                           <valueResource>
                               <reference value="http://local.emhp/Practitioner/4941"/>
                           </valueResource>
                       </extension>
                       <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ParticipantRole">
                           <valueCodeableConcept>
                               <coding>
                                   <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanParticipantRole"/>
                                   <code value="Caregiver"/>
                                   <display value="Caregiver"/>
                               </coding>
                           </valueCodeableConcept>
                       </extension>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#StartDate">
                       <valueDateTime value="2015-06-02T14:13:57+02:00"/>
                   </extension>
                   <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlan#ActivityStatus">
                       <valueCoding>
                           <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/CarePlanActivityStatus"/>
                           <code value="Available"/>
                           <display value="Available"/>
                       </valueCoding>
                   </extension>
                   <goal value="3797"/>
                   <prohibited value="false"/>
                   <notes value="Seems to be very difficult for this participant."/>
                   <simple>
                       <category value="procedure"/>
                       <performer>
                           <reference value="http://local.emhp/Patient/2697"/>
                       </performer>
                   </simple>
               </activity>
           </CarePlan>
       </content>
   </entry>
   <entry>
       <link href="http://local.emhp/Patient/2697" rel="self"/>
       <content type="text/xml">
           <Patient id="2697" xmlns="http://hl7.org/fhir">
               <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Patient#Age">
                   <valueInteger value="43"/>
               </extension>
               <name>
                   <use value="official"/>
                   <family value="Todea"/>
                   <given value="Reli"/>
               </name>
               <gender>
                   <coding>
                       <system value="http://hl7.org/fhir/vs/administrative-gender"/>
                       <code value="M"/>
                       <display value="Male"/>
                   </coding>
               </gender>
               <birthDate value="1972-02-28T00:00:00+01:00"/>
           </Patient>
       </content>
   </entry>
```

## Response Contains the UNIQIE VERSION ID

```markup
  <id>urn:uuid:07fb24ab-f598-488e-a637-ebbe12636012</id>
  <category term="http://ggz.koppeltaal.nl/fhir/Koppeltaal/Domain#MindDistrict Kickass" label="MindDistrict Kickass" scheme="http://hl7.org/fhir/tag/security"/>
  <category term="http://hl7.org/fhir/tag/message" scheme="http://hl7.org/fhir/tag"/>
  <entry>
     <id>urn:uuid:a2277945-9042-4747-a2d4-754c04317a8b</id>
     <content type="text/xml">
        <MessageHeader xmlns="http://hl7.org/fhir">
           <identifier value="urn:uuid:a2277945-9042-4747-a2d4-754c04317a8b"/>
           <timestamp value="2015-06-18T13:56:11+02:00"/>
           <event>
              <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents"/>
              <code value="CreateOrUpdateCarePlan"/>
              <display value="CreateOrUpdateCarePlan"/>
           </event>
           <response>
              <identifier value="9b616571-544c-4d78-ad4c-33cf78f28138"/>
              <code value="ok"/>
           </response>
           <source>
              <name value=""/>
              <software value=""/>
              <version value=""/>
              <endpoint value="https://testconnectors.vhscloud.nl/FHIR/Koppeltaal/Mailbox"/>
           </source>

              <reference value="http://local.emhp/CarePlan/4289/_history/2015-06-18T11:56:11:338.7674"/>

        </MessageHeader>
     </content>
  </entry>
```

## CarePlan Activity

The new CarePlan Activity will need to have the Version updated -CreateOrUpdateCarePlanActivityResult

The Response contains the CarePlan Version ID that must be provided for further updates referencing the same CarePlan 

```markup
<MessageHeader xmlns="http://www.w3.org/2005/Atom">

           <extension xmlns="http://hl7.org/fhir"
             url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#Patient">
              <valueResource>
                 <reference value="http://antes.emhp.nl/Patient/1157"/>
              </valueResource>
           </extension>
           <extension xmlns="http://hl7.org/fhir"
             url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#ProcessingStatus">
              <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#ProcessingStatusStatus">
                 <valueCode value="Success"/>
              </extension>
              <extension url="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageHeader#ProcessingStatusStatusLastChanged">
                 <valueInstant value="2015-06-18T14:08:48+02:00"/>
              </extension>
           </extension>
           <identifier xmlns="http://hl7.org/fhir" value="e279c094-4fe8-4857-a544-0817a18ebbda"/>
           <timestamp xmlns="http://hl7.org/fhir" value="2015-06-18T12:08:47+00:00"/>
           <event xmlns="http://hl7.org/fhir">
              <system value="http://ggz.koppeltaal.nl/fhir/Koppeltaal/MessageEvents"/>
              <code value="UpdateCarePlanActivityStatus"/>
              <display value="UpdateCarePlanActivityStatus"/>
           </event>
           <source xmlns="http://hl7.org/fhir">
              <software value="KoppeltaalRegressionTests"/>
              <endpoint value="None"/>
           </source>

              <reference value="http://local.emhp/CarePlanActivityStatus/426/_history/2015-06-18T12:08:47:450.4455"/>

        </MessageHeader>
```

## Response

The Answer for the CreateOrUpdateCarePlanActivityResult status contains the 200 code 200 OK Server: Microsoft-IIS/8.0 Set-Cookie: ASP.NET\_SessionId=c1hnzdl5gfuzwxquuj2eoxrn; path=/; HttpOnly

