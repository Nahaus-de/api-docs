# Nahaus API V2.0.0

[EN]

**Nahaus Enterprise API V2**

Welcome to the **Nahaus.de API V2** documentation! This repository contains comprehensive guides and documentation to help you start working with Nahaus.de's API as quickly as possible and support you in effectively integrating your software.

**Documentation URL:** [Interactive Swagger UI](https://europe-west3-pool-dev-nahaus-de.cloudfunctions.net/api-v2/docs/v2/)

**Base URL:** `https://europe-west3-pool-dev-nahaus-de.cloudfunctions.net`

**Please Note:** To access and use the Nahaus.de API, you must possess an ENTERPRISE ACCOUNT with Nahaus.de.

[DE]

Die **nahaus API V2** ermöglicht es Entwicklern, auf die Funktionalitäten unserer Immobilienmanagement-Software zuzugreifen und diese in ihre eigenen Anwendungen zu integrieren.

Sie können die API verwenden, um nicht nur Immobilien und Einheiten zu verwalten, sondern auch Kontakte, Finanzen (Ausgaben), Scrumboards, Kalender, Erinnerungen, Dokumente und Zählerstände zu integrieren. Mit unserer RESTful API können Sie HTTP-Anfragen senden, um Daten zu lesen, zu erstellen, zu aktualisieren und zu löschen.

---

## Authentication

The V2 API uses **Bearer Token** authentication. You must first exchange your credentials for an ID Token.

### 1. Login to get Access Token

**POST** `/api-auth/login`

> **Note:** This endpoint specifically uses the Auth Service URL: `https://europe-west3-pool-dev-nahaus-de.cloudfunctions.net`

**Request Body:**

```json
{
  "email": "user@example.com",
  "password": "password123",
  "returnSecureToken": true
}

```

**Response:**

```json
{
  "idToken": "[YOUR_ACCESS_TOKEN]",
  "email": "user@example.com",
  "refreshToken": "[REFRESH_TOKEN]",
  "expiresIn": "3600",
  "localId": "..."
}

```

### 2. Authorize Requests

Include the `idToken` from the login response in the **Authorization** header of every subsequent request.

```text
Authorization: Bearer [YOUR_ACCESS_TOKEN]

```

---

# Routes & Resources

## 👥 Contacts

*Manage address book contacts.*

* **GET** `/api-v2/contacts`
* *Query:* `limit` (default: 25)
* *Description:* Get all contacts.


* **GET** `/api-v2/contacts/{contactID}`
* *Description:* Get details of a specific contact.


* **PUT** `/api-v2/contacts/{contactID}`
* *Body:* `Contact` object.
* *Description:* Update a contact.


* **DELETE** `/api-v2/contacts/{contactID}`
* *Description:* Delete a contact.



## 🏠 Landlords

*Manage owners.*

* **GET** `/api-v2/landlords`
* *Description:* List all landlords.


* **POST** `/api-v2/landlords`
* *Body:* `Landlord` object.
* *Description:* Create a new landlord.


* **GET** `/api-v2/landlords/{landlordID}`
* *Description:* Get Landlord by ID.


* **PUT** `/api-v2/landlords/{landlordID}`
* *Body:* `Landlord` object.
* *Description:* Update an existing landlord.



## 🧑‍💼 Managers

*Manage facility managers.*

* **GET** `/api-v2/managers`
* *Description:* List all managers.


* **POST** `/api-v2/managers`
* *Body:* `Manager` object.
* *Description:* Create a new manager.


* **GET** `/api-v2/managers/{managerID}`
* *Description:* Get manager details.


* **PUT** `/api-v2/managers/{managerID}`
* *Body:* `Manager` object.
* *Description:* Update a manager.


* **DELETE** `/api-v2/managers/{managerID}`
* *Description:* Delete a manager.



## 📝 MSA (Tenancy Application Management)

*Mieterselbstauskunft.*

* **GET** `/api-v2/msa`
* *Description:* List MSA entries.


* **POST** `/api-v2/msa`
* *Body:* `MSA` object.
* *Description:* Create a new MSA.


* **GET** `/api-v2/msa/{msaID}`
* *Description:* Get MSA by ID.


* **PUT** `/api-v2/msa/{msaID}`
* *Body:* `MSA` object.
* *Description:* Update MSA.


* **DELETE** `/api-v2/msa/{msaID}`
* *Description:* Delete MSA.



## 📋 Scrumboards

*Boards, Lists, and Cards.*

* **GET** `/api-v2/scrumboards`
* *Query:* `limit`, `cursor`, `page`
* *Description:* Get Scrumboards (Paginated).


* **POST** `/api-v2/scrumboards`
* *Body:* `Scrumboard` object.
* *Description:* Create Scrumboard.


* **GET** `/api-v2/scrumboards/{boardID}`
* *Description:* Get Board By ID.


* **PUT** `/api-v2/scrumboards/{boardID}`
* *Body:* `Scrumboard` object.
* *Description:* Update Board.


* **DELETE** `/api-v2/scrumboards/{boardID}`
* *Description:* Delete Board.



### Scrumboard Cards

* **GET** `/api-v2/scrumboards/{boardID}/cards`
* *Query:* `limit`, `cursor`, `page`
* *Description:* Get Cards for Board.


* **POST** `/api-v2/scrumboards/{boardID}/cards`
* *Body:* `ScrumboardCard` object.
* *Description:* Create Card.


* **PUT** `/api-v2/scrumboards/{boardID}/cards/{cardID}`
* *Body:* `ScrumboardCard` object.
* *Description:* Update Card.


* **DELETE** `/api-v2/scrumboards/{boardID}/cards/{cardID}`
* *Description:* Delete Card.



## 🔔 Reminders

*Time-based and recurring reminders.*

* **GET** `/api-v2/reminders` (Paginated)
* **POST** `/api-v2/reminders` (Body: `NahausReminder`)
* **GET** `/api-v2/reminders/{reminderID}`
* **PUT** `/api-v2/reminders/{reminderID}` (Body: `NahausReminder`)
* **DELETE** `/api-v2/reminders/{reminderID}`

## 📅 Calendars

*Calendar management.*

* **GET** `/api-v2/calendars` (Paginated)
* **POST** `/api-v2/calendars` (Body: `NahausCalendar`)
* **GET** `/api-v2/calendars/{calendarID}`
* **PUT** `/api-v2/calendars/{calendarID}` (Body: `NahausCalendar`)
* **DELETE** `/api-v2/calendars/{calendarID}`

## 💶 Expenses

*Financial expenses and invoices.*

* **GET** `/api-v2/expenses` (Paginated)
* **POST** `/api-v2/expenses` (Body: `Expense`)
* **GET** `/api-v2/expenses/{expenseID}`
* **PUT** `/api-v2/expenses/{expenseID}` (Body: `Expense`)
* **DELETE** `/api-v2/expenses/{expenseID}`

## 🏢 Properties

*Real estate properties.*

* **GET** `/api-v2/properties`
* *Description:* Get All Properties.


* **POST** `/api-v2/properties`
* *Body:* `Property` object.
* *Description:* Create Property.


* **GET** `/api-v2/properties/{propertyID}`
* **PUT** `/api-v2/properties/{propertyID}`
* **DELETE** `/api-v2/properties/{propertyID}`

## 🚪 Units

*Rental units.*

* **GET** `/api-v2/properties/{propertyID}/units`
* *Description:* Get Units of a Property.


* **POST** `/api-v2/properties/{propertyID}/units`
* *Body:* `Unit` object.
* *Description:* Create Unit.


* **GET** `/api-v2/properties/{propertyID}/units/{unitID}`
* **PUT** `/api-v2/properties/{propertyID}/units/{unitID}`
* **DELETE** `/api-v2/properties/{propertyID}/units/{unitID}`

## 👥 Periods (Tenancies)

*Rental periods and Tenancies.*

* **GET** `/api-v2/periods/filtered/ended`
* *Description:* Get ended periods.


* **POST** `/api-v2/properties/{propertyID}/units/{unitID}/periods`
* *Body:* `RentalPeriod` object.
* *Description:* Create new rental period.


* **GET** `/api-v2/properties/{propertyID}/units/{unitID}/periods/{periodID}`
* *Description:* Get Period/Tenant Details.


* **POST** `/api-v2/properties/{propertyID}/units/{unitID}/periods/{periodID}`
* *Description:* Create Tenant in Period.



## 🔑 Managements

*Management contracts for units.*

* **GET** `/api-v2/properties/{propertyID}/units/{unitID}/managements`
* **POST** `/api-v2/properties/{propertyID}/units/{unitID}/managements` (Body: `Management`)
* **GET** `/api-v2/properties/{propertyID}/units/{unitID}/managements/{managementID}`
* **PUT** `/api-v2/properties/{propertyID}/units/{unitID}/managements/{managementID}` (Body: `Management`)
* **DELETE** `/api-v2/properties/{propertyID}/units/{unitID}/managements/{managementID}`

## ⏲️ Meters & Readings

*Property and Unit meters.*

### Property Meters

* **GET** `/api-v2/properties/{propertyID}/meters`
* **POST** `/api-v2/properties/{propertyID}/meters` (Body: `Meter`)
* **PUT** `/api-v2/properties/{propertyID}/meters/{meterID}` (Body: `Meter`)
* **DELETE** `/api-v2/properties/{propertyID}/meters/{meterID}`

### Unit Meters

* **GET** `/api-v2/properties/{propertyID}/units/{unitID}/meters`
* **POST** `/api-v2/properties/{propertyID}/units/{unitID}/meters` (Body: `Meter`)
* **PUT** `/api-v2/properties/{propertyID}/units/{unitID}/meters/{meterID}` (Body: `Meter`)
* **DELETE** `/api-v2/properties/{propertyID}/units/{unitID}/meters/{meterID}`

### Meter Readings

* **POST** `/api-v2/properties/{propertyID}/meters/{meterID}/readings`
* *Body:* `MeterReading`


* **POST** `/api-v2/properties/{propertyID}/units/{unitID}/meters/{meterID}/readings`
* *Body:* `MeterReading`



## 📂 Files

*File and Folder management.*

* **GET** `/api-v2/files`
* *Query:* `folderID`, `limit`, `page`.


* **POST** `/api-v2/files`
* *Body:* `FileMetadata`.


* **GET** `/api-v2/files/{fileID}`
* **PUT** `/api-v2/files/{fileID}`
* *Body:* `FileMetadata`.


* **DELETE** `/api-v2/files/{fileID}`

---

# Data Schemas (JSON Models)

### Property

```json
{
  "address": {
    "street": "string",
    "city": "string",
    "postalCode": "string",
    "country": "string"
  },
  "propertyType": "APARTMENT_BUILDING",
  "totalUnits": 12,
  "yearBuilt": 1995,
  "totalLivingArea": 1850.5
}

```

### Unit

```json
{
  "label": "Apartment 101",
  "unitType": "APARTMENT",
  "size": 85.5,
  "rooms": 3
}

```

### Contact

```json
{
  "firstName": "Fatima",
  "lastName": "Dib",
  "displayName": "Fatima Dib",
  "emails": [
    { "label": "work", "value": "fatima@example.com" }
  ],
  "phoneNumbers": [
    { "type": "MOBILE", "value": "0356972654" }
  ]
}

```

### Landlord

```json
{
  "type": "PRIVATE", // or COMMERCIAL
  "firstName": "string",
  "lastName": "string",
  "email": "user@example.com",
  "phone": "string",
  "address": {
    "street": "string",
    "city": "string",
    "postalCode": "string",
    "country": "string"
  },
  "bankAccount": {
    "iban": "string",
    "bic": "string",
    "accountHolder": "string"
  }
}

```

### Meter

```json
{
  "m_id": "WATER-001",
  "type": "WATER", // WATER, ELECTRICITY, GAS, HEAT, OIL
  "description": "string",
  "meterLocation": "string",
  "manufacturer": "string",
  "serialNumber": "string",
  "unit": "m³",
  "initialValue": 0,
  "factor": 1
}

```

### MeterReading

```json
{
  "value": 1250.75,
  "date": "2023-10-27T10:00:00Z",
  "readBy": "Technician Name",
  "notes": "Annual check",
  "imageUrl": "https://..."
}

```

### Expense

```json
{
  "description": "Monthly maintenance fee",
  "amount": 150.75,
  "category": "Maintenance",
  "paymentMethod": "Bank Transfer",
  "supplierOrService": "Handyman Service Inc.",
  "includesVAT": true,
  "vatRate": 19,
  "date": "2023-10-01T00:00:00Z",
  "serviceStartDate": "2023-10-01",
  "serviceEndDate": "2023-10-31",
  "associatedProperty": "{propertyID}"
}

```

### ScrumboardCard

```json
{
  "title": "Schedule apartment viewing",
  "description": "Client is available after 5pm",
  "listId": "todo-list-123",
  "propertyID": "string",
  "unitID": "string",
  "dueDate": "2023-12-01T17:00:00Z",
  "priority": "NORMAL",
  "position": 0
}

```

### FileMetadata (NahausFile)

```json
{
  "name": "Rental Contract.pdf",
  "isFolder": false,
  "parentId": "folder-123",
  "mimeType": "application/pdf",
  "size": 2048,
  "downloadUrl": "string"
}

```

### MSA

```json
{
  "status": "WAITING",
  "contactData": {
    "firstName": "string",
    "lastName": "string",
    "email": "string"
  },
  "target": {
    "propertyID": "string",
    "unitID": "string",
    "netRentMax": 0
  },
  "employment": {
    "employer": "string",
    "incomeMonthlyNet": 0
  }
}

```

---

<a name="support"/>

## Support

* Drop an email to: [support@nahaus.de](mailto:support@nahaus.de)
* or open an appropriate [issue](https://github.com/Nahaus-de/api-docs/issues)

Built by and for developers :heart: we will help you :punch:

---

<a name="license"/>

## License

Copyright (c) 2023-2025 [Nahaus.de](https://github.com/Nahaus-de). Licensed under the MIT License (MIT)

```

```