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


