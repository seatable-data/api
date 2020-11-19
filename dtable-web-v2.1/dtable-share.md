# DTable Share

## List Bases Shared to me

**GET** /api/v2.1/dtables/shared/

**Sample request**

```
curl -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8000/api/v2.1/dtables/shared/"

```

**Sample response**

```
{
    "table_list": [
        {
            "workspace_id": 3,
            "uuid": "7847ab38-c5c5-4259-8515-eaa1b977b686",
            "creator": "456",
            "created_at": "2019-06-26T03:06:51+00:00",
            "permission": "rw",
            "updated_at": "2019-06-29T04:03:00+00:00",
            "from_user_name": "456",
            "from_user_type": "Group",
            "from_user": "456@qq.com",
            "modifier": "123",
            "id": 4,
            "name": "test4567"
        },
        {
            "workspace_id": 4,
            "uuid": "3944abb8-148a-4d0c-a1f9-596d772cf921",
            "creator": "789",
            "created_at": "2019-06-29T04:11:25+00:00",
            "permission": "rw",
            "updated_at": "2019-06-29T04:11:25+00:00",
            "from_user_name": "789",
            "from_user_type": "Personal",
            "from_user": "789@qq.com",
            "modifier": "789",
            "id": 10,
            "name": "from_7890"
        }
    ]
}

```

**Errors**

* 500 Internal Server Error.

## List Users Sharing a Base

**GET** /api/v2.1/workspace/\<workspace_id>/dtable/\<name>/share/

**Request parameters**

* **workspace_id**
* **name** of the base

**Sample request**

```
curl -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8000/api/v2.1/workspace/12/dtable/test/share/"

```

**Sample response**

```
{
    "user_list": [
        {
            "permission": "rw",
            "avatar_url": "http://127.0.0.1:8000/media/avatars/1/e/6fd8e56879c84999cd481255530592/resized/80/6380b959064ee3f947fb2676836dd2a4.png",
            "contact_email": "2@2.com",
            "email": "2@2.com",
            "name": "two"
        }
    ]
}

```

**Errors**

* 404 NOT FOUND.
* 403 PERMISSION DENIED.
* 500 Internal Server Error.

## Share a Base to Another User in the Organization

**POST** /api/v2.1/workspace/\<workspace_id>/dtable/\<name>/share/

**Request parameters**

* **workspace_id**
* **name** of the base
* **permission**, share permission, with the options `r` and `rw` meaning read-only and read-write, required
* **email **is not the contact email, but the user's ID ending with @auth.local

**Sample request**

```
curl -X POST -d "permission=rw&email=2436ce64315b4b4azfcff9e5491db296@auth.local" -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8000/api/v2.1/workspace/12/dtable/test/share/"

```

**Sample response**

```
{
    "success":true
}

```

**Errors**

* 400 BAD REQUEST
* 404 NOT FOUND.
* 403 PERMISSION DENIED.
* 409 CONFLICT.
* 500 Internal Server Error.

## Update a Base's Sharing Permission to a User

**PUT** /api/v2.1/workspace/\<workspace_id>/dtable/\<name>/share/

**Request parameters**

* **workspace_id**
* **name** of the base
* **permission**, share permission, with the options `r` and `rw` meaning read-only and read-write, required
* **email **is not the contact email, but the user's ID ending with @auth.local

**Sample request**

```
curl -X PUT -d "permission=r&email=2@2.com" -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8000/api/v2.1/workspace/12/dtable/test/share/"

```

**Sample response**

```
{
    "success":true
}

```

**Errors**

* 400 BAD REQUEST
* 404 NOT FOUND.
* 403 PERMISSION DENIED.
* 500 Internal Server Error.

## Cancel a Base's Share to a User

**DELETE** /api/v2.1/workspace/\<workspace_id>/dtable/\<name>/share/

**Request parameters**

* **workspace_id**
* **name** of the base
* **email **is not the contact email, but the user's ID ending with @auth.local

**Sample request**

```
curl -X DELETE -d "email=2436ce64315b4b4azfcff9e5491db296@auth.local" -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8000/api/v2.1/workspace/12/dtable/test/share/"

```

**Sample response**

```
{
    "success":true
}

```

**Errors**

* 400 BAD REQUEST
* 404 NOT FOUND.
* 403 PERMISSION DENIED.
* 500 Internal Server Error.


