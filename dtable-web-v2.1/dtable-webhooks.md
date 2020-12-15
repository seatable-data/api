# Webhooks

## List base webhooks

**GET** /api/v2.1/workspace/:workspace_id/dtable/:name/webhooks/

**Sample request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/workspace/107/dtable/for-add%20(2)/webhooks/' --header 'Authorization: Token 3120688f207383ba90e6160190ff70036d2e185d'

```

**Sample Response (200)**

```
{
    "webhook_list": [
        {
            "id": 2,
            "dtable_uuid": "626e40fa76304a4fb7641b71efab4795",
            "url": "http://127.0.0.1:5001",
            "creator": "xiongchao.cheng@seafile.com",
            "created_at": "2020-09-23T06:28:06.412738",
            "settings": {
                "secret": "wow"
            }
        },
        {
            "id": 12,
            "dtable_uuid": "626e40fa76304a4fb7641b71efab4795",
            "url": "http://127.0.0.1:5002",
            "creator": "xiongchao.cheng@seafile.com",
            "created_at": "2020-09-24T09:54:09.264397"
        }
    ]
}

```

## Create a base webhook

**POST** /api/v2.1/workspace/:workspace_id/dtable/:name/webhooks/

**Request params**:

* **url**: webhook's url, required
* **secret**: When you set a secret, you'll receive the X-SeaTable-Signature header in the webhook POST request. Its value is the result of hashing the secret key with SHA1 algorithm

**Sample request**

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/workspace/107/dtable/for-add%20(2)/webhooks/' --header 'Authorization: Token 3120688f207383ba90e6160190ff70036d2e185d' --form 'url=http://127.0.0.1:5004' --form 'secret=123'

```

**Sample Response (200)**

```
{
    "webhook": {
        "id": 15,
        "dtable_uuid": "626e40fa76304a4fb7641b71efab4795",
        "url": "http://127.0.0.1:5005",
        "creator": "xiongchao.cheng@seafile.com",
        "created_at": "2020-09-24T10:10:59.473003",
        "settings": {
            "secret": "123"
        }
    }
}

```

## Update a base webhook

**PUT** /api/v2.1/workspace/:workspace_id/dtable/:name/webhooks/:webhook_id/

**Request params**:

* **url**: webhook's url, required
* **secret**: When you set a secret, you'll receive the X-SeaTable-Signature header in the webhook POST request. Its value is the result of hashing the secret key with SHA1 algorithm

**Sample request**

```
curl --request PUT 'https://cloud.seatable.io/api/v2.1/workspace/107/dtable/for-add%20(2)/webhooks/15/' --header 'Authorization: Token 3120688f207383ba90e6160190ff70036d2e185d' --form 'url=http://127.0.0.1:5005' --form 'secret=456'

```

**Sample Response (200)**

```
{
    "webhook": {
        "id": 15,
        "dtable_uuid": "626e40fa76304a4fb7641b71efab4795",
        "url": "http://127.0.0.1:5005",
        "creator": "xiongchao.cheng@seafile.com",
        "created_at": "2020-09-24T10:10:59.473003",
        "settings": {
            "secret": "456"
        }
    }
}

```

## Delete a base webhook

**DELETE** /api/v2.1/workspace/:workspace_id/dtable/:name/webhooks/:webhook_id/

**Sample request**

```
curl --request DELETE 'https://cloud.seatable.io/api/v2.1/workspace/107/dtable/for-add%20(2)/webhooks/15/' --header 'Authorization: Token 3120688f207383ba90e6160190ff70036d2e185d'

```

**Sample Response (200)**

```
200 OK

```


