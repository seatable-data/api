# Dtable share to group

## List All DTables Shares to All Groups Which I am in

**GET** api/v2.1/dtables/group-shared/

**Request Sample**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/dtables/group-shared/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Response Sample**

```
{
    "group_shared_dtables": {
        "64": [  // group_id
            {
                "id": 239,
                "workspace_id": 103,
                "uuid": "60505783-d44e-44ab-872c-33e1a184db20",
                "name": "for-copy",
                "creator": "成雄超",
                "modifier": "成雄超",
                "created_at": "2020-04-08T02:27:59+00:00",
                "updated_at": "2020-04-08T02:27:59+00:00"
            },
            {
                "id": 249,
                "workspace_id": 103,
                "uuid": "fd82617b-619d-49f6-8566-c5f4eb98dbc3",
                "name": "for-copy-3",
                "creator": "成雄超",
                "modifier": "成雄超",
                "created_at": "2020-04-08T02:40:22+00:00",
                "updated_at": "2020-04-08T02:40:22+00:00"
            }
        ]
    }
}

```

**Errors**

* **500**: Internal Server Error.

## Add a DTable Share to Group

**POST** api/v2.1/workspace/:workspace_id/dtable/:name/group-shares/

**Request Params**

* **group_id**: which group you will share to, required
* **permission**: share permission, there are options `r` `rw` means read-only and read-write, required

**Request Sample**

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/workspace/103/dtable/for-group-share/group-shares/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' --form 'group_id=64' --form 'permission=r'

```

**Response Sample**

```
{
    "dtable_group_share": {
        "group_id": "64",
        "group_name": "after-delete-2",
        "permission": "r"
    }
}

```

**Errors**

* **403**: Permission Denied.
* **404**: Not Found.
* **500**: Internal Server Error.

## Update a DTable Share Permission to Group

**PUT** api/v2.1/workspace/:workspace_id/dtable/:name/group-shares/:group_id/

**Request Params**

* **permission**: share permission, there are options `r` `rw` means read-only and read-write, required

**Request Sample**

```
curl --location --request PUT 'https://cloud.seatable.io/api/v2.1/workspace/103/dtable/for-copy-4/group-shares/64/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' --form 'permission=rw'

```

**Response Sample**

```
{
    "success": true
}

```

**Errors**

* **403**: Permission Denied.
* **404**: Not Found.
* **500**: Internal Server Error.

## List a DTable Shares to Groups

**GET** api/v2.1/workspace/:workspace_id/dtable/:name/group-shares/

**Request Sample**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/workspace/103/dtable/for-copy/group-shares/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Response Sample**

```
{
    "dtable_group_shares": [
        {
            "group_id": 64,
            "group_name": "after-delete-2",
            "permission": "rw"
        }
    ]
}

```

**Errors**

* **403**: Permission Denied.
* **404**: Not Found.
* **500**: Internal Server Error.

## Delete a DTable Share to Group

**DELETE** api/v2.1/workspace/:workspace_id/dtable/:name/group-shares/:group_id/

**Request Sample**

```
curl --request DELETE 'https://cloud.seatable.io/api/v2.1/workspace/103/dtable/for-copy-4/group-shares/64/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Response Sample**

```
{
    "success": true
}

```

**Errors**

* **403**: Permission Denied.
* **404**: Not Found.
* **500**: Internal Server Error.


