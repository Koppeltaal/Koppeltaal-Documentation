---
title: Mobile Launch Sequence
category: Technical Designs
order: 3
---

# TD-refresh-tokens

Author: Bart Mehlkop Datum: 03-03-2017 Versie: 0.1

## Version management

| Versie | Datum | Auteur | Aanpassingen |
| :--- | :--- | :--- | :--- |


## Table of content

\[\[TOC\]\]

## Mobile Launch Sequence

The Koppeltaal Mobile Launch sequence has a lot of similarities with the Web Launch sequence described above, but has some subtle differences:

The initial call is made to the MobileLaunch endpoint, and is used to retrieve a Mobile Activation Code. This call must also be made with the credentials of the calling application.

[https://ggz.koppeltaal.nl/OAuth2/Koppeltaal/MobileLaunch?client\_id=RANJKA&patient=https%3A%2F%2Fggzeindhoven.minddistrict.com%2FPatient%2F72308&user=https%3A%2F%2Fggzeindhoven.minddistrict.com%2FRelatedPerson%2F452&resource=RANJKA](https://ggz.koppeltaal.nl/OAuth2/Koppeltaal/MobileLaunch?client_id=RANJKA&patient=https%3A%2F%2Fggzeindhoven.minddistrict.com%2FPatient%2F72308&user=https%3A%2F%2Fggzeindhoven.minddistrict.com%2FRelatedPerson%2F452&resource=RANJKA) For a detailed description of the URL and is parameters, see the description of the Web Launch Sequence above.

The response will be an activation code and the expiry time of the activation code in days:

{"activation\_code":"593740","expires\_in":7} This activation code must be provided to the person that wants to use the mobile game app.

When the Mobile App starts, it will prompt the user for an activation code The Mobile App must have a hard-coded or configurable FHIR Base URL for the Koppeltaal Server, since it cannot be passed in the initial launch call. The app should retrieve the Authorize and Token endpoints from the Koppeltaal Server by retrieving the Conformance from the Koppeltaal Server, as described above. The Mobile app will call the Authorize endpoint with the Mobile Activation Code as Launch Code: [https://ggz.koppeltaal.nl/FHIR/Authorize?](https://ggz.koppeltaal.nl/FHIR/Authorize?) response\_type=code& client\_id=RANJKA& redirect\_uri=http%3A%2F%2Ftest.kickass.ranjgames.com%2Fbuilds%2Frev-1005%2Findex-game.html%2FAfter-Auth& scope=patient%2F\*.read%20launch%3A593740& state=98wrghuwuogerg97 The Koppeltaal server will return an authorization\_code as a JSON response:

{"authorization\_code":"0db34c09-201b-41da-af41-deee89302f4b"} Finally, the Mobile App will retrieve a token from the Koppeltaal Server in exactly the same way as it is done in the Web Launch Sequence. The returned Access Token can subsequently be used to receive message from and submit messages to the Koppeltaal Server. A mobile launch code can only be used once.

## Use of Refresh Tokens

If configured in the Koppeltaal server for a specific ClientId, the Koppeltaal Server will also return a refresh\_token in the reply to the token request:

```markup
{
"access_token": "f3d421f4-d036-468a-b9aa-de9c777ede95",
"token_type": "Bearer",
"expires_in": 900,
"refresh_token": "e54a2533-df44-4e32-bc4d-820c05b2aed0",
"scope": "patient/*.*",
"patient": "https://ggzeindhoven.minddistrict.com/Patient/72308",
"resource": "https://ggzeindhoven.minddistrict.com/RelatedPerson/452"
}
```

The expiry time specified in the attribute expires\_in will usually be 15 minutes or shorter, indicating that the access\_token will expire sooner, and will need to be refreshed after it has expired. The client will be informed about an expired access\_token through the code "expired" in the OperationOutcome:

xml:

```markup
<OperationOutcome xmlns="http://hl7.org/fhir">
<issue>
<type>
<system value="http://hl7.org/fhir/issue-type" />
<code value="expired" />
</type>
<details value="Authentication failed: Bearer token 98510180-8d78-4987-9e27-c958c449f383 has expired at 2016/02/10 22:54:51" />
</issue>
</OperationOutcome>
```

json:

```javascript
{
"resourceType": "OperationOutcome",
"issue": [{
"type": {
"system": "http://hl7.org/fhir/issue-type",
"code": "expired"
},
"details": "Authentication failed: Bearer token 98510180-8d78-4987-9e27-c958c449f383 has expired at 2016/02/10 22:54:51"
}]
}
```

After receiving this reply, the client must get a new access\_token and refresh\_token from the Token-endpoint as retrieved in the Conformance, using the refresh\_token that was previously received:

POST [https://localhost/Petrel244/OAuth2/VHProvisioning/Token](https://localhost/Petrel244/OAuth2/VHProvisioning/Token) Authorization: Basic UU1OYXRpdmVBcHA6V2hvQHJlVTEyMz8= Content-Type: application/x-www-form-urlencoded

grant\_type=refresh\_token&refresh\_token=e54a2533-df44-4e32-bc4d-820c05b2aed0 The Koppeltaal Server will reply with a token response with the same fields as the original token response, containing a new Access\_token as well as a new refresh\_token:

```javascript
{
"access_token": "41aeeebe-14d3-46e9-a994-54e9b5028140",
"token_type": "Bearer",
"expires_in": 900,
"refresh_token": "c9141239-aec5-4e0a-af51-7c307d559184"
}
```

## Possible error codes:

\| Status code \| Issue code \| Description \| 400 \| invalid\_request \| The request is missing a required parameter, includes an unsupported parameter value \(other than grant type\), repeats a parameter, includes multiple credentials, utilizes more than one mechanism for authenticating the client, or is otherwise malformed. \| 400 or 401 \| invalid\_client \| Client authentication failed \(e.g., unknown client, no client authentication included, or unsupported authentication method\). The authorization server MAY return an HTTP 401 \(Unauthorized\) status code to indicatewhich HTTP authentication schemes are supported. If the client attempted to authenticate via the "Authorization" request header field, the authorization server MUST respond with an HTTP 401 \(Unauthorized\) status code and include the "WWW-Authenticate" response header field matching the authentication scheme used by the client. \| 400 or 401 \| invalid\_grant \| The provided authorization grant \(e.g., authorization code, resource owner credentials\) or refresh token is invalid, expired, revoked, does not match the redirection URI used in the authorization request, or was issued to another client. \| 401 \| unauthorized\_client \| The authenticated client is not authorized to use this authorization grant type. \| 401 \| unsupported\_grant\_type \| The authorization grant type is not supported by the authorization server. \| 400 \| invalid\_scope \| The requested scope is invalid, unknown, malformed, or exceeds the scope granted by the resource owner. \| 400 \| unsupported\_token\_type \| The authorization server does not support the revocation of the presented token type. That is, the client tried to revoke an access token on a server not supporting this feature.

