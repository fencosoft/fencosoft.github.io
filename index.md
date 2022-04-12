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

### Data Types:

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

| Data Type | Notes                           |
|:----------|:--------------------------------|
| bool      |                                 |
| float     |                                 |
| int       |                                 |
| date      |                                 |
| dateTime  |                                 |
| uuid1     |                                 |
| uuid4     |                                 |
| string    | Must specify a `reervedType`    |
| array     | Can contain any data type above |


- bool
- float
- int
- date
- dateTime
- uuid1
- uuid4
- string
  - firstName
  - lastName
  - middleName
  - fullName
  - businessName
  - address1
  - address2
  - city
  - state
  - stateName
  - zip
  - country
  - phone
  - url
  - email
  - imageUrl
  - searchable
  - varchar
- array
  - bool
  - float
  - int
  - date
  - dateTime
  - uuid1
  - uuid2
  - string
    - firstName
    - lastName
    - middleName
    - fullName
    - businessName
    - address1
    - address2
    - city
    - state
    - stateName
    - zip
    - country
    - phone
    - url
    - email
    - imageUrl
    - searchable
    - varchar
    - custom

## Response Object

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```
Syntax highlighted code block

# Header 1

## Header 2

### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/fencosoft/fencosoft.github.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
