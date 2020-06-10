# Collaborators

## List collaborators of a table

**GET** /api/v1/dtables/:dtable_uuid/related-users/

**Sample request**

```
curl -X GET https://cloud.seatable.io/dtable-server/api/v1/dtable/ff977dc8f06546729d489defd64cfe8f/related-users/ \
  -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg1NjUzMzUsImR0YWJsZV91dWlkIjoiZmY5NzdkYzhmMDY1NDY3MjlkNDg5ZGVmZDY0Y2ZlOGYiLCJ1c2VybmFtZSI6ImFkbWluQHNlYWZpbGV0ZXN0LmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.7j3nTzViP9LxINGIxf9YR8KyWs633DHRW7SyfXvOF7Y'

```

**Sample response**

```
{
    "user_list": [
        {
            "email": "admin@seafiletest.com",
            "name": "admin",
            "contact_email": "admin@seafiletest.com",
            "avatar_url": "http://127.0.0.1:8000/media/avatars/f/c/306ab43564752a999eecb57cabcefe/resized/80/e9d4953412684d3eccf7eaed805541f1_WuoaewF.png"
        }
    ]
}

```

**Errors**:

* 403 Permission denied
* 500 Internal Server Error


