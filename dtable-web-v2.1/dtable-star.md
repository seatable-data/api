# Dtable Star

## Get Starred Bases

**GET** /api/v2.1/starred-dtables/

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/starred-dtables/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Sample Response (200)**

```
{
    "user_starred_dtable_list": [
        {
            "id": 278,
            "workspace_id": 107,
            "uuid": "00390415-b6dc-416a-8f2a-70a3a1356a18",
            "name": "for-add",
            "creator": "admin",
            "modifier": "admin",
            "created_at": "2020-04-15T08:42:36+00:00",
            "updated_at": "2020-04-17T07:06:39+00:00"
        },
        {
            "id": 239,
            "workspace_id": 103,
            "uuid": "60505783-d44e-44ab-872c-33e1a184db20",
            "name": "for-copy",
            "creator": "admin",
            "modifier": "admin",
            "created_at": "2020-04-08T02:27:59+00:00",
            "updated_at": "2020-04-08T02:27:59+00:00"
        }
    ]
}

```

## Add a Star to a Base

**POST** /api/v2.1/starred-dtables/

**Request Params**

* **dtable_uuid**: the uuid of the base, required

**Sample Request**

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/starred-dtables/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' --form 'dtable_uuid=00390415b6dc416a8f2a70a3a1356a18'

```

**Sample Response (200)**

```
{
    "success": true
}

```

## Delete Star of a Base

 **DELETE** /api/v2.1/starred-dtables/?dtable_uuid=\<dtable_uuid>

**Request Params**

* **dtable_uuid**: the uuid of the starred base, required

**Sample Request**

```
curl --request DELETE 'https://cloud.seatable.io/api/v2.1/starred-dtables/?dtable_uuid=00390415b6dc416a8f2a70a3a1356a18' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Sample Response (200)**

```
{
    "success": true
}

```


