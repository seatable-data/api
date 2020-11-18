# Bases (DTables)

## Create a base

**POST **api/v2.1/dtables/

**Request parameters**

* owner: the ID of the owner (xxxx@auth.local) or a group ID
* name: name of dtable
* color: color of dtable, optional
* icon: icon of dtable, optional
* text_color: text_color of dtable, optional

**Sample request**

```
curl -X POST -d 'name=nice&owner=xxxx@auth.local&color=#7626FD&icon=icon-software-test-management' -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' "http://127.0.0.1:8000/api/v2.1/dtables/"

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
        "uuid": "747d0ded-2d55-4465-adbc-a74100e458a5",
        "color": "#7626FD",
        "text_color": null,
        "icon": "icon-software-test-management"
    }
}

```

**Errors**

* 400 Bad Request.
* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## Rename a base

**PUT **api/v2.1/workspace/\<workspace_id>/dtable/

**Request parameters**

* workspace_id
* name
* new_name

**Sample request**

```
curl -X PUT -d "name=hi&new_name=hey" -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' "http://127.0.0.1:8000/api/v2.1/workspace/1/dtable/"

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

## Delete a base

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

## Update a base

**PUT** /api/v2.1/:workspace_id/107/dtable/

**Request parameters**:

* **name**: table name, required
* **new_name**: new table name, optional
* **color**: table color, optional
* **text_color**: text color, optional
* **icon**: table icon, optional

**Request Sample**

```
curl --request PUT 'https://cloud.seatable.io/api/v2.1/workspace/107/dtable/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' --form 'name=for-email-put-3' --form 'color=red' --form 'text_color=blue'

```

**Response Sample**

```
{
    "table": {
        "id": 272,
        "workspace_id": 107,
        "uuid": "b29b244c-ea06-4846-a7b6-15d5dbdc4728",
        "name": "for-email-put-3",
        "creator": "admin",
        "modifier": "admin",
        "created_at": "2020-04-13T08:20:32+00:00",
        "updated_at": "2020-07-24T02:50:54+00:00",
        "color": "red",
        "text_color": "blue",
        "icon": null
    }
}

```

**Errors**

* 400 Bad Request.
* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.


