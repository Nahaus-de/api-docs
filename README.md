# Nahaus API V2.0.0

[EN]

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

**POST** `/api2-auth/login`

**Request Body:**

```json
{
  "email": "your@email.com",
  "password": "your_password",
  "returnSecureToken": true
}
````

**Response:**

```json
{
  "idToken": "[YOUR_ACCESS_TOKEN]",
  "email": "your@email.com",
  "refreshToken": "[REFRESH_TOKEN]",
  "expiresIn": "3600",
  "localId": "..."
}
```

### 2\. Authorize Requests

Include the `idToken` from the login response in the **Authorization** header of every subsequent request.

```text
Authorization: Bearer [YOUR_ACCESS_TOKEN]
```

-----

# Routes & Resources

## 👥 Contacts

Manage your address book contacts.

  * **GET** `/api-v2/contacts`
      * *Query Params:* `limit`
      * *Description:* Get all contacts.
  * **GET** `/api-v2/contacts/{contactID}`
      * *Description:* Get details of a specific contact.
  * **PUT** `/api-v2/contacts/{contactID}`
      * *Body:* `Contact` object.
      * *Description:* Update a contact.
  * **DELETE** `/api-v2/contacts/{contactID}`
      * *Description:* Delete a contact.

## 🏠 Landlords

Manage property owners.

  * **GET** `/api-v2/landlords`
      * *Description:* List all landlords.
  * **POST** `/api-v2/landlords`
      * *Body:* `Landlord` object.
      * *Description:* Create a new landlord.
  * **PUT** `/api-v2/landlords/{landlordID}`
      * *Body:* `Landlord` object.
      * *Description:* Update an existing landlord.

## 🧑‍💼 Managers

Manage facility managers and agents.

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

## 📝 MSA (Mieterselbstauskunft)

Manage tenancy applications.

  * **GET** `/api-v2/msa`
      * *Description:* List all applications.
  * **POST** `/api-v2/msa`
      * *Body:* `MSA` object.
      * *Description:* Create a new application manually.
  * **GET** `/api-v2/msa/{msaID}`
      * *Description:* Get application details.
  * **PUT** `/api-v2/msa/{msaID}`
      * *Body:* `MSA` object.
      * *Description:* Update status or details.
  * **DELETE** `/api-v2/msa/{msaID}`
      * *Description:* Delete an application.

## 📋 Scrumboards

Manage project boards, lists, and tasks.

  * **GET** `/api-v2/scrumboards`
      * *Description:* List all boards.
  * **POST** `/api-v2/scrumboards`
      * *Body:* `Scrumboard` object.
      * *Description:* Create a new board.
  * **GET** `/api-v2/scrumboards/{boardID}`
      * *Description:* Get board details.
  * **PUT** `/api-v2/scrumboards/{boardID}`
      * *Body:* `Scrumboard` object.
      * *Description:* Update board settings.

### Scrumboard Cards

  * **GET** `/api-v2/scrumboards/{boardID}/cards`
      * *Description:* Get all cards for a specific board.
  * **POST** `/api-v2/scrumboards/{boardID}/cards`
      * *Body:* `ScrumboardCard` object.
      * *Description:* Create a new card.
  * **PUT** `/api-v2/scrumboards/{boardID}/cards/{cardID}`
      * *Body:* `ScrumboardCard` object.
      * *Description:* Update a card.
  * **DELETE** `/api-v2/scrumboards/{boardID}/cards/{cardID}`
      * *Description:* Delete a card.

## 🔔 Reminders

Manage time-based and recurring reminders.

  * **GET** `/api-v2/reminders`
  * **POST** `/api-v2/reminders` (Body: `NahausReminder`)
  * **GET** `/api-v2/reminders/{reminderID}`
  * **PUT** `/api-v2/reminders/{reminderID}` (Body: `NahausReminder`)
  * **DELETE** `/api-v2/reminders/{reminderID}`

## 📅 Calendars

Calendar management.

  * **GET** `/api-v2/calendars`
  * **POST** `/api-v2/calendars` (Body: `NahausCalendar`)
  * **GET** `/api-v2/calendars/{calendarID}`
  * **PUT** `/api-v2/calendars/{calendarID}` (Body: `NahausCalendar`)
  * **DELETE** `/api-v2/calendars/{calendarID}`

## 💶 Expenses

Financial expenses and invoices.

  * **GET** `/api-v2/expenses`
  * **POST** `/api-v2/expenses` (Body: `Expense`)
  * **GET** `/api-v2/expenses/{expenseID}`
  * **PUT** `/api-v2/expenses/{expenseID}` (Body: `Expense`)
  * **DELETE** `/api-v2/expenses/{expenseID}`

## 🏢 Properties & Units

Manage Real Estate structure.

  * **GET** `/api-v2/properties`
      * *Description:* Get all real estate properties.
  * **POST** `/api-v2/properties`
      * *Description:* Create a property.
  * **GET** `/api-v2/properties/{propertyID}`
  * **PUT** `/api-v2/properties/{propertyID}`
  * **DELETE** `/api-v2/properties/{propertyID}`
  * **GET** `/api-v2/properties/{propertyID}/units`
      * *Description:* Get all units belonging to a specific property.
  * **POST** `/api-v2/properties/{propertyID}/units`
  * **GET** `/api-v2/properties/{propertyID}/units/{unitID}`
  * **PUT** `/api-v2/properties/{propertyID}/units/{unitID}`
  * **DELETE** `/api-v2/properties/{propertyID}/units/{unitID}`

## 👥 Tenants & Periods

Manage rental periods and tenancies.

  * **GET** `/api-v2/periods/filtered/ended`
      * *Description:* Get rental periods that have ended.
  * **POST** `/api-v2/properties/{propID}/units/{unitID}/periods`
      * *Description:* Create a new rental period.
  * **GET** `/api-v2/properties/{propID}/units/{unitID}/periods/{periodID}`
      * *Description:* Get details of a specific rental period/tenant.
  * **POST** `/api-v2/properties/{propID}/units/{unitID}/periods/{periodID}`
      * *Description:* Create a tenant within an existing period.

## 🔑 Managements

Manage property management contracts.

  * **GET** `/api-v2/properties/{propID}/units/{unitID}/managements`
  * **POST** `/api-v2/properties/{propID}/units/{unitID}/managements`
  * **GET** `/api-v2/properties/{propID}/units/{unitID}/managements/{mgmtID}`
  * **PUT** `/api-v2/properties/{propID}/units/{unitID}/managements/{mgmtID}`
  * **DELETE** `/api-v2/properties/{propID}/units/{unitID}/managements/{mgmtID}`

## ⏲️ Meters & Readings

Manage utility meters (Water, Electricity, Gas, etc.).

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
      * *Description:* Add a reading to a Property Meter.
  * **POST** `/api-v2/properties/{propertyID}/units/{unitID}/meters/{meterID}/readings`
      * *Body:* `MeterReading`
      * *Description:* Add a reading to a Unit Meter.

## 📂 Files

File and Folder management.

  * **GET** `/api-v2/files`
      * *Query Params:* `parentId` (ID of folder), `limit`.
      * *Description:* List files and folders.
  * **POST** `/api-v2/files`
      * *Body:* `FileMetadata`
      * *Description:* Create a folder or upload file metadata.
  * **GET** `/api-v2/files/{fileID}`
      * *Description:* Get file details.
  * **PUT** `/api-v2/files/{fileID}`
      * *Body:* `FileMetadata`
      * *Description:* Rename, move, or update a file.
  * **DELETE** `/api-v2/files/{fileID}`
      * *Description:* Delete a file or folder.

-----

# Data Schemas (JSON Models)

### Meter

```json
{
  "m_id": "WATER-001",
  "type": "WATER", // Options: WATER, ELECTRICITY, GAS, HEAT, OIL
  "description": "Main Connection",
  "meterLocation": "Basement",
  "manufacturer": "Siemens",
  "serialNumber": "SN-123456",
  "unit": "m³",
  "initialValue": 100.5,
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
  "imageUrl": "[https://storage.googleapis.com/](https://storage.googleapis.com/)..."
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
  "associatedProperty": "{propertyID}"
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

### ScrumboardCard

```json
{
  "title": "Schedule apartment viewing",
  "description": "Client is available after 5pm",
  "listId": "todo-list-123",
  "propertyID": "{optional_property_id}",
  "unitID": "{optional_unit_id}",
  "dueDate": "2023-12-01T17:00:00Z",
  "priority": "NORMAL" // Options: LOW, NORMAL, HIGH
}
```

### FileMetadata

```json
{
    "name": "Contract.pdf",
    "isFolder": false,
    "parentId": "folder_id_or_null",
    "mimeType": "application/pdf",
    "size": 1024
}
```

-----

\<a name="support"/\>

## Support

  - Drop an email to: [support@nahaus.de](mailto:support@nahaus.de)
  - or open an appropriate [issue](https://github.com/Nahaus-de/api-docs/issues)

Built by and for developers :heart: we will help you :punch:

-----

\<a name="license"/\>

## License

Copyright (c) 2023-2024 [Nahaus.de](https://github.com/Nahaus-de). Licensed under the MIT License (MIT)

```
```