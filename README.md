# Nahaus API V1.0.0 Beta

[EN]

Welcome to the Nahaus.de API documentation! This repository contains comprehensive guides and documentation to help you
start working with Nahaus.de's API as quickly as possible, and support you in effectively integrating your software.

Please Note: To access and use the Nahaus.de API, you must possess an ENTERPRISE ACCOUNT with Nahaus.de.

Before you can use the API, you'll first need to obtain an ID token. There are two authentication options available:

1. If you have a username and password, use Authentication Option 1.
2. Otherwise, use Authentication Option 2, which requires a customerID and an API key. These can be provided by us upon
   request.

For more information on how to get set up with these authentication methods, please contact us at **support@nahaus.de**

[DE]

Die nahaus API ermöglicht es Entwicklern, auf die Funktionalitäten unserer Immobilienmanagement-Software zuzugreifen und
diese in ihre eigenen Anwendungen zu integrieren. Sie können die API verwenden, um Vermietungsdaten zu manipulieren,
Stammdaten zu verwalten, Vermietungen anlegen, Zähler zu tracken, und vieles mehr.

Die nahaus API ermöglicht es Entwicklern, auf die Funktionalitäten unserer Immobilienmanagement-Software zuzugreifen und
diese in ihre eigenen Anwendungen zu integrieren. Sie können die API verwenden, um Vermietungsdaten zu manipulieren,
Verträge zu verwalten, Zahlungen zu tracken, und vieles mehr. Mit unserer RESTful API können Sie HTTP-Anfragen senden,
um Daten zu lesen, zu erstellen, zu aktualisieren und zu löschen, was Ihnen die Flexibilität gibt, die Sie benötigen, um
Ihre Anwendung nach Ihren spezifischen Anforderungen zu gestalten. Wir unterstützen auch verschiedene
Authentifizierungsmethoden, um sicherzustellen, dass Ihre Daten sicher und geschützt sind.

Unsere API-Dokumentation bietet ausführliche Anleitungen zu jedem Endpunkt, einschließlich der erforderlichen Parameter,
der erwarteten Antworten und Beispiele für Anfragen und Antworten. Sie finden auch allgemeine Anleitungen zum Umgang mit
Fehlern, zur Authentifizierung und zum Paginieren durch große Datensätze.

baseURL = `contact us to receive the baseURL`
projectKey `contact us to receive the projectKey`

## Authentication with USERNAME and PASSWORD (Option 1)

### POST Request

`https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key={projectKey}`

body

```JSON
{
  "email": "your@email.com",
  "password": "your_password",
  "returnSecureToken": "true"
}
```

## Authentication with CUSTOMER_ID and API_KEY (Option 2)

### STEP1: POST Request

`{baseURL}/auth`

body

```JSON
{
  "customerID": "your_customerID",
  "apiKey": "your_apiKey"
}
```

response

```
customToken
```

### STEP2: POST Request

`https://identitytoolkit.googleapis.com/v1/accounts:signInWithCustomToken?key={projectKey}`

REQUEST BODY

```JSON
{
  "token": "{{customToken}}",
  "returnSecureToken": "true"
}
```

SAMPLE RESPONSE

```JSON
{
  "idToken": "[ID_TOKEN]",
  "refreshToken": "[REFRESH_TOKEN]",
  "expiresIn": "3600"
}
```

# AUTHORIZATIONS

set authorization header for every request

```
Authorization: Bearer {{customToken}}
```

# Routes

## Properties

### Get All properties

GET `{baseURL}/properties`

SAMPLE RESPONSE

```JSON
[
  {
    "id": "[ID]",
    "customerID": "[CUSTOMER_ID]",
    "h_id": "[H_ID]",
    "h_id_text": "[H_ID_TEXT]",
    "address": "[ADDRESS]",
    "createdAt": "[CREATED_AT]",
    "updatedAt": "[UPDATED_AT]",
    "type": "[TYPE]",
    "managementType": "[MANAGEMENT_TYPE]",
    "isLocked": "[IS_LOCKED]",
    "wegLandlordsName": "[wegLandlordsName]",
    "landlord": "[LANDLORD]",
    "bankAccount": "[BANK_ACCOUNT]",
    "wegBankAccount": "[WEG_BANK_ACCOUNT]",
    "reserveBankAccount": "[RESERVE_BANK_ACCOUNT]",
    "archived": "[ARCHIVED]",
    "deleted": "[DELETED]",
    "rentalStats": "[RENTAL_STATS]"
  }
]
```

### Get Property By ID - {propertyID}

GET `{baseURL}/properties/:propertyID`

REQUEST PARAMS

```typescript
propertyID: string
```

SAMPLE RESPONSE

```JSON
{
  "id": "[ID]",
  "customerID": "[CUSTOMER_ID]",
  "h_id": "[H_ID]",
  "h_id_text": "[H_ID_TEXT]",
  "address": "[ADDRESS]",
  "createdAt": "[CREATED_AT]",
  "updatedAt": "[UPDATED_AT]",
  "managementType": "[MANAGEMENT_TYPE]",
  "isLocked": "[IS_LOCKED]",
  "wegLandlordsName": "[wegLandlordsName]",
  "landlord": "[LANDLORD]",
  "bankAccount": "[BANK_ACCOUNT]",
  "wegBankAccount": "[WEG_BANK_ACCOUNT]",
  "reserveBankAccount": "[RESERVE_BANK_ACCOUNT]",
  "archived": "[ARCHIVED]",
  "deleted": "[DELETED]",
  "rentalStats": "[RENTAL_STATS]"
}
```

----------

## Units

### Get All units by PropertyID

GET `{baseURL}/properties/:propertyID/units`

Params

```typescript
propertyID: string
```

### Get All Unit byID

GET `{baseURL}/properties/:propertyID/units/:unitID`

Params

```typescript
propertyID: string
unitID: string
```

----------

## Periods

### Get PeriodByID

GET `{baseURL}/properties/:propertyID/units/:unitID/periods/:periodID`

Params

```typescript
propertyID: string
unitID: string
periodID: string
```

### Get current Periods what will end

GET `{baseURL}/periods/filtered/ended`

### Create new period

POST `{baseURL}/properties/:propertyID/units/:unitID/periods`

Params

```typescript
propertyID: string
unitID: string
```

BODY

``` PERIOD SCHEME ```

----------

## Tenants

### Get all tenants per period

GET `{baseURL}/properties/:propertyID/units/:unitID/periods/:periodID/tenants`

Params

```typescript
propertyID: string
unitID: string
periodID: string
```

Response: `tenants[]` array of tenants

### Create new tenant within a period

POST `{baseURL}/properties/:propertyID/units/:unitID/periods/:periodID`

Params

```typescript
propertyID: string
unitID: string
periodID: string
```

BODY

``` TENANT SCHEME ```

You received the SCHEME per E-Mail separately

---

more routes and features are coming soon...

---


<a name="support"/>

## Support

- Drop an email to: [SUPPORT E-MAIL](mailto:support@nahaus.de)
- or open an appropriate [issue](https://github.com/Nahaus-de/api-docs/issues)

Built by and for developers :heart: we will help you :punch:

---

<a name="license"/>

## License

Copyright (c) 2023 [Nahaus.de](https://github.com/Nahaus-de). Licensed under the MIT License (MIT)

