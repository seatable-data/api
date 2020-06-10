# DTables

## Create a DTable

**POST **api/v2.1/dtables/

**Request parameters**

* owner
* name: personal or a group id

**Sample request**

```
curl -X POST -d 'name=nice&owner=1@1.com' -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' "http://127.0.0.1:8000/api/v2.1/dtables/"

```

**Sample response**

```
{
    "table": {
        "workspace_id": 1,
        "name": "nice",
        "creator": "one",
        "updated_at": "2019-06-25T07:51:55+00:00",
        "created_at": "2019-06-25T07:51:55+00:00",
        "modifier": "one",
        "id": 6,
        "uuid": "747d0ded-2d55-4465-adbc-a74100e458a5"
    }
}

```

**Errors**

* 400 Bad Request.
* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## Rename a DTable

**PUT **api/v2.1/workspace/\<workspace_id>/dtable/

**Request parameters**

* workspace_id
* old_name
* new_name

**Sample request**

```
curl -X PUT -d "old_name=hi&new_name=hey" -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' "http://127.0.0.1:8000/api/v2.1/workspace/1/dtable/"

```

**Sample response**

```
{
    "table": {
        "modifier": "one",
        "name": "hey",
        "mtime": "2019-06-24T10:12:44+00:00"
    }
}

```

**Errors**

* 400 Bad Request.
* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## Delete a DTable

**DELETE **api/v2.1/workspace/\<workspace_id>/dtable/

**Request parameters**

* workspace_id
* name

**Sample request**

```
curl -X DELETE -d "name=dtable_2" -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' "http://127.0.0.1:8000/api/v2.1/workspace/1/dtable/"

```

**Sample response**

```
{
    "success": "true"
}

```

**Errors**

* 400 Bad Request.
* 403 Permission Denied.
* 404 Not Found.
* 500 Internal Server Error.

