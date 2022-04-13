---
layout: default
title: Fencosoft API Documentation
---
# DataGen API Reference & Tutorial

Welcome to the DataGen API documentation page. 
Please review this document thoroughly before posting requests to the API.

* * *
## Url Parameters
The only required parameter is *{quantity}*.

For example, if you would like 500 documents returned you would set the *{quantity}* parameter like this:

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

As you can see, we've requested 1 object to be returned with the given schema and the response contains an array called `data`
with a single object. The returned object contains a field named as it was defined in the schema with a value that is a randomly generated integer between 100 and 2000, as configured in the schema definition.

The `schema` object is structured like a standard JSON document and it defines the way you want your output objects/data to look.
For example, if I wanted to create an array of 5 products that contain the following fields:
- productName
- productNumber
- price
- quantityOnHand

I would build my request like this:
```json
{
  "schema": {
    "productName": {  // declare the name of the field
      "type": "string",  // indicate the data type
        "reservedType": "searchable",  // indicate the reservedType (this will be explained more)
          "minWords": 1,  // configure the parameters for the reservedType
          "maxWords": 4,
          "maxLength": 120
    },
    "productNumber": {
      "type": "int",
        "min": 1000,
        "max": 9999
    },
    "price": {
      "type": "float",
        "min": 1.01,
        "max": 199.99,
        "precision": 2
    },
    "quantityOnHand": {
      "type": "int",
        "min": 0,
        "max": 200
    }
  }
}
```
Then I would call the POST to the API and set the *{quantity}* parameter to 5:
```
/api/v1/generate/10
```

And here is an example response from the API given the request above:
```json
{
  "requestId": "2fcd1b12-8d1e-4e9b-ac9b-1f50eddc33ef",
  "success": true,
  "recordCount": 5,
  "data": [
    {
      "productName": "undress reason",
      "productNumber": 2594,
      "price": 84.11,
      "quantityOnHand": 18
    },
    {
      "productName": "egg flame statement",
      "productNumber": 5882,
      "price": 11.18,
      "quantityOnHand": 165
    },
    {
      "productName": "physical gather reconcile grant",
      "productNumber": 8312,
      "price": 31.15,
      "quantityOnHand": 33
    },
    {
      "productName": "cuddly",
      "productNumber": 9333,
      "price": 70.71,
      "quantityOnHand": 179
    },
    {
      "productName": "stomach",
      "productNumber": 8578,
      "price": 109.78,
      "quantityOnHand": 195
    }
  ]
}
```

### Data Types:
| Type Name | Notes                                            |
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

| Type Name    | Description                                                         |
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
```json
{
  "requestId": "30bfdf44-00a5-4025-b07f-de2ee23b6cdd",
  "success": true,
  "recordCount": 1,
  "data": [
    {
      "orderNumber": 1724,
      "itemNumber": 388,
      "orderQuantity": 4,
      "orderDate": "2019-04-06T18:35:12.000-05:00",
      "price": 9.19
    }
  ]
}
```

