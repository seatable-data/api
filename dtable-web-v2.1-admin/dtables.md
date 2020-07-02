# DTables

## List All DTables

**GET **api/v2.1/admin/dtables/

**Sample request**

```
curl -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' "http://127.0.0.1:8000/api/v2.1/admin/dtables/?page=1&per_page=100"

```

**Sample response**

```
{
    "page_info": {
        "has_next_page": false,
        "current_page": 1
    },
    "dtables": [
        {
            "id": 1,
            "workspace_id": 1,
            "uuid": "251d501a-4492-4c17-97e1-c7bc64d87d13",
            "name": "t1",
            "creator": "123",
            "modifier": "123",
            "created_at": "2019-10-18T08:28:27+00:00",
            "updated_at": "2019-10-18T08:28:27+00:00"
        },
        {
            "id": 2,
            "workspace_id": 1,
            "uuid": "3cc5aff5-d4ca-488b-9ccd-9758b624cbd8",
            "name": "t2",
            "creator": "123",
            "modifier": "123",
            "created_at": "2019-10-18T08:54:06+00:00",
            "updated_at": "2019-10-18T08:54:06+00:00"
        },
        {
            "id": 7,
            "workspace_id": 2,
            "uuid": "52a2ae0d-d675-4a42-8e89-b14bfd0f4118",
            "name": "gt-1",
            "creator": "123",
            "modifier": "123",
            "created_at": "2019-10-21T07:14:32+00:00",
            "updated_at": "2019-10-21T07:14:32+00:00"
        }
    ]
}

```

**Errors**

* 403 Permission Denied.
* 500 Internal Server Error.

## List User's DTables

**GET** /api/v2.1/admin/users/:email/dtables/

**Request Params**

* **page**: the number of page to list, default 1, optional
* **per_page**: the number of tables per page, default 25, optional

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/admin/users/xiongchao.cheng%40seafile.com/dtables/?page=2' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Sample Response**

```
{
    "dtable_list": [
        {
            "id": 371,
            "workspace_id": 107,
            "uuid": "d091825a-960f-42ce-a7b4-4273cb114f07",
            "name": "for-add-restore-15",
            "creator": "admin",
            "modifier": "admin",
            "created_at": "2020-06-23T02:18:39+00:00",
            "updated_at": "2020-06-23T02:18:39+00:00",
            "rows_count": 0
        }
    ],
    "count": 34
}

```

## List Organization DTables

**GET** /api/v2.1/admin/organizations/:org_id/dtables/

**Request Params:**

* **page**: the number of page to list, default 1, optional
* **per_page**: the number of tables per page, default 25, optional

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/admin/organizations/23/dtables/?page=2&per_page=3' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Sample Response**

```
{
    "dtable_list": [
        {
            "id": 276,
            "workspace_id": 109,
            "uuid": "24fdb4a5-282e-41f2-9724-5d9b41199694",
            "name": "for-delete-restore",
            "creator": "org~4-admin-1",
            "modifier": "org~4-admin-1",
            "created_at": "2020-04-14T07:15:13+00:00",
            "updated_at": "2020-04-14T07:15:13+00:00",
            "rows_count": 0
        }
    ],
    "count": 6
}

```

## List Trash DTables

**GET** /api/v2.1/admin/trash-dtables/

**Request query params**

* **per_page**: number of dtables in per page response, default 25
* **page**: which page default 1

**Request Sample**

```
curl -X GET 'https://cloud.seatable.io/api/v2.1/admin/trash-dtables/?per_page=25&page=1' \
  -H 'authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Response Sample**

```
{
    "count": 1,
    "trash_dtable_list": [
        {
            "id": 30,
            "workspace_id": 56,
            "uuid": "52394e1a-05a5-4a90-afe0-cea0555c1e91",
            "name": "for-delete",
            "creator": "Big Boss",
            "modifier": "Big Boss",
            "created_at": "2020-02-18T03:35:57+00:00",
            "updated_at": "2020-02-18T03:35:57+00:00",
            "deleted": true,
            "delete_time": "2020-02-18T03:40:48.082457"
        }
    ]
}

```

**Errors**

* **400**: Bad Request
* **403**: Permission denied
* **500**: Internal Server Error

## Restore a Trash DTable

**PUT** /api/v2.1/admin/trash-dtables/:dtable_id/

**Request Sample**

```
curl -X PUT 'https://cloud.seatable.io/api/v2.1/admin/trash-dtables/30/' \
  -H 'authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Response Sample**

```
{
    "success": true
}

```

**Errors**

* **400**: Bad Request
* **403**: Permission denied
* **500**: Internal Server Error


