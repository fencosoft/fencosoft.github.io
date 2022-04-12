---
layout: default
title: Fencosoft API Documentation
---
# DataGen API Reference & Tutorial

Welcome to the DataGen API documentation page. 
Please review this document thoroughly before posting requests to the API.

* * *
## Url Parameters
The only required parameter is quantity.

For example, if you would like 500 documents returned you would post your request like this:

```
/api/v1/generate/500
```


## Request Body
The request body requires the `schema` object.
Within this object you will define your entire schema and data types for each field.

Basic request example:
```json
{
  "schema": {
    "desiredFieldName": {
      "type": "int",
        "min": 100,
        "max": 2000
    }
  }
}
```
Response:
```json
{
  "requestId": "148c4f3b-d13e-4e76-b6fb-fa3bdf3e08b5",
  "success": true,
  "recordCount": 1,
  "data": [
    {
      "desiredFieldName": 1322
    }
  ]
}
```

As you can see, we've requested 1 document to be returned with the given schema and the response contains an array called `data`
with a single document. The returned document has the field name that was defined in the schema and a randomly generated integer between 100 and 2000.

The `schema` object is structured like a typical JSON document.

#### Data Types:

| Data Type | Notes                                            |
|:----------|:-------------------------------------------------|
| bool      |                                                  |
| float     |                                                  |
| int       |                                                  |
| date      | Just a date                                      |
| dateTime  | Date and time                                    |
| uuid1     |                                                  |
| uuid4     |                                                  |
| string    | Must specify a `reservedType`                    |
| array     | Can contain any data type above, including array |

#### ReservedTypes:

| reservedType | Description                                                         |
|:-------------|:--------------------------------------------------------------------|
| firstName    | A randomly selected first name                                      |
| lastName     | A randomly selected last name                                       |
| middleName   | A randomly selected first name or inital                            |
| fullName     | A randomly selected first and last name with randomized middle name |
| businessName | A randomly generated business name constructed from business words  |
| address1     |                                                                     |
| address2     |                                                                     |
| city         |                                                                     |
| state        |                                                                     |
| stateName    |                                                                     |
| zip          |                                                                     |
| country      |                                                                     |
| phone        |                                                                     |
| url          |                                                                     |
| email        |                                                                     |
| imageUrl     |                                                                     |
| searchable   |                                                                     |
| varchar      |                                                                     |


## Response Object

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

