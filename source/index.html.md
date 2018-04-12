---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ


toc_footers:
  - <a href='https://partners.pennfoster.edu'>Penn Foster Partners</a>
  - <a href='https://www.youtube.com/watch?v=qHrN5Mf5sgo'>Made in Scranton, PA</a>
  - <a href='https://github.com/lord/slate'>Hat tip to Slate</a>

includes:
  - errors

search: true
---

# Introduction
Penn Foster's (PF) integration APIs allow partners and clients to interact with our systems and services through a set of REST endpoints (resources) which provide services like student enrollment, student progression, and account information.

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

# Accounts

At Penn Foster all API calls will require your Account ID.  This ID will be supplied by the Penn Foster team.
Accounts are in a 3 tier hierarchy:

1. Account ID *(also referred to as Parent ID)*
2. Location ID
3. Client ID

Each Account ID can have 1 or many Location IDs.
Each Location ID can have 1 or many Client IDs.


## Get All Accounts

> Example Get All Accounts Request:

```javascript
GET https://environment-url/api/v1/accounts/<account_id>

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json

{
  "parent_id": 0,
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
      "parent_id": 0,
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
          "parent_id": 0,
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

Get All Account Information.

### HTTP Request

`GET /accounts/{account_id}`

## Get Accounts by Location

> Example Get Accounts info by Location Request:

```javascript
GET https://environment-url/api/v1/accounts/{account_id}/location/{location_id}

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json

{
  "parent_id": 0,
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
      "parent_id": 0,
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
          "parent_id": 0,
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

Get Accounts information by a specific Location ID.

### HTTP Request

`GET /accounts/{account_id}/location/{location_id}`

## Get Accounts by Client

> Example Get Accounts info by Location and Client Request:

```javascript
GET https://environment-url/api/v1/accounts/{account_id}/location/{location_id}/client/{client_id}

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json

{
  "parent_id": 0,
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
      "parent_id": 0,
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
          "parent_id": 0,
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

Get Accounts information by a specific Location and Client ID.

### HTTP Request

`GET /accounts/{account_id}/location/{location_id}/client/{client_id}`

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
        "parent_id": 143738,
        "location_id": 247319,
        "client_id": 333813,
        "program_id": "00787105",
        "first_name": "Herman",
        "last_name": "Munster",
        "date_of_birth": "01/01/1963",
        "phone_number": "",
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
parent_id | 6 | Unique ID for account.  This is the Account_id.
location_id | 6 | Unique ID for location under parent.
client_id | 6 | Unique ID for client under parent/location.
program_id | 15 | Program to enroll person into. PF will provide this data.
first_name | 40 | Student first name. Will remove any non-alphabetic characters.
last_name | 40 | Student last name. Will remove any non-alphabetic characters.
date_of_birth | 8 | Student Date of birth. Format `mmddyyyy`, non-numeric values will be removed.
phone_number | 20 | Student phone number. Format `18001234567`, non-numeric values will be removed.
email_address | 40 | Student email address. Must have an `@` and a `.`.
contact_email_address | 40 | Patrtner Admin email address. Must have an `@` and a `.`.

### Lead Object Optional Fields

Parameter | Size | Description
--------- | ---- | -----------
gender | 1 | M = Male, F = Female, U = Unknown.
alternate_id | 75 | Unique id for student on 3rd party system.
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


# Students

At Penn Foster a person participating in 1 or more courses is referred to as a Student.

## Get Student Information

> Example Get Student Info Request:

```javascript
GET https://environment-url/api/v1/accounts/api/v1/students/{account_id}/{student_id}

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json
{
  "resource_id": 2,
  "student_id": "50034621",
  "first_name": "FName",
  "last_name": "LName",
  "email_address": "exampl@example.com",
  "active_status": "Graduated",
  "date_enrolled": "2012-04-20T00:00:00",
  "program_id": "00711105",
  "program_name": "HIGH SCHOOL DIPLOMA"
}
```

Get a specific Student's information.

### HTTP Request

`GET /students/{account_id}/{student_id}`

## Create a Student

> Example Create a new Student Request:

```javascript
POST https://environment-url/api/v1/students

// Request Headers
Authorization: Bearer <token>
Content-type: application/json

// Request Body
[
   {
      "required_info":{
         "parent_id":141982,
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

Create a new Student in the Penn Foster system. Typically referred to as an Enrollment.

### HTTP Request

`POST /students`

This post expects an array of Student objects.  The maximum length of the array is 20 per request.

### Student Object Required Fields

Parameter | Size | Description
--------- | ---- | -----------
parent_id | 6 | Unique ID for account.  This is the Account_id.
location_id | 6 | Unique ID for location under parent.
client_id | 6 | Unique ID for client under parent/location.
first_name | 40 | Student first name. Will remove any non-alphabetic characters.
last_name | 40 | Student last name. Will remove any non-alphabetic characters.
email_address | 40 | Student email address. Must have an `@` and a `.`.
program_id | 15 | Program to enroll student into. PF will provide this data.
ship_to_location | bool | Shipping options. `true` will ship physical contents (if available) to location specified on Account. `false` will ship to student address.
user_id | 15 | User ID for system. PF will provide.

### Student Object Optional Fields

Parameter | Size | Description
--------- | ---- | -----------
date_of_birth | 8 | Student Date of birth. Format `mmddyyyy` non-numeric values will be removed.
alternate_id | 75 | Unique id for student on 3rd party system.
phone_number | 20 | Student phone number. Format `18001234567`, non-numeric values will be removed.
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
order_number | A system generated order number for this particular student object.
student_id | Student ID generated after successful enrollment.
enrollment_status | X = Success. E = Error.
errors | Error with particular object. See [Errors](#penn-foster-system-codes).
links | Not currently populated.

## Cancel Student

> Example Cancel Student Request:

```javascript
GET https://environment-url/api/v1/accounts/api/v1/students/{account_id}/{student_id}/cancel

// Request Headers
Authorization: Bearer <token>
Content-type: application/json
```
>Response (JSON)

```json
{
  "message": "Accepted"
}
```

Create a request to cancel a student.  Please note this is only a *request* to cancel a student. The Penn Foster team will need to execute the request in order for the Student to be officially cancelled in the system.

### HTTP Request

`GET /students/{account_id}/{student_id}/cancel`

<aside class="notice">
<code>alternate_id</code> can be substituted for <code>student_id</code> in this call.
</aside>
