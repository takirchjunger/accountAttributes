# TOEGANG.ORG accountAttributes API

TOEGANG.ORG provides an easy way to controll access to online content based on license models. All the hard stuff such as Single Sign On access from Schools or other organizations, maintaining privacy proof accounts and administration of licenses (including the Dutch ECK standards and connections to distributors and Kennisnet) are handled by TOEGANG.ORG. 

This document describes the REST API for retrieving account attributes


**Prerequisite**
This service is only for publishers that make use of toegang.org for more information about our services please visit [www.toegang.org](https://www.toegang.org)) It will only return only information that is direct related to the authenticated user when this user has a relation to the publisher. Please contact [info@toegang.org](mailto:info@toegang.org) to obtain oAUth credentials for this API based on your pubisherId 

**Test and Production Environments**
TOEGANG.ORG provides seperated test and production environments. Please use our test environment for testing, not the production environment.

| Environment | URL |
|---|---|
| TEST | https://api-test.toegang.org/accounts/attributes/ |
| PROD  | https://api.toegang.org/accounts/attributes/|  

##REST API Usage
1.	User logs on using toegang.org and you receive the tlink code (in the JWT)\
2. Obtain a baerer token based on your client name and client secret (or use the cached version if valid)
3. Call `https://api.toegang.org/accounts/attributes/<tlink>` 

**Method** GET

**HTTP Headers**

 `Content-Type: application/json`  
 `Authorzation: Bearer <baerer token>` 
 
 **Response**
 
| HTTP code | Description |
|---|---|
| 200 | Succesfull; you receive a json structure with the attributes |
| 400 | No tlink given |
| 401 | Unauthorized |
| 403 | No license found, or tlink has no relation to this publisher |
| 409 | No account found for this tlink |  
 
 
**Attributes**
Depending on the privacy regulations and contracts the following attributes might be returned with a succesfull call:

| Attribute | Description |
|---|---|
| knfUid	| Unique Id from Kennisnet |
| knfOrgName | organizationName (schoolname) |
| knfOrgId | BRIN code |
| knfDigiDeliveryId | Organization Identifyer used for ECK specifications |
| knfEduPersonRealId | user identifyer based on portalId for Secundary Education only (will become obsolete soon) | 
| knfEduPersonProfileId | User identifyer based on ECK 1.0 standards used for Vocational Education (will become obsolete soon) | 
| eduPersonAffiliation | User role: student, employee, staff or affiliate |
| eckId | New ECK user identifyer |
| sn | surname |
| knfEduPersonTussenvoegsels | middle name |
| mail | email address |
| ou | Organizational Unit (operational group or class within organization) |
| knfEduPersonUnit | Primary group or class (unique within the organization) |
 
 
##Obtain a bearer token
In order to use the API, a baerer token must be obtained. This token can be used for subsequential calls to all methods of the Toegang.org API, until expiration. We advice you to cache the token in memory for performance reasons. Standard oAuth2 authentication is required using your credentials (see prerequisite). Using these, you can obtain the baerer token at this endpoint:

| Environment | URL |
|---|---|
| TEST | https://idp-test.toegang.org/token |
| PROD  | https://idp.toegang.org/token|  

**Method** POST

**HTTP Headers**

 `Content-Type: application/x-www-form-urlencoded`  
 `Authorzation: Basic <base64clientcredetials>`
 
 The base64clientcredentials string can be constructed by the following steps:
 
 1. Combine client id and client secret with a semicolmn in between.
 2. urlencode this combination
 3. base64encode the urlencoded string

Example:

```
Client id: 7e702c99-6569-43af-a758-935ebdd88082
Client secret: 033927ee-03ae-484f-818f-c1961c75136b
Combined token: 7e702c99-6569-43af-a758-935ebdd88082:033927ee-03ae-484f-818f-c1961c75136b
URL encoded: 7e702c99-6569-43af-a758-935ebdd88082%3A033927ee-03ae-484f-818f-c1961c75136b
Base64 encoded:
N2U3MDJjOTktNjU2OS00M2FmLWE3NTgtOTM1ZWJkZDg4MDgyJTNBMDMzOTI3ZWUtMDNhZS00ODRmLTgxOGYtYzE5NjFjNzUxMzZi

```

 **Body**
You must suply a grand_type parameter and the sole clientId in the body like this:  
`grant_type=client_credentials&client_id=<clientId>`
(substitute the `<clientId>` with your unencoded clientId).


**Response**
 
| HTTP code | Description |
|---|---|
| 200 | Succesfull; you receive a json structure access token and expiration time |
| 401 | Unauthorized |

Example reponse:
 
```
{
"access_token": "YmFkN2Y3ZmItOTUzZC00M2YyLWExNmUtYW",
"expires_in": 3600,
"token_type": "Bearer"
}

```

 

