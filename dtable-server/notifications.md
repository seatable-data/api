# Notifications

## List notifications

**GET** /api/v1/dtables/:dtable_uuid/notifications/

**Request Parameters**

* **dtable_uuid**
* **page**: page number, default 1, optional
* **per_page**: number of notifications per page, default 25, optional

**Sample Request**

```
curl -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' "https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aaedbc14325a8901c2e79ea5319/notifications/"

```

**Sample Response**

```
{
    "notification_list": [
        {
            "id": 2,
            "username": "1@1.com",
            "msg_type": "row_comment",
            "created_at": "2020-01-11T03:50:37.000Z",
            "detail": {
                "author": "2@2.com",
                "table_id": "0000",
                "row_id": "NqXZP3YyTyCBOlPf5RNvWQ",
                "comment": "nice"
            },
            "seen": 1
        }
    ]
}

```

**Errors**

* **400**: Bad Request
* **403**: Permission Denied
* **404**: Not Found
* **500**: Internal Server Error

## Add a notification

**POST** /api/v1/dtables/:dtable_uuid/notifications/

**Request Parameters**

* **dtable_uuid**
* **to_user**
* **msg_type**
* **detail**

**Sample Request**

```
curl -X POST -d '{
	"to_user": "1@1.com",
	"msg_type": "row_comment",
	"detail": {"author": "2@2.com", "row_id": "NqXZP3YyTyCBOlPf5RNvWQ", "comment": "world"}
}' -H 'Content-type: application/json' -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' "https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aaedbc14325a8901c2e79ea5319/notifications/"

```

**Sample Response**

```
{
    "success": true
}

```

**Errors**

* **400**: Bad Request
* **403**: Permission Denied
* **404**: Not Found
* **500**: Internal Server Error

## Mark all notifications

**PUT** /api/v1/dtables/:dtable_uuid/notifications/

**Request Parameters**

* **dtable_uuid**
* **seen**: true or false, otherwise invalid

**Sample Request**

```
curl -X PUT -d 'seen=true' -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' "https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aaedbc14325a8901c2e79ea5319/notifications/"

```

**Sample Response**

```
{
    "success": true
}

```

**Errors**

* **400**: Bad Request
* **403**: Permission Denied
* **404**: Not Found
* **500**: Internal Server Error

## Mark a notification

**PUT** /api/v1/dtables/:dtable_uuid/notifications/:notification_id/

**Request Parameters**

* **dtable_uuid**
* **notification_id**
* **seen**: true or false, otherwise invalid

**Sample Request**

```
curl -X PUT -d 'seen=true' -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' "https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aaedbc14325a8901c2e79ea5319/notifications/2/"

```

**Sample Response**

```
{
    "success": true
}

```

**Errors**

* **400**: Bad Request
* **403**: Permission Denied
* **404**: Not Found
* **500**: Internal Server Error

## Clear notifications

**DELETE** /api/v1/dtables/:dtable_uuid/notifications/

**Request Parameters**

* **dtable_uuid**

**Sample Request**

```
curl -X DELETE -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' "https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aaedbc14325a8901c2e79ea5319/notifications/"

```

**Sample Response**

```
{
    "success": true
}

```

**Errors**

* **400**: Bad Request
* **403**: Permission Denied
* **404**: Not Found
* **500**: Internal Server Error


