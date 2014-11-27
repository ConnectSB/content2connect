---
title: Content2Connect API

language_tabs:
  - shell

includes:

search: false
---

# Introduction

Welcome to ConnectSB's Content2Connect API. This is still a work in progress.

# Authentication

Content2Connect uses OAuth2 for authenticating and authorizing users.

Content2Connect excepts for the access token be included in all API requests, this is a GET parameter which looks like this:

`?access_token=CONTENT2CONNECTACCESSTOKEN`

## Request authorization code

### HTTP Request
`GET http://csbauth2.apps2connect.nl/oauth/v2/auth`

### Query parameters
Parameter | Description
--------- | ------- | -----------
client_id | String which was sent by us when applying for a client.
redirect_uri | URI to redirect to with the response, this should be set to one of the URI's you provided when applying for a client.
scope | Space seperated list of the scopes to request an authorization code for.
response_type | This can only be code for now.

<aside class="notice">
  For now only the scopes: email & content are supported
</aside>

## Request access code

### HTTP Request
`POST http://csbauth2.apps2connect.nl/oauth/v2/token`

### Post parameters
Parameter | Description
--------- | -----------
grant_type | Can only be authorization_code
code | Code that was received from the authorization code request
redirect_uri | URI to redirect to with the response, this should be set to one of the URI's you provided when applying for a client.
client_id | String which was sent by us when applying for a client.
client_secret | String which was sent by us when applying for a client.


> Successful request to this end-point will return JSON structured like this:

```json
{
  "access_token": "CONTENT2CONNECTACCESSTOKEN",
  "expires_in": 3600,
  "token_type": "bearer",
  "scope": "content",
  "refresh_token": "CONTENT2CONNECTREFRESHTOKEN"
}
```

## Refresh your access code

### HTTP Request
`POST http://csbauth2.apps2connect.nl/oauth/v2/token`

### Post parameters
Parameter | Description
--------- | ---------
grant_type | Can only be refresh_token
client_id | String which was sent by us when applying for a client.
client_secret | String which was sent by us when applying for a client.
refresh_token | Refresh token which was received when requesting access code

> Successful request to this end-point will return JSON structured like this:

```json
{
  "access_token": "CONTENT2CONNECTACCESSTOKEN",
  "expires_in": 3600,
  "token_type": "bearer",
  "scope": "content",
  "refresh_token": "CONTENT2CONNECTREFRESHTOKEN"
}
```

# Content2Connect

## Get all user's content

Request to this URL will return the user's content.

### HTTP Request
`GET http://content.connectsb.nl/api/content`

### Query parameters
Parameter | Description
--------- | -----------
access_token | Access token received by successfully requesting access code

> Successful request to this end-point will return JSON structured like this:

```json
{
  "content_items": [
    "/uploads/content_uploads/test.jpeg"
  ]
}
```

