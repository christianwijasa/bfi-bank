# API Design

## Account API

### Account Properties

#### Accounts

| No. | Name           | Data Type | Description               |
|-----|----------------|-----------|---------------------------|
| 1.  | account_id     | UUID      | Account ID                |
| 2.  | account_number | String    | Account number            |
| 3.  | balance        | Float64   | Balance of the account    |
| 4.  | created_at     | Timestamp | Time account created      |
| 5.  | updated_at     | Timestamp | Time account last updated |
| 6.  | deleted_at     | Timestamp | Time account deleted      |

#### Cards

| No. | Name        | Data Type | Description               |
|-----|-------------|-----------|---------------------------|
| 1.  | card_id     | UUID      | Card ID                   |
| 2.  | fk_account  | UUID      | Foreign key of account    |
| 3.  | card_number | String    | Card number               |
| 4.  | expiry      | String    | Expiry card               |
| 5.  | is_active   | Boolean   | Active status of the card |
| 6.  | created_at  | Timestamp | Time account created      |
| 7.  | updated_at  | Timestamp | Time account last updated |
| 8.  | deleted_at  | Timestamp | Time account deleted      |

### Get account

`[GET] /api/v1/account`

#### Request

Authorization: Bearer token

#### Response

```json
{
  "data": {
    "account_id": "",
    "account_number": "0000 0000 0000",
    "balance": 123,
    "card": {
      "card_id": "",
      "card_number": "0000 0000 0000 0000",
      "expiry": "02/27",
      "is_active": true
    }
  },
  "error_code": "",
  "message": ""
}
```

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description   |
|-----|--------|-------------|---------------|
| 1.  | ACC000 | 500         | Unknown error |
| 2.  | ACC001 | 401         | Unauthorized  |

### Create new card

`[POST] /api/v1/account/card`

#### Request

Authorization: Bearer token

#### Response

```json
{
  "data": {
    "card_id": "",
    "card_number": "0000 0000 0000 0000",
    "expiry": "02/27"
  },
  "error_code": "",
  "message": ""
}
```

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description                  |
|-----|--------|-------------|------------------------------|
| 1.  | ACC000 | 500         | Unknown error                |
| 2.  | ACC001 | 401         | Unauthorized                 |
| 3.  | ACC100 | 400         | There's still an active card |

### Deactivate card

`[POST] /api/v1/account/card/deactivate`

#### Request

Authorization: Bearer token

| No. | Name    | Required | Data Type | Description                          |
|-----|---------|----------|-----------|--------------------------------------|
| 1.  | card_id | TRUE     | Integer   | Card ID that wants to be deactivated |

#### Response

```json
{
  "data": {
    "card_id": "",
    "deleted_at": "2023-12-31 00:00:00"
  },
  "error_code": "",
  "message": ""
}
```

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description     |
|-----|--------|-------------|-----------------|
| 1.  | ACC000 | 500         | Unknown error   |
| 2.  | ACC001 | 401         | Unauthorized    |
| 3.  | ACC200 | 400         | Invalid card ID |

## Contact API

### Contact Properties

#### Contacts

| No. | Name           | Data Type | Description               |
|-----|----------------|-----------|---------------------------|
| 1.  | contact_id     | UUID      | Contact's ID              |
| 2.  | account_number | String    | Contact's account number  |
| 3.  | bank_id        | UUID      | Bank contact's ID         |
| 4.  | contact_name   | String    | Contact's name            |
| 5.  | created_at     | Timestamp | Time Contact created      |
| 6.  | updated_at     | Timestamp | Time Contact last updated |
| 7.  | deleted_at     | Timestamp | Time Contact deleted      |

### Get contact list

`[GET] /api/v1/contacts`

#### Request

Authorization: Bearer token

| No. | Name   | Required | Data Type | Description                              |
|-----|--------|----------|-----------|------------------------------------------|
| 1.  | page   | FALSE    | Integer   | Page of products (Default 1)             |
| 2.  | limit  | FALSE    | Integer   | Limit item to retrieve (Default 20)      |
| 3.  | search | FALSE    | String    | Search by account number or contact name |

#### Response

```json
{
  "data": {
    "contacts": [
      {
        "contact_id": "",
        "account_number": "000 000 000",
        "bank_id": "BCA",
        "contact_name": "name",
        "created_at": "2023-12-31 00:00:00",
        "updated_at": "2023-12-31 00:00:00",
        "deleted_at": null
      }
    ],
    "page": 1,
    "limit": 20,
    "total": 100,
    "last": false
  },
  "error_code": "",
  "message": ""
}
```

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description   |
|-----|--------|-------------|---------------|
| 1.  | CNT000 | 500         | Unknown error |
| 2.  | ACC001 | 401         | Unauthorized  |

### Get contact by ID

`[GET] /api/v1/contact/{contact_id}`

#### Request

Authorization: Bearer token

| No. | Name       | Required | Data Type | Description          |
|-----|------------|----------|-----------|----------------------|
| 1.  | contact_id | TRUE     | UUID      | Search by contact id |

#### Response

```json
{
  "data": {
    "contact_id": "",
    "account_number": "000 000 000",
    "bank_id": "BCA",
    "contact_name": "name",
    "created_at": "2023-12-31 00:00:00",
    "updated_at": "2023-12-31 00:00:00",
    "deleted_at": null
  },
  "error_code": "",
  "message": ""
}
```

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description       |
|-----|--------|-------------|-------------------|
| 1.  | CNT000 | 500         | Unknown error     |
| 2.  | ACC001 | 401         | Unauthorized      |
| 3.  | CNT200 | 404         | Contact not found |

### Create contact

`[POST] /api/v1/contact`

#### Request

Authorization: Bearer token

| No. | Name           | Required | Data Type | Description      |
|-----|----------------|----------|-----------|------------------|
| 1.  | account_number | TRUE     | String    | Account's number |
| 2.  | bank_id        | TRUE     | String    | Bank's ID        |
| 3.  | contact_name   | TRUE     | String    | Contact's name   |

```json
{
  "account_number": "000 000 000",
  "bank_id": "BCA",
  "contact_name": "name"
}
```

#### Response

```json
{
  "data": {
    "contact_id": "",
    "account_number": "000 000 000",
    "bank_id": "BCA",
    "contact_name": "name",
    "created_at": "2023-12-31 00:00:00",
    "updated_at": "2023-12-31 00:00:00",
    "deleted_at": null
  },
  "error_code": "",
  "message": ""
}
```

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description                                  |
|-----|--------|-------------|----------------------------------------------|
| 1.  | CNT000 | 500         | Unknown error                                |
| 2.  | ACC001 | 401         | Unauthorized                                 |
| 3.  | CNT300 | 400         | Contact not registered in the requested bank |

### Delete Contact

`[DELETE] /api/v1/contact/{contact_id}`

#### Request

Authorization: Bearer token

| No. | Name       | Type | Required | Data Type | Description            |
|-----|------------|------|----------|-----------|------------------------|
| 1.  | contact_id | Path | TRUE     | UUID      | Contact's ID to delete |

```json
{
  "contact_id": ""
}
```

#### Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description       |
|-----|--------|-------------|-------------------|
| 1.  | CNT000 | 500         | Unknown error     |
| 2.  | ACC001 | 401         | Unauthorized      |
| 3.  | CNT400 | 400         | Contact not found |
