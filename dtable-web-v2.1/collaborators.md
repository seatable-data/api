# Collaborators

## List Collaborators of a DTable

**GET** api/v2.1/workspace/\<workspace_id>/dtable/\<name>/related-users/

**Sample request**

```
curl -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' 
-H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8000/api/v2.1/workspace/<workspace_id>/dtable/<name>/related-users/"

```

**Sample response**

```
{
    "user_list": [
        {
            "avatar_url": "http://127.0.0.1:8000/media/avatars/default.png",
            "contact_email": "tony@seafile.com",
            "email": "tony@seafile.com",
            "name": "tony"
        },
        {
            "avatar_url": "http://127.0.0.1:8000/media/avatars/default.png",
            "contact_email": "jason@seafile.com",
            "email": "jason@seafile.com",
            "name": "jason"
        }
    ]
}

```

**Errors**

* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.


