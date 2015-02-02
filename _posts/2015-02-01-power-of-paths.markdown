---
layout: post
title:  "The Power of Paths"
date:   2015-02-01 19:00:00
categories: Paths
---

Paths are used to query JSON for field values.

The compact notation allows many defaults and abbreviations for common cases. Given the source JSON

```json
{
  "id": 12345,
  "name": {
    "first": "Simple First",
    "last": "Simple Last"
  },
  "phone_numbers": ["867-5309", "606-0842"],
  "addresses": [{
      "street": "123 Street"
    },{
      "street": "456 Street"
  }]
}
```

the following paths can be derived:

- `/id/*`
The simplest path is the key value. Here the path is describing the id as residing at the top level with a value that is not a collection.

- `/name/first/*`
Here the first field is nested under name and is not a collection.

- `/phone_numbers/[]`
A variation of the key value except the value is a collection.

- `/addresses//street/*`
Here the street field is described as nested under addresses within a collection, but the field value itself is not a collection.

SimpleAPI requires API publishers to use paths to describe the JSON they will accepted and return. When the API is installed from the Marketplace the published paths will be used to create a DataEncoding for the installer. The installer can then go and update the DataEncoding altering the paths to reflect the format they require for the data.

Here are some scenarios for possible paths:

__The API returns a collection but the installer deals with individuals__

The API's path `/TWITTER/[]`
The installer can set up the DataEncoding path to be `/TWITTER/*`

The installer can send JSON

```json
{
  ...
  "TWITTER": "simple_api",
  ...
}
```

and SimpleAPI will automatically turn it into

```json
{
  ...
  "TWITTER": ["simple_api"],
  ...
}
```

when sending to to the API. The inverse is true. _A caveat to be wary of is that since the data from the API is a collection SimpleAPI will only return the first item of the collection to the installer._


__The installer uses collections, but the API equivalent is an individual__

The API's path `/street/*`
The installer's path `/addresses//street/*`

The installer can send JSON

```json
{
  ...
  "addresses": [{
    "street": "123 street",
    ...
  },{
    "street": "456 street",
    ...
  }],
  ...
}
```

and SimpleAPI will automatically turn it into

```json
{
  ...
  "street": "123 street",
  ...
}
```

when sending to to the API. The inverse is true. _A caveat to be wary of is that since the data from the installer is a collection SimpleAPI will only send the first item of the collection to the installer._

__The API says _Tomato_, the installer says _Tomatoe___

The API's path `/FIRST_NAME/*`
The installer's path `/fname/*`

The installer can send JSON

```json
{
  ...
  "fname": "Simple First",
  ...
}
```

and SimpleAPI will automatically turn it into

```json
{
  ...
  "FIRST_NAME": "Simple First",
  ...
}
```

Less drastic of a change, but SimpleAPI does the heavy lifting so your data can remain consistent from native representation to API integration and back again.

Feel free to [contact-us](mailto:{{ site.email }}) regarding any questions you have or support you need while using SimpleAPI.
