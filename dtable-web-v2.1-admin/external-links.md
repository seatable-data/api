# External Links

## List All External Links

**GET **api/v2.1/admin/dtables/

**Request parameters**

* per_page, default is 25
* page, default is 1

**Sample request**

```
curl -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' "https://cloud.seatable.io/api/v2.1/admin/external-links/?per_page=25&page=1"

```

**Sample response**

```
{
    "has_next_page": false,
    "external_link_list": [
        {
            "id": 3,
            "from_dtable": "t1",
            "creator": "6f46581085834012abc0ad20a5e85b8a@auth.local",
            "creator_name": "a",
            "token": "acbdef3e30a3404084b6",
            "permission": "r",
            "create_at": "2020-02-28T08:03:36+00:00"
        },
        {
            "id": 20,
            "from_dtable": "tt",
            "creator": "1c85431b78144701962e7ba04b0a8bd3@auth.local",
            "creator_name": "b",
            "token": "b755207356374b6e8b4d",
            "permission": "r",
            "create_at": "2020-03-23T09:19:10+00:00"
        }
    ]
}

```

**Errors**

* 403 Permission Denied.
* 500 Internal Server Error.

## Delete An External Link By Token

**DELETE **api/v2.1/admin/dtables/:token/

**Sample request**

```
curl -X DELETE -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' "https://cloud.seatable.io/api/v2.1/admin/external-links/acbdef3e30a3404084b6/"

```

**Sample response**

```
{
    "success": true
}

```

**Errors**

* 403 Permission Denied.
* 500 Internal Server Error.


