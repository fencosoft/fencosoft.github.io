---
layout: default
title: Fencosoft API Documentation
---
# DataGen API Reference & Tutorial

Welcome to the DataGen API documentation page. 
Please review this document thoroughly before posting requests to the API.

* * *
## Url Parameters
The only required parameter is `quantity`.

For example, if you would like 500 documents returned you would set the `quantity` parameter like this:

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
    "productName": {
      "type": "string",
      "reservedType": "searchable",
        "minWords": 1,
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
Then I would call the POST to the API and set the `quantity` parameter to 5:
```
/api/v1/generate/5
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

### Schema Fields
A schema field is an object that defines the name of the field, the data type of the field value and
parameter values for the given data type when applicable.

Let's use the field `productNumber` from our example above.
We have declared that this field will return a random value of type `int`.
The `int` type requires `min` and `max` range values so that it can return a random integer between the two.
In our example we set the range from 1000 to 9999.
```json
{
  "schema": {
    "productNumber": { // Define the name of the field
      "type": "int", // Declare a data type
      "min": 1000, // The lowest value integer in the range
      "max": 9999 // The highest value integer in the range
    }
  }
}
```

### Data Types
There are 9 basic data types to choose from when building your schema.
See the charts below for configuration options and usage details.

| Type      | * Required attribute                                                    |
|:----------|:------------------------------------------------------------------------|
| bool      | Returns `true` or `false`                                               |
| float     | `*max`: -9007199254740991 to 9007199254740991                           |
|           | `*min`: -9007199254740991 to 9007199254740991 (must be less than `max`) |
|           | `*precision`: 1 to 14                                                   |
|           | `allowNull`: true or false (allows the value to randomly return `null`) |
| int       | `*max`: -9007199254740991 to 9007199254740991                           |
|           | `*min`: -9007199254740991 to 9007199254740991 (must be less than `max`) |
|           | `allowNull`: true or false (allows the value to randomly return `null`) |
| date      | `dayMin`: 1 - 31                                                        |
|           | `dayMax`: 1 - 31                                                        |
|           | `monthMin`: 1 - 12                                                      |
|           | `monthMax`: 1 - 12                                                      |
|           | `*yearMin`: 1 - current year + 200                                      |
|           | `*yearMax`: 1 - current year + 200                                      |
|           | `format`: M = month, d = day, y = year. 'MM/dd/yyyy' = 01/01/1970       |
|           | `allowNull`: true or false (allows the value to randomly return `null`) |
|           | Default format: 'yyyy-MM-dd'                                              |
| dateTime  | `dayMin`: 1 - 31                                                          |   
|           | `dayMax`: 1 - 31                                                          |
|           | `monthMin`: 1 - 12                                                        |
|           | `monthMax`: 1 - 12                                                        |
|           | `*yearMin`: 1 - current year + 200                                        |
|           | `*yearMax`: 1 - current year + 200                                        |
|           | `hourMin`: 0 - 23                                                         |
|           | `hourMax`: 0 - 23                                                         |
|           | `minuteMin`: 0 - 59                                                       |
|           | `minuteMax`: 0 - 59                                                       |
|           | `secondMin`: 0 - 59                                                       |
|           | `secondMax`: 0 - 59                                                       |
|           | `format`: M = month, d = day, y = year, h = hour, m = minute, s = second  |
|           | `allowNull`: true or false (allows the value to randomly return `null`)   |
|           | Default format: ISODate                                                   |
| uuid1     | Returns a uuid1 GUID                                                      |
| uuid4     | Returns a uuid4 GUID                                                      |
| string    | `*minLength`: 1 - less than or equal to `maxLength`                       |
|           | `*maxLength`: 1 - 8000                                                    |
|           | `reservedType`: See the [Reserved Types](#reserved-types) table below.    |
|           | `allowNull`: true or false (allows the value to randomly return `null`)   |
|           | If `reservedType` is not specified a random varchar string is returned    |
| array     | `minElements`: 0 - 14999                                                  |
|           | `maxElements`: 1 - 15000                                                  |
|           | `*dataType`: All basic types plus `custom` (see below). Excludes `array`. |
|           | `allowNull`: true or false (allows the value to randomly return `null`)   |

The `custom` data type can be used to define a document within an array. When the `dataType` is set to `custom`
the `_definition_` attribute is used to define a document schema in exactly the same way as the `schema` attribute 
defines the overall schema.

```json
{
  "schema": {
    "arrayOfCustomType": {
      "type": "array",
      "minElements": 1,
      "maxElements": 3,
      "dataType": "custom",
      "_definition_": {
        "recordId": {
          "type": "uuid4"
        }
      }
    }
  }
}
```

### Reserved Types

Reserved types are strings that can populate commonly used data fields with "real world" values. 
Some follow specific formats while others are configureable.

| Type         | * Required attribute                                                |
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

The response object is very straightforward and consists of the following fields.

| Field Name  | Description                                                         |
|:------------|:--------------------------------------------------------------------|
| requestId   | A system generated guid used for tracking purposes.                 |
| success     | A boolean value to indicate the success of the request.             |
| recordCount | The number of records returned in the data array.                   |
| data        | An array of objects populated with data as defined in the `schema`  |


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

