# Dtable Asset

## DTable Asset Exists

**GET** /api/v2.1/workspace/:workspace_id/dtable/:name/asset-exists/

**Request Parameters**

* wordspace_id
* name
* path

**Sample request**

```
curl -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.com/api/v2.1/workspace/1/dtable/t1/asset-exists/?path=files/2020-04/apple.png"

```

**Sample response**

```
{
    "is_exist": true
}

```

**Errors**

* 403 permission denied.
* 404 not found.
* 500 Internal Server Error.


