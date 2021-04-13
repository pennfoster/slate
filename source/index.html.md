---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ


toc_footers:
  - <a href='https://partners.pennfoster.edu'>Penn Foster Partners</a>
  - <a href='https://www.youtube.com/watch?v=cS9qCre_sv8'>Made in Scranton, PA</a>
  - <a href='https://github.com/lord/slate'>Hat tip to Slate</a>

includes:
  - errors

search: true
---

# Introduction
Penn Foster's (PF) integration APIs allow partners and clients to interact with our systems and services through a set of REST endpoints (resources) which provide services like learner enrollment, learner progression, and organization information.

Most current API Version is v3 

## Environments
The APIs are hosted in 3 different environments as listed below:

* Test: [https://tst-api-gateway.pennfoster.edu](https://tst-api-gateway.pennfoster.edu)
* Staging: [https://stg-api-gateway.pennfoster.edu](https://stg-api-gateway.pennfoster.edu)
* Production: [https://api-gateway.pennfoster.edu](https://api-gateway.pennfoster.edu)

Each environment also provides a Swagger page by attaching `swagger/ui/index` to the URL.

Email `itdevapp@pennfoster.edu` to request a Developer Key.

## API Endpoints
* All API endpoints use role based security.
* All API access is over HTTPS.
* All boolean values should be passed as true/false.
* For POST and PUT requests, parameters can be sent using standard [HTML form encoding](https://www.w3.org/TR/html4/interact/forms.html#h-17.13.4).
* Optionally, POST and PUT requests may be sent in [JSON format](http://www.json.org/). The content-type of the request must be set to application/json in this case.


# Authentication

> Example OAuth Request:

```javascript
POST https://environment-url/oauth/token

// Request Headers
Authorization: {auth_key}

// Request Body
grant_type=client_credentials&api_key={api_key}
```

>Response (JSON)

```json

{
  "access_token": "<access_token>",
  "token_type": "bearer",
  "expires_in": "<expiration_secs>"
}
```

Penn Foster uses the [OAuth 2.0](https://tools.ietf.org/html/rfc6749) authentication/authorization mechanism. Before making any requests, PF will provide you with the following parameters for each [environment](#environments).

Parameter | Description | Required
--------- | ----------- | --------
grant_type | client_credentials | Yes
client_id | The client_id for your registered application and environment | Yes
client_secret | The client_secret for your registered application and environment | Yes
api_key | The api_key for your registered application and environment | Yes
auth_key | For convenience the auth_key is a base64 encoded client_id:client_secret | No

Penn Foster expects for the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer secretToken`

<aside class="notice">
You must replace <code>secretToken</code> with the token received from the authentication call.
</aside>

# Organizations

Organizations are in a 3 tier hierarchy:

1. Organization ID *(also referred to as Parent ID)*
2. Location ID
3. Client ID

Each Organization ID can have 1 or many Location IDs.
Each Location ID can have 1 or many Client IDs.


## Get All Organizations

> Example Get All Organizations Request:

```javascript
GET https://environment-url/api/v1/organizations/<organization_id>

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json

{
  "organization_id": 0,
  "type": "string",
  "name": "string",
  "status": "string",
  "address": {
    "address_1": "string",
    "address_2": "string",
    "address_3": "string",
    "address_4": "string",
    "city": "string",
    "state": "string",
    "postal_code": "string",
    "country": "string"
  },
  "locations": [
    {
      "organization_id": 0,
      "location_id": 0,
      "type": "string",
      "name": "string",
      "status": "string",
      "address": {
        "address_1": "string",
        "address_2": "string",
        "address_3": "string",
        "address_4": "string",
        "city": "string",
        "state": "string",
        "postal_code": "string",
        "country": "string"
      },
      "clients": [
        {
          "organization_id": 0,
          "location_id": 0,
          "client_id": 0,
          "type": "string",
          "name": "string",
          "status": "string",
          "address": {
            "address_1": "string",
            "address_2": "string",
            "address_3": "string",
            "address_4": "string",
            "city": "string",
            "state": "string",
            "postal_code": "string",
            "country": "string"
          }
        }
      ]
    }
  ],
  "errors": [
    {
      "error_code": "string",
      "message": "string"
    }
  ],
  "links": [
    {
      "href": "string",
      "rel": "string",
      "method": "string"
    }
  ]
}
```

Get All Organization Information.

### HTTP Request

`GET /organizations/{organization_id}`

## Get Organizations by Location

> Example Get Organizations info by Location Request:

```javascript
GET https://environment-url/api/v1/organizations/{organization_id}/location/{location_id}

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json

{
  "organization_id": 0,
  "type": "string",
  "name": "string",
  "status": "string",
  "address": {
    "address_1": "string",
    "address_2": "string",
    "address_3": "string",
    "address_4": "string",
    "city": "string",
    "state": "string",
    "postal_code": "string",
    "country": "string"
  },
  "locations": [
    {
      "organization_id": 0,
      "location_id": 0,
      "type": "string",
      "name": "string",
      "status": "string",
      "address": {
        "address_1": "string",
        "address_2": "string",
        "address_3": "string",
        "address_4": "string",
        "city": "string",
        "state": "string",
        "postal_code": "string",
        "country": "string"
      },
      "clients": [
        {
          "organization_id": 0,
          "location_id": 0,
          "client_id": 0,
          "type": "string",
          "name": "string",
          "status": "string",
          "address": {
            "address_1": "string",
            "address_2": "string",
            "address_3": "string",
            "address_4": "string",
            "city": "string",
            "state": "string",
            "postal_code": "string",
            "country": "string"
          }
        }
      ]
    }
  ],
  "errors": [
    {
      "error_code": "string",
      "message": "string"
    }
  ],
  "links": [
    {
      "href": "string",
      "rel": "string",
      "method": "string"
    }
  ]
}
```

Get Organizations information by a specific Location ID.

### HTTP Request

`GET /organizations/{organization_id}/location/{location_id}`

## Get Organizations by Client

> Example Get Organizations info by Location and Client Request:

```javascript
GET https://environment-url/api/v1/organizations/{organization_id}/location/{location_id}/client/{client_id}

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json

{
  "organization_id": 0,
  "type": "string",
  "name": "string",
  "status": "string",
  "address": {
    "address_1": "string",
    "address_2": "string",
    "address_3": "string",
    "address_4": "string",
    "city": "string",
    "state": "string",
    "postal_code": "string",
    "country": "string"
  },
  "locations": [
    {
      "organization_id": 0,
      "location_id": 0,
      "type": "string",
      "name": "string",
      "status": "string",
      "address": {
        "address_1": "string",
        "address_2": "string",
        "address_3": "string",
        "address_4": "string",
        "city": "string",
        "state": "string",
        "postal_code": "string",
        "country": "string"
      },
      "clients": [
        {
          "organization_id": 0,
          "location_id": 0,
          "client_id": 0,
          "type": "string",
          "name": "string",
          "status": "string",
          "address": {
            "address_1": "string",
            "address_2": "string",
            "address_3": "string",
            "address_4": "string",
            "city": "string",
            "state": "string",
            "postal_code": "string",
            "country": "string"
          }
        }
      ]
    }
  ],
  "errors": [
    {
      "error_code": "string",
      "message": "string"
    }
  ],
  "links": [
    {
      "href": "string",
      "rel": "string",
      "method": "string"
    }
  ]
}
```

Get Organizations information by a specific Location and Client ID.

### HTTP Request

`GET /organizations/{organization_id}/location/{location_id}/client/{client_id}`

# Leads

## Create a Lead

```javascript
POST https://environment-url/api/v1/leads

// Request Headers
Authorization: Bearer <token>
Content-type: application/json

// Request Body
[
  [
    {
      "required_info": {
        "organization_id": 143738,
        "location_id": 247319,
        "client_id": 333813,
        "program_id": "00787105",
        "first_name": "Herman",
        "last_name": "Munster",
        "date_of_birth": "01/01/1963",
        "phone_number": "5701234567",
        "email_address": "hermanmunster@example.com",
        "contact_email_address": "contact@example.com"
      },
      "optional_info": {
        "gender": "M",
        "alternate_id": "6a535c93-dd15-41d7-8c8d-a097a83857e9",
        "address": {
          "address_1": "1313 Mockingbird Lane",
          "address_2": "",
          "address_3": "",
          "address_4": "",
          "city": "Mockingbird Heights",
          "state": "CA",
          "postal_code": "90210",
          "country": "USA"
        }
      }
    }
  ]
]
```
>Response (JSON)

```json
[
    {
        "lead_id": "123456",
        "lead_status": "X",
        "errors": [],
        "links": []
    }
]
```

Create a new Lead in the Penn Foster system. A lead is used when there is a workflow required before a person can be enrolled at Penn Foster.

### HTTP Request

`POST /leads`

This post expects an array of Lead Objects.  The maximum length of the array is 20 per request.

### Lead Object Required Fields

Parameter | Size | Description
--------- | ---- | -----------
organization_id | 6 | Unique ID for an organization.
location_id | 6 | Unique ID for location under an organization.
client_id | 6 | Unique ID for client under an organization/location.
program_id | 15 | Program to enroll person into. PF will provide this data.
first_name | 40 | Learner first name. Will remove any non-alphabetic characters.
last_name | 40 | Learner last name. Will remove any non-alphabetic characters.
date_of_birth | 8 | Learner Date of birth. Format `mmddyyyy`, non-numeric values will be removed.
phone_number | 20 | Learner phone number. Format `18001234567`, non-numeric values will be removed.
email_address | 40 | Learner email address. Must have an `@` and a `.`.
contact_email_address | 40 | Patrtner Admin email address. Must have an `@` and a `.`.

### Lead Object Optional Fields

Parameter | Size | Description
--------- | ---- | -----------
gender | 1 | M = Male, F = Female, U = Unknown.
alternate_id | 75 | Unique id for learner on 3rd party system.
address_1 | 40 | Street address line 1.
address_2 | 40 | Street address line 2.
address_3 | 40 | Street address line 3.
address_4 | 40 | Street address line 4.
city | 25 | City.
state | 3 | Expecting 2 character state.
postal_code | 12 | Expecting a 5 digit code.
country | 3 | Expecting a 3 digit country code.

### Response Object

The response will be an object or an array of objects depending on the request.

Name | Description
---- | -----------
lead_id | A system generated ID for lead.
lead_status | X = Success. E = Error.
errors | Error with particular Lead object. See [Errors](#penn-foster-system-codes).
links | Not currently populated.


# Learners

At Penn Foster a person participating in 1 or more courses is referred to as a Learner.  Historically, we referred to Learners as Students, therefore, you will see a Learner is given a `Student ID` once enrolled at Penn Foster.

## Create a Learner

> Example Create a new Learner Request:

```javascript
POST https://environment-url/api/v1/learners

// Request Headers
Authorization: Bearer <token>
Content-type: application/json

// Request Body
[
   {
      "required_info":{
         "organization_id":141982,
         "location_id":244648,
         "client_id":329209,
         "first_name":"Joe",
         "last_name":"Smith",
         "email_address":"abc@mycompany.com",
         "program_id":"00736105",
         "ship_to_location":false,
         "user_id":"B2BAPIENR"
      },
      "optional_info":{
         "date_of_birth":"",
         "alternate_id":"83957d62-7436-4260-8f6b-783f64721fdb",
         "phone_number":"123456789",
         "po_number":"",
         "Address":{
            "address_1":"999 18th st",
            "address_2":"",
            "address_3":"",
            "address_4":"",
            "city":"Denver",
            "state":"CO",
            "postal_code":"80202",
            "country":"USA"
         }
      }
   }
]
```
>Response (JSON)

```json
[
    {
        "order_number": "51775",
        "student_id": "56012279",
        "enrollment_status": "X",
        "errors": [],
        "links": []
    }
]
```

Create a new Learner in the Penn Foster system. Typically referred to as an Enrollment.

### HTTP Request

`POST /learners`

This post expects an array of Learner objects.  The maximum length of the array is 20 per request.

### Learner Object Required Fields

Parameter | Size | Description
--------- | ---- | -----------
organization_id | 6 | Unique ID for organization.
location_id | 6 | Unique ID for location under an organization.
client_id | 6 | Unique ID for client under an organization/location.
first_name | 40 | Learner first name. Will remove any non-alphabetic characters.
last_name | 40 | Learner last name. Will remove any non-alphabetic characters.
email_address | 40 | Learner email address. Must have an `@` and a `.`.
program_id | 15 | Program to enroll learner into. PF will provide this data.
ship_to_location | bool | Shipping options. `true` will ship physical contents (if available) to location specified on system. `false` will ship to learner address.
user_id | 15 | User ID for system. PF will provide.

### Learner Object Optional Fields

Parameter | Size | Description
--------- | ---- | -----------
date_of_birth | 8 | Learner Date of birth. Format `mmddyyyy` non-numeric values will be removed.
alternate_id | 75 | Unique id for learner on 3rd party system.
phone_number | 20 | Learner phone number. Format `18001234567`, non-numeric values will be removed.
po_number | 75 | Purchase order number, if applicable.
address_1 | 40 | Street address line 1.
address_2 | 40 | Street address line 2.
address_3 | 40 | Street address line 3.
address_4 | 40 | Street address line 4.
city | 25 | City.
state | 3 | Expecting 2 character state.
postal_code | 12 | Expecting a 5 digit code.
country | 3 | Expecting a 3 digit country code.

### Response Object

The response will be an object or an array of objects depending on the request.

Name | Description
---- | -----------
order_number | A system generated order number for this particular learner object.
student_id | Student ID (Learner ID) generated after successful enrollment.
enrollment_status | X = Success. E = Error.
errors | Error with particular object. See [Errors](#penn-foster-system-codes).
links | Not currently populated.

## Get Learners by Organization

> Example Get Learner Info Request:

```javascript
GET https://environment-url/api/v1/learners?organization_id=141982&rows_per_page=10&page_number=1

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json

{
    "page_number": 1,
    "page_count": 75,
    "record_count": 746,
    "results": {
        "52975707": {
            "organization_id": 141982,
            "location_id": 244648,
            "client_id": 329209,
            "student_id": "52975707",
            "alternate_id": "ThisCouldBeAnyTypeOfData",
            "alternate_location_id": "ThisCouldBeAnyTypeOfData",
            "first_name": "First",
            "last_name": "Last",
            "email_address": "test@test.com",
            "program_id": "TES01105",
            "program_name": "SOFT SKILLS",
            "active_status": "Active", //Active, Inactive, Graduated, Canceled
            "date_enrolled": "07/18/2018",
            "date_last_active": "07/18/2018",
            "date_completed": "07/18/2018",
            "expiration_date": "07/18/2019"
        },
        "52977876": {
            "organization_id": 141982,
            "location_id": 244648,
            "client_id": 329209,
            "student_id": "52977876",
            "alternate_id": "ThisCouldBeAnyTypeOfData",
            "alternate_location_id": "ThisCouldBeAnyTypeOfData",
            "first_name": "Johnny",
            "last_name": "Twosheds",
            "email_address": "test@test.com",
            "program_id": "TES01105",
            "program_name": "SOFT SKILLS",
            "active_status": "Active", //Active, Inactive, Graduated, Canceled
            "date_enrolled": "07/18/2018",
            "date_last_active": "07/18/2018",
            "date_completed": "07/18/2018",
            "expiration_date": "07/18/2019"
        },
        ...
  }
}
```

Get all learners by `Organization ID`.

Will return a dictionary of learner objects.

### HTTP Request

`GET /learners?organization_id={organization_id}`

### URL Parameters


Parameter | Size | Required | Description
--------- | ---- | -------- | -----------
organization_id | 6 | Yes | Unique ID for an organization.
location_id | 6 | No | Unique ID for location under an organization.
alternate_location_id | 6 | No | 3rd party unique ID for location under an organization.
client_id | 6 | No | Unique ID for client under an organization/location.
alternate_client_id | 6 | No | 3rd party unique ID for client under an organization/location.
page_number | 5 | No | If using pagination specify the page number you want returned.
rows_per_page | 5 | No | If using pagination specify the number of records per page.

## Get Learners by Alternate ID

> Example Get Learner by Alternate ID Request:

```javascript
GET https://environment-url/api/v1/learners/6d5f84ed-2fad-4e09-b8bb-e50fac2d00f7

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json

{
    "page_number": 1,
    "page_count": 1,
    "record_count": 2,
    "results": {
        "52975707": {
            "organization_id": 141982,
            "location_id": 244648,
            "client_id": 329209,
            "student_id": "52975707",
            "alternate_id": "6d5f84ed-2fad-4e09-b8bb-e50fac2d00f7",
            "alternate_location_id": "ThisCouldBeAnyTypeOfData",
            "first_name": "First",
            "last_name": "Last",
            "email_address": "test@test.com",
            "program_id": "TES01105",
            "program_name": "SOFT SKILLS",
            "active_status": "Active", //Active, Inactive, Graduated, Canceled
            "date_enrolled": "07/18/2018",
            "date_last_active": "07/18/2018",
            "date_completed": "07/18/2018",
            "expiration_date": "07/18/2019"
        },
        "52977876": {
            "organization_id": 141982,
            "location_id": 244648,
            "client_id": 329209,
            "student_id": "52977876",
            "alternate_id": "6d5f84ed-2fad-4e09-b8bb-e50fac2d00f7",
            "alternate_location_id": "ThisCouldBeAnyTypeOfData",
            "first_name": "Johnny",
            "last_name": "Twosheds",
            "email_address": "test@test.com",
            "program_id": "TES01105",
            "program_name": "SOFT SKILLS",
            "active_status": "Active", //Active, Inactive, Graduated, Canceled
            "date_enrolled": "07/18/2018",
            "date_last_active": "07/18/2018",
            "date_completed": "07/18/2018",
            "expiration_date": "07/18/2019"
        },
  }
}
```

Get learners by `Alternate ID`.

Will return a dictionary of learner objects.

### HTTP Request

`GET /learners?alternate_id={alternate_id}`

### URL Parameters


Parameter | Size | Required | Description
--------- | ---- | -------- | -----------
alternate_id | 75 | Yes | 3rd party unique ID for a learner.
organization_id | 6 | No | Unique ID for an organization.
location_id | 6 | No | Unique ID for location under an organization.
alternate_location_id | 6 | No | 3rd party unique ID for location under an organization.
client_id | 6 | No | Unique ID for client under an organization/location.
alternate_client_id | 6 | No | 3rd party unique ID for client under an organization/location.
page_number | 5 | No | If using pagination specify the page number you want returned.
rows_per_page | 5 | No | If using pagination specify the number of records per page.

## Get Learners by Student ID

> Example Get Learner by Student ID Request:

```javascript
GET https://environment-url/api/v1/learners/52975707

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json

{
  "organization_id": 141982,
  "location_id": 244648,
  "client_id": 329209,
  "student_id": "52975707",
  "alternate_id": "6d5f84ed-2fad-4e09-b8bb-e50fac2d00f7",
  "alternate_location_id": "ThisCouldBeAnyTypeOfData",
  "first_name": "First",
  "last_name": "Last",
  "email_address": "test@test.com",
  "program_id": "TES01105",
  "program_name": "SOFT SKILLS",
  "active_status": "Active", //Active, Inactive, Graduated, Canceled
  "date_enrolled": "07/18/2018",
  "date_last_active": "07/18/2018",
  "date_completed": "07/18/2018",
  "expiration_date": "07/18/2019"
}
```

Get learners by `Student ID`.

Will return one learner object.

### HTTP Request

`GET /learners?student_id={student_id}`

## Cancel Learners

> Example Cancel Learner Request:

```javascript
POST https://environment-url/api/v1/api/v1/learners/cancel

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json
{
  "organization_id": 123456,
  "location_id": 247319,
  "client_id": 333813,
  "student_id": 5123456,
  "alternate_id": "example@example.com",
  "program_id": "00787105"
}
```

Create a request to cancel a learner.  Please note this is only a *request* to cancel a learner. The Penn Foster team will need to execute the request in order for the learner to be officially cancelled in the system.

A learner can be cancelled by `Student ID` or `Alternate ID`.

### HTTP Request

`POST /learners/{student_id}/cancel`

### URL Parameters

An `Alternate ID` or `Student ID` is required.

If an `Alternate ID` is provided, then a `Program ID` is required.

Parameter | Size | Description
--------- | ---- | -----------
student_id | 8 | Unique ID for for Learner at Penn Foster.
alternate_id | 75 | Unique ID for 3rd party.
program_id | 8 | Specific Program ID to cancel for Learner/Alternate ID.
