# Org admin dtables

## List DTables

**GET** api/v2.1/org/:org_id/admin/dtables/

**Request Params**

* **page**: default 1, optional
* **per_page**: default 25, optional

**Request Sample**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/org/23/admin/dtables/?page=1&per_page=1' --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6'

```

**Response Sample**

```
{
    "dtable_list": [
        {
            "id": 230,
            "workspace_id": 98,
            "uuid": "64fab82d-c0e8-485d-a63c-b82652211e4a",
            "name": "for-quota",
            "creator": "org~4-admin-1",
            "modifier": "org~4-admin-1",
            "created_at": "2020-03-28T09:41:08+00:00",
            "updated_at": "2020-03-28T09:43:33+00:00"
        }
    ],
    "count": 4
}

```

**Errors**

* **400 **Bad Request**.**
* **404** Not Found.
* **403** Permission Denied.
* **500** Internal Server Error.

## Delete a DTable

**DELETE** api/v2.1/org/:org_id/admin/dtables/:dtable_id/

**Request Sample**

```
curl --request DELETE 'https://cloud.seatable.io/api/v2.1/org/23/admin/dtables/277/' --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6'

```

**Response Sample**

```
{
    "success": true
}

```

**Errors**

* **400 **Bad Request**.**
* **404** Not Found.
* **403** Permission Denied.
* **500** Internal Server Error.

## List Trash DTables

**GET** api/v2.1/org/:org_id/admin/trash-dtables/

**Request Params**

* **page**: default 1, optional
* **per_page**: default 25, optional

**Request Sample**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/org/23/admin/trash-dtables/?page=1&per_page=1' --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6'

```

**Response Sample**

```
{
    "dtable_list": [
        {
            "id": 271,
            "workspace_id": 106,
            "uuid": "cd5f54a9-4323-4bf2-9ef8-b58d05851859",
            "name": "for-delete-store",
            "creator": "org~4-admin-1",
            "modifier": "org~4-admin-1",
            "created_at": "2020-04-13T06:20:41+00:00",
            "updated_at": "2020-04-13T06:20:41+00:00",
            "deleted": true,
            "delete_time": "2020-04-14T06:47:27.784759"
        }
    ],
    "count": 5
}

```

**Errors**

* **400 **Bad Request**.**
* **404** Not Found.
* **403** Permission Denied.
* **500** Internal Server Error.

## Restore a DTable

**PUT** api/v2.1/org/:org_id/admin/trash-dtables/:dtable_id/

**Request Sample**

```
curl --request PUT 'https://cloud.seatable.io/api/v2.1/org/23/admin/trash-dtables/277/' --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6'

```

**Response Sample**

```
{
    "success": true
}

```

**Errors**

* **400 **Bad Request**.**
* **404** Not Found.
* **403** Permission Denied.
* **500** Internal Server Error.


