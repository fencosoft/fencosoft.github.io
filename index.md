---
layout: default
title: Fencosoft API Documentation
---
# DataGen API Reference & Tutorial

Welcome to the DataGen API documentation page. 
Please review this document thoroughly before posting requests to the API.

* * *
## Url Parameters
The only required parameter is **{quantity}.

For example, if you would like 500 documents returned you would set the **{quantity} parameter like this:

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
For example, if I wanted to create an array of 10 products that contain the following fields:
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
Then I would call the POST to the API and set the **{quantity} parameter to 10:
```
/api/v1/generate/10
```

And here is an example response from the API given the request above:
```json
{
  "requestId": "7dd5d8dc-4e8b-43e0-8863-7bb71d51eb03",
  "success": true,
  "recordCount": 10,
  "data": [
    {
      "productName": "skip ashamed linen crash",
      "productNumber": 7133,
      "price": 189.81,
      "quantityOnHand": 23
    },
    {
      "productName": "terrific plastic overflow",
      "productNumber": 6491,
      "price": 22.71,
      "quantityOnHand": 132
    },
    {
      "productName": "kindhearted bite-sized effect",
      "productNumber": 5715,
      "price": 123.84,
      "quantityOnHand": 37
    },
    {
      "productName": "horn treat",
      "productNumber": 9163,
      "price": 129.88,
      "quantityOnHand": 135
    },
    {
      "productName": "protest window travel",
      "productNumber": 8371,
      "price": 111.91,
      "quantityOnHand": 8
    },
    {
      "productName": "tired",
      "productNumber": 9372,
      "price": 84.59,
      "quantityOnHand": 88
    },
    {
      "productName": "quarrel hot cow",
      "productNumber": 1188,
      "price": 102.81,
      "quantityOnHand": 173
    },
    {
      "productName": "estate degree comfortable",
      "productNumber": 7557,
      "price": 159.48,
      "quantityOnHand": 38
    },
    {
      "productName": "suit",
      "productNumber": 5713,
      "price": 161.74,
      "quantityOnHand": 149
    },
    {
      "productName": "mom line",
      "productNumber": 3405,
      "price": 14.33,
      "quantityOnHand": 85
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

