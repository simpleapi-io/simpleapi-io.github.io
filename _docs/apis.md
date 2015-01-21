---
layout: doc
title:  "APIs"
---
# Supported Actions

### Create
Publish an API.

<p>
  <code class="url">POST /v1/app/apis</code>
</p>

``` curl
curl https://simpleapi.io/v1/app/apis \
  -H 'Authorization: Token {{"{{user_token"}}}}' \
  -H 'Content-Type: application/json' \
  -d '{"name":"RemoteAPI", ... }'
```

**Example Response**

``` json
{
  "id": 1,
  "name": "RemoteAPI",
  "install_url": "https://remoteapi.com/install",
  "uninstall_url": "https://remoteapi.com/uninstall",
  "is_active": false,
  "resources_attributes": [{
      "id": 1,
      "name": "Contacts",
      "customs_url": "https://remoteapi.com/customs",
      "search_url": "https://remoteapi.com/search",
      "created_url": "https://remoteapi.com/created",
      "updated_url": "https://remoteapi.com/updated",
      "read_url": "https://remoteapi.com/read",
      "create_url": "https://remoteapi.com/create",
      "update_url": "https://remoteapi.com/update",
      "delete_url": "https://remoteapi.com/delete",
      "fields_attributes": [
        {"id": 1, "name": "FIRST_NAME", "dpath": "/FIRST_NAME/*"},
        {"id": 2, "name": "EMAIL", "dpath": "/EMAIL/*"}
      ]
    }
  ]
}
```

### List
List APIs you have published.

<p>
  <code class="url">GET /v1/app/apis</code>
</p>

``` curl
curl https://simpleapi.io/v1/app/apis \
  -H 'Authorization: Token {{"{{user_token"}}}}'
```

**Example Response**

``` json
[{
  "id": 1,
  "name": "RemoteAPI",
  "install_url": "https://remoteapi.com/install",
  "uninstall_url": "https://remoteapi.com/uninstall",
  "is_active": false,
  "resources_attributes": [{
      "id": 1,
      "name": "Contacts",
      "customs_url": "https://remoteapi.com/customs",
      "search_url": "https://remoteapi.com/search",
      "created_url": "https://remoteapi.com/created",
      "updated_url": "https://remoteapi.com/updated",
      "read_url": "https://remoteapi.com/read",
      "create_url": "https://remoteapi.com/create",
      "update_url": "https://remoteapi.com/update",
      "delete_url": "https://remoteapi.com/delete",
      "fields_attributes": [
        {"id": 1, "name": "FIRST_NAME", "dpath": "/FIRST_NAME/*"},
        {"id": 2, "name": "EMAIL", "dpath": "/EMAIL/*"}
      ]
    }
  ]
}]
```


# Attributes

| Name | Type | Required | Comment |
| - | - | :-: |
| id | integer | | read-only
| name | string | &#10003; | name displayed in the Marketplace
| install_url | string | &#10003; | url used to associate SimpleAPI token with API user
| uninstall_url | string |
| is_active | boolean | | becomes active after approval by SimpleAPI
| [resources_attributes](#resources) | json | | nested json defining the resources available

## install_url

After a user has installed the active API the API will receive a `GET` request at the `install_url` location. The request will include a `token` and a `redirect_uri`. After the API has authenticated a user it should save the token with the user and redirect back to the `redirect_uri`.

**Example Install Request**

``` curl
curl 'https://remoteapi.com/install?token={{"{{simpleapi_token"}}}}&redirect_uri={{"{{redirect_uri"}}}}'
```

If SimpleAPI has been white-labeled the `redirect_uri` will not direct back to SimpleAPI.

___

<header class="doc-header">
  <h1 class="doc-title">Resources<a id="resources" ></a></h1>
</header>

# Attributes

| Name | Type | Required | Comment |
| - | - | :-: |
| id | integer | | read-only
| name | string | &#10003; |
| customs_url | string | |
| search_url | string | | `GET` request type
| created_url | string | | `GET` request type
| updated_url | string | | `GET` request type
| read_url | string | | `GET` request type
| create_url | string | | `POST` request type
| update_url | string | | `PUT` request type
| delete_url | string | | `DELETE` request type
| [fields_attributes](#fields) | json | | nested json defining the fields available

## created_url

___

<header class="doc-header">
  <h1 class="doc-title">Fields<a id="fields" ></a></h1>
</header>

# Attributes

| Name | Type | Required | Comment |
| - | - | :-: |
| id | integer | | read-only
| name | string | | read-only, auto generated from dpath
| dpath | string | &#10003; | string representation of location of field within a returned record
