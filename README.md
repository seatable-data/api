# SeaTable Web API

## Basic

SeaTable manages your bases. A base contains multiple tables. A table contains columns and rows. A base is also called dtable in this API document.

SeaTable server consists of following component:

* dtable-web: The web site for manage bases.
* dtable-server: Store the bases and provide collaborating feature.
* seaf-server: Store attachments (files and images)

## API Basics

All API calls must be authenticated with a valid SeaTable API key.

```
curl -H 'Authorization: Token 24fd3c026886e3121b2ca630805ed425c272cb96' https://
cloud.seatable.io/api2/auth/ping/

```

The API key can be retrieved by the obtain auth token API. See `Quick Start` below.

For each API, we provide `curl` examples to illustrate the usage. We also provide `python`  examples:

* <https://github.com/seatable/seatable-python-scripts-examples>

## Status Code

* 200: OK
* 201: CREATED
* 202: ACCEPTED
* 301: MOVED_PERMANENTLY
* 400: BAD_REQUEST
* 403: FORBIDDEN
* 404: NOT_FOUND
* 409: CONFLICT
* 429: TOO_MANY_REQUESTS
* 440: REPO_PASSWD_REQUIRED
* 441: REPO_PASSWD_MAGIC_REQUIRED
* 500: INTERNAL_SERVER_ERROR
* 520: OPERATION_FAILED

## Quick Start

**ping**

```
curl https://cloud.seatable.io/api2/ping/

"pong"

```

**obtain auth token**

```
curl -d "username=username@example.com&password=123456" https://cloud.seatable.io/api2/auth-token/

{"token": "24fd3c026886e3121b2ca630805ed425c272cb96"}

```

you should use `--data-urlencode` if you want to process some special characters properly.

```
curl --data-urlencode username=user+name@example.com -d password=123456 https://cloud.seatable.io/api2/auth-token/

{"token":"265757b0a5aaf5d6b2e266d0c21791121ce6cdec"}

```

If you have enabled two-factor authentication, you need to add 2FA header in HTTP when getting the access token:

```
curl -d "username=username@example.com&password=123456" -H 'X-SEAFILE-OTP: <token>' https://cloud.seatable.io/api2/auth-token/

```

**auth ping**

```
curl -H 'Authorization: Token 24fd3c026886e3121b2ca630805ed425c272cb96' https://cloud.seatable.io/api2/auth/ping/

"pong"

```

## DTable Web APIs

See [DTable Web APIs](dtable-web-v2.1)

## DTable Web Admin APIs

See [DTable Web Admin APIs](dtable-web-v2.1-admin)

## DTable Server APIs

DTable server API is for calling APIs provided by the DTable server directly. You should first get an dtable access token, with this access token you can call the APIs to manipulate a dtable.

There are two ways to get an dtable access token. One is using your personal API Token, and get a dtable access token via API `api/v2.1/workspace/<workspace_id>/dtable/<name>/access-token/` .

The other is using a dtable's API token which can be generated in the dropdown menu of a dtable. To get access token with a dtable's API token, call the following API:

```
curl -H 'Accept: application/json; charset=utf-8; indent=4' 'Authorization: Token 8g971000df0d6fbntc59580766329a5b37adfh'"https://cloud.seatable.io/api/v2.1/dtable/app-access-token/"

```

The two ways will give you the same response as following

```
{    
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjkyMjYxNzEsImR0YWJsZV91dWlkIjoiYjFjYWViNjFjZThmNDhiOWFlY2ZkNDZkNDI5OGM2MmQiLCJ1c2VybmFtZSI6IjEyM0BxcS5jb20iLCJwZXJtaXNzaW9uIjoiciIsImFwcF9uYW1lIjoicnR5dSJ9.pUn_HtrNwISji0nOe0_-0b5JyXN0yEIwzhdIaju-8VE",    
    "dtable_uuid": "b1caeb61ce8f48b9aecfd46d4298c62d",
    "dtable_server": 'https://cloud.seatable.io/dtable-server/',
    "dtable_socket: 'https://cloud.seatable.io/'
}

```

With the **access token, dtable_uuid **and** dtable_server** information, you can call the APIs of [dtable-server](dtable-server)
