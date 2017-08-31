---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

--- 

title: Nextech Select Patient API 

language_tabs: 
   - shell 

toc_footers: 
   - <a href='#'>Sign Up for a Developer Key</a> 
   - <a href='https://github.com/lavkumarv'>Documentation Powered by lav</a> 

includes: 
   - errors 

search: true 

--- 

# Introduction 

The Nextech Select Patient API is a RESTful implementation based on the STU 3 (3.0.1) version of the [FHIR® standard](https://www.hl7.org/fhir/index.html).

Although the FHIR® standard supports both JSON and XML, this API currently only supports JSON.  Therefore any type explicitly defined in the request's `Accept` header will be ignored.  


## Authentication
Nextech's implementation of the FHIR® standard is protected by the OAuth 2 protocol for authenticating requests.  Every API request requires a Bearer token to be passed in the Authorization Header.

```Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng...```

### Request Authorization
To obtain a Bearer token, the user must first request authorization using a registered app's client identifier.

```https://login.microsoftonline.com/mdintellesys.com/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmdintellesys.com%2FPartnerAPI&client_id=[client_id] ```

The user will be asked to log in using their credentials.  Upon first login, they will be asked to authorize the use of the application.  If they don't have credentials, they will need to create an account which will verify their identity. 

Upon successful authentication, an authorization code will be included as the value of the `code` parameter in the redirect URL.  This code, along with the client secret will be included in the request to get an access token.

### Request Access Token
```POST https://login.microsoftonline.com/mdintellesys.com/oauth2/token ```

Add the following parameters as a `x-www-form-urlencoded` query string to the request body:
```
grant_type: authorization_code
client_id: [client_id]
code: [authorization_code]
client_secret: [client_secret]
```

The response includes the `access_token` which should be included in the Authorization header when making an API request.
```
{
  "token_type": "Bearer",
  "scope": "user_impersonation",
  "expires_in": "3599",
  "ext_expires_in": "0",
  "expires_on": "1495481979",
  "not_before": "1495478079",
  "resource": "https://mdintellesys.com/PartnerAPI",
  "access_token": "eyJ0eXAiOiJKV1QiLC..."
  "refresh_token": "AQABAAAAAABnfiG-m..."
  "id_token": "eyJ0eXAiOiJKV1QiLCJh..."
}
  ``` 

**Version:** v1 

# Authentication 

|oauth2|*OAuth 2.0*|
|---|---| 

# /{PATIENTUID}/ALLERGYINTOLERANCE
## ***GET*** 

**Summary:** Get a bundle of allergies for a single patient

**Description:** RESTful searching for allergies by last update date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUID}/AllergyIntolerance` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of allergy last update date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of allergies for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}/BINARY/$AUTOGEN-CCD-IF
## ***GET*** 

**Summary:** Get a CCDA summary document for the specified patient

### HTTP Request 
`***GET*** /{patientUid}/Binary/$autogen-ccd-if` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUid | path | The patient's unique identifier (can be found by patient ID search method) | Yes | string |
| start | query | The start date for which the CCD should be generated (if not specified then all records              starting with the patient's first visit are included) | No | dateTime |
| end | query | The end date for which the CCD should be generated (if not specified then all records              through the patient's latest visit are included) | No | dateTime |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a FHIR Binary object containting the base64-ecoded CCDA summary document              https://www.hl7.org/fhir/binary.html |
| 400 | Invalid patient ID provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}/CAREPLAN
## ***GET*** 

**Summary:** Get a bundle of care plans for a single patient

**Description:** RESTful searching for care plans by visit date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUID}/CarePlan` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of visit date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of care plans for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}/CLINICALIMPRESSION
## ***GET*** 

**Summary:** Get a bundle of clinical impressions for a patient

**Description:** RESTful searching for clinical impressions by visit date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUID}/ClinicalImpression` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of visit date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of clinical impressions for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}/CONDITION
## ***GET*** 

**Summary:** Get a bundle of conditions for a single patient

**Description:** RESTful searching for conditions by onset date and abatement date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUID}/Condition` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| onset-date | query | The collection of condition onset date filters | No | array |
| abatement-date | query | The collection of condition abatement date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of conditions for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}/DEVICE
## ***GET*** 

**Summary:** Get a bundle of devices for a patient

### HTTP Request 
`***GET*** /{patientUID}/Device` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of device effective date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of devices for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}/ENCOUNTER
## ***GET*** 

**Summary:** Get a bundle of encounters for a single patient

**Description:** RESTful searching for conditions by encounter date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUID}/Encounter` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of encounter date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of encounters for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /REFERENCE
## ***GET*** 

### HTTP Request 
`***GET*** /Reference` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |

# /ERROR
## ***GET*** 

### HTTP Request 
`***GET*** /Error` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| errorCode | query |  | Yes | string |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |

# /{PATIENTUID}/GOAL
## ***GET*** 

**Summary:** Get a bundle of goals for a single patient

**Description:** RESTful searching for goals by visit date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUID}/Goal` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of visit date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of goals for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}/IMMUNIZATION
## ***GET*** 

**Summary:** Get a bundle of immunizations for a single patient

**Description:** RESTful searching for current immunizations by administration date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUID}/Immunization` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of current immunization administration date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of immunizations for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}/MEDICATIONDISPENSE
## ***GET*** 

**Summary:** Get a bundle of medication dispensements for a single patient

**Description:** RESTful searching for medication dispensements by preparation date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUID}/MedicationDispense` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| whenprepared | query | The collection of preparation date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of medications for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}/MEDICATIONSTATEMENT
## ***GET*** 

**Summary:** Get a bundle of medication statements for a single patient

**Description:** RESTful searching for medication statements by effective date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUID}/MedicationStatement` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| effective | query | The collection of effective date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of medications for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}/OBSERVATION
## ***GET*** 

**Summary:** Get a bundle of diagnostic observations for a single patient

**Description:** This request requires a category code to search on. The following category codes are supported:
- laboratory
- social-history
- vital-signs

RESTful searching for observations by date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUid}/Observation` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUid | path | The unique identifier acquired from the patient search | Yes | string |
| category | query | The category of observation to load | Yes | string |
| date | query | The collection of observation obtained date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of diagnostic observations for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /{PATIENTUID}
## ***GET*** 

**Summary:** Get the demographic information for a patient

### HTTP Request 
`***GET*** /{patientUID}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns patient information |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

# /ID
## ***GET*** 

**Summary:** Attempts to find a single patient that matches the given search criteria and if
successful returns that patient's unique identifier.

At least one of query parameters is required to perform a search.

### HTTP Request 
`***GET*** /ID` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| family | query | The family (last) name of the patient | No | string |
| given | query | The given (first) name of the patient | No | string |
| birthdate | query | The patient's date of birth formatted as YYYY-MM-DD | No | dateTime |
| phone | query | The patient's phone number which will be matched against any phone number (home, cell, etc.) | No | string |
| email | query | The patient's email address | No | string |
| address-city | query | The city of the patient's address | No | string |
| address-state | query | The state of the patient's address | No | string |
| address-postalcode | query | The postal (zip) code of the patient's address | No | string |
| identifier | query | The patient's Nextech chart number | No | string |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns the patient's unique identifier |
| 400 | No search parameters were specified or the search is not specific enough |
| 404 | No patients met the search criteria |
| 500 | Internal server error |

# /
## ***GET*** 

**Summary:** Searches for all patients matching the given search criteria. At least one search parameter is required.

Note: The search currently has a limit of 500 patients.

### HTTP Request 
`***GET*** /` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| family | query | The family (last) name of the patient | No | string |
| given | query | The given (first) name of the patient | No | string |
| birthdate | query | The patient's date of birth formatted as YYYY-MM-DD | No | dateTime |
| phone | query | The patient's phone number which will be matched against any phone number (home, cell, etc.) | No | string |
| email | query | The patient's email address | No | string |
| address-city | query | The city of the patient's address | No | string |
| address-state | query | The state of the patient's address | No | string |
| address-postalcode | query | The postal (zip) code of the patient's address | No | string |
| identifier | query | The patient's Nextech chart number | No | string |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns patient objects for the matching patients |
| 400 | No search parameters were specified |
| 404 | No patients met the search criteria |
| 500 | Internal server error |

# /{PATIENTUID}/PROCEDURE
## ***GET*** 

**Summary:** Get a bundle of procedures for a single patient

**Description:** RESTful searching for procedures by performed date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne.

### HTTP Request 
`***GET*** /{patientUID}/Procedure` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of procedure performed date filters | No | array |
| nx-practice-id | header | The unique identifier for a practice | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns a bundle of diagnostic observations for a patient |
| 400 | No supported search parameters provided |
| 404 | Specified patient does not exist |
| 500 | Internal server error |

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
