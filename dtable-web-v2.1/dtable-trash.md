# DTable trash

## List trash dtables

**GET** api/v2.1/trash-dtables/

**Request Sample**

```
curl https://cloud.seatable.io/api/v2.1/trash-dtables/ --header 'Authorization: Token 788fe6cf0776feb46f311f014587105e7a4f7089' 

```

**Response Sample**

```
{
    "count": 1,
    "trash_dtable_list": [
        {
            "id": 32,
            "workspace_id": 20,
            "uuid": "123aca9c-1cd1-4556-a00c-36546644f9be",
            "name": "customer_test_2",
            "creator": "ranjiwei",
            "modifier": "ranjiwei",
            "created_at": "2020-11-27T02:23:04+00:00",
            "updated_at": "2020-11-27T02:23:04+00:00",
            "color": null,
            "text_color": null,
            "icon": null,
            "deleted": true,
            "delete_time": "2020-11-30T05:36:54+00:00"
        },
    ]
}

```

## Restore trash dtable

**PUT** api/v2.1/trash-dtables/:dtable_id/

**Request parameters**

* **dtable_id**

**Request Sample**

```
curl -X PUT https://cloud.seatable.io/api/v2.1/trash-dtables/32/ --header 'Authorization: Token 788fe6cf0776feb46f311f014587105e7a4f7089' 

```

**Response Sample**

```
{
    "success": true,
}

```


