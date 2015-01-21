---
layout: doc
title:  "Jobs"
---
# Supported Actions

### Read

<p>
  <code class="url">GET /v1/app/jobs/{id}</code>
</p>

``` curl
curl https://simpleapi.io/v1/app/jobs/1 \
  -H 'Authorization: Token {{"{{user_token"}}}}'
```

**Example Response**

``` json
{
  "id": 1,
  "status": "processed",
  "params": {"updated_since": "2015-01-04T22:07:23-0500"},
  "api": "RemoteAPI",
  "data_encoding": "My RemoteAPI Encoding",
  "data_encoding_id": 1,
  "encoded_resource": "Contacts",
  "results": [
    {"CONTACT_ID": 94941790, "FIRST_NAME": "Coty"}
  ]
}
```

### List

<p>
  <code class="url">GET /v1/app/jobs</code>
</p>

``` curl
curl https://simpleapi.io/v1/app/jobs \
  -H 'Authorization: Token {{"{{user_token"}}}}'
```

**Example Response**

``` json
[{
  "id": 1,
  "status": "processed",
  "params": {"updated_since": "2015-01-04T22:07:23-0500"},
  "api": "RemoteAPI",
  "data_encoding": "My RemoteAPI Encoding",
  "data_encoding_id": 1,
  "encoded_resource": "Contacts",
  "results": [
    {"CONTACT_ID": 94941790, "FIRST_NAME": "Coty"}
  ]
}]
```

# Attributes (read-only)

| Name | Type | Comment |
| - | - | - |
| id | integer |
| status | string | Statuses are `queued`, `requesting`, `encoding`, `processed`, `errored`
| params | json | Only returned for `GET` requests
| api | string | The name of the installed API
| data_encoding | string |
| data_encoding_id | integer | The `data_encoding_id` used in the request
| encoded_resource | string |
| results | json | Only returned when status is `processed`
| message | string | Usually an error message from the API

**List action only returns id and status*
