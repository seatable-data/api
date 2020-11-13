# Access Token

## Get a DTable Access Token

**GET** /api/v2.1/workspace/:workspace_id/dtable/:name/access-token/

**Sample request**

```
curl -H 'Authorization: Token 57782e1e42a7fefc6a5026e00c6a62c9d249e760' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/hello/access-token/"

```

**Sample response**

```
{
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkdGFibGVfdXVpZCI6IjIwMDRjZWIzZDQyZDRiMDI5YTkzYjFkOWEwOWQxZTYxIiwiZXhwIjoxNTY1NTg5NjI5fQ.PdzbZKoEFQ2zONPwX9ouMdzM4GAzD5xAhxtGkmr4P9M",
    "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60"
}

```

**Errors**

* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## Get a DTable Access Token via Share Link

**GET** /api/v2.1/dtable/share-link-access-token/

**Sample request**

```
curl -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/dtable/share-link-access-token/?token=d64ec2886e9e45b696d9"

```

**Sample response**

```
{
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkdGFibGVfdXVpZCI6IjIwMDRjZWIzZDQyZDRiMDI5YTkzYjFkOWEwOWQxZTYxIiwiZXhwIjoxNTY1NTg5NjI5fQ.PdzbZKoEFQ2zONPwX9ouMdzM4GAzD5xAhxtGkmr4P9M",
    "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60"
}

```

**Errors**

* 400 Bad Request.
* 403 Permission Denied.
* 500 Internal Server Error.


