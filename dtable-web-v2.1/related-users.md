# Related Users

## Get user list by user id list

**GET **api/v2.1/user-list/

**Request Parameters**

* user_id_list

**Sample request**

```
curl -X POST -H 'Authorization:Token e1518ab0624eed78ab9456d207e312666fcaf748' -H 'Content-type: application/json' -d '{
    "user_id_list": [
        "5758ecdce3e741ad81293a304b6d3388@auth.local",
        "5ed78cb2cd264b0e8c400f131bc5c4c8@auth.local"
    ]
}' -H 'Accept: application/json; indent=4' "https://cloud.seatable.io/dtable-web/api/v2.1/user-list/"

```

**Sample Response (200)**

```json
{
    "user_list": [
        {
            "email": "5758ecdce3e741ad81293a304b6d3388@auth.local",
            "name": "Alex",
            "contact_email": "1@1.com",
            "avatar_url": "http://127.0.0.1:8000/media/avatars/0/4/8f833bd2e242f195f40a77c21b39b6/resized/80/03e77af8819c66f25260297dd5e97dc7_uawl0f1.png"
        },
        {
            "email": "5ed78cb2cd264b0e8c400f131bc5c4c8@auth.local",
            "name": "Bob",
            "contact_email": "2@2.com",
            "avatar_url": "http://127.0.0.1:8000/media/avatars/4/8/8da703fbbf61f4c398943c609924c0/resized/80/1ae78cb64ba5442c2929247926af0e6f.png"
        }
    ]
}

```

**Errors**

* 400 Bad Request.
* 500 Internal Server Error.


