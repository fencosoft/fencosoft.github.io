---
layout: default
title: Fencosoft API Documentation
---

# DataGen API Reference & Tutorial

Welcome to the DataGen API documentation page. Please read through carefully before posting requests to the API.

### Url Parameters
The only required parameter is quantity.
For example, if you would like 500 documents returned you would post your request like this:

`/api/v1/generate/[500]()`

### Request Body
The request body requires

```json
{
    "schema": {
        "desiredFieldName": {
            "type": "int",
            "min": 100,
            "max": 2000
    }
}
```


### Markdown

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
