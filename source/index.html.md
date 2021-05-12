---
title: RentPrep V3 SmartMove API Reference

language_tabs: # must be one of https://git.io/vQNgJ
    - JSON

includes:
    - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Rent Prep SmartMove API. You can use this API to submit credit report applications for your customer's on behalf of your company once you've established an API Account with Rent Prep.

The general flow of a credit report application is as follows:

1. Request a credit report for tenants
1. Receive a link to create the credit report
1. Emails are sent to each tenant requesting action be taken as well as the landlord to confirm the order
1. Tenant will accept or reject the application and complete their part of the application
1. Reports will become available

When requesting an order you must supply the unique ID for your user from your system, as well as any optional data about your user, property, applicants, etc which will pre-populate the application creation form.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "x-apiKey: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
```

> Make sure to replace `XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX` with your API key.

Rent Prep uses API keys to allow access to the API. You can register for a new Rent Prep API key by contacting us.

Rent Prep expects for the API key to be included in all API requests to the server in a header that looks like the following:

`x-apiKey: XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX`

<aside class="notice">
You must replace <code>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX</code> with your personal API key.
</aside>

# Endpoints

## Create Application

```json
{
    "Product": "PackageCore",
    "Application": {
        "Applicants": ["applicant1@test.com", "applicant2@test.com"],
        "declineForOpenBankruptcies": false,
        "openBankruptcyWindow": 0,
        "LandlordPays": true
    },
    "Customer": {
        "referenceId": "123"
    },
    "Property": {
        "LandlordCity": "Springfield",
        "LandlordFirstName": "Homer",
        "LandlordLastName": "Simpson",
        "LandlordPhoneNumber": "5555555555",
        "LandlordState": "MA",
        "LandlordStreetAddressLineOne": "123 Fake Street",
        "LandlordZip": "12345",
        "LandlordEmail": "landlordemail@landlord.com",
        "Street": "123 Property Street",
        "City": "Springfield",
        "State": "MA",
        "Zip": "12345",
        "UnitNumber": "4",
        "PropertyName": "742 Evergreen Terrace",
        "Classification": "Conventional",
        "IsFcraAgreementAccepted": true
    },
    "RequestParameters": {
        "postbackUri": "https://yoursite.com",
        "postback_password": "",
        "postback_username": "",
        "referenceId": "",
        "redirectUri": "https://yoursite.com/redirect",
        "cartUrl": "https://yoursite.com/cart"
    }
}
```

> The above command returns JSON structured like this:

```json
{
    "data": {
        "checkout_id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
        "checkout_login": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
    },
    "meta": {
        "message": "SmartMove order created successfully"
    }
}
```

Create an application by posting a valid SmartMoveOrder object to the api `/smartmove/application/create/embedded`

### HTTP Request

`POST /smartmove/application/create/embedded`

### Model Definition

| Parameter          | Description                     | Type                              | Requirements |
| ------------------ | ------------------------------- | --------------------------------- | ------------ |
| Application        | The details of the application  | <a href="#">Application</a>       | Required     |
| Product            | The product being ordered       | <a href="#">Product</a>           | Required     |
| Customer           | The customer creating the order | <a href="#">Customer</a>          | Required     |
| Property           | The property details            | <a href="#">Property</a>          | Required     |
| Request Parameters | Additional Request Parameters   | <a href="#">RequestParameters</a> | Required     |

<aside class="success">
Remember — all API requests need to pass your <a href="#authentication">API Key</a> in the Request Header
</aside>
