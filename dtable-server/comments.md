# Comments

## Get Comments Count

**GET** /dtable-server/api/v1/dtables/:dtable_uuid/comments-count/

**request query params**

* **row_id**:  Row id, required

**request sample**

```
curl -X GET \
  'https://cloud.seatable.io/dtable-server/api/v1/dtables/a57b56d31cc54ebd8a6ca1b28ac3dbdf/comments-count/?row_id=289eb40b-cd25-47aa-b664-da35b4afa210' \
  -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' \
  -H 'cache-control: no-cache' \
  -H 'postman-token: fe1e4d7b-bfd2-7a24-1948-60df75fc6a90'

```

**response sample**

```
{
    "count": 1
}

```

**Errors**

* **400**: bad request
* **403**: permission denied
* **500**: internal server error

## List Comments

**GET** /dtable-server/api/v1/dtables/:dtable_uuid/comments/

**request query params**

* **page**: page number，default is 1, optional
* **per_page**: number of records per page, default i 10, optional
* **row_id**: row id, required

**request sample**

```
curl -X GET \
  'https://cloud.seatable.io/dtable-server/api/v1/dtables/a57b56d31cc54ebd8a6ca1b28ac3dbdf/comments/?page=1&count=10&row_id=289eb40b-cd25-47aa-b664-da35b4afa210' \
  -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' \
  -H 'cache-control: no-cache' \
  -H 'postman-token: 9afab10e-86f1-abb8-dc9d-0cb0f290cf10'

```

**response sample**

```
[
    {
        "id": 11,
        "author": "xiongchao.cheng@seafile.com",
        "comment": "test-comment-again-after-changing",
        "dtable_uuid": "a57b56d31cc54ebd8a6ca1b28ac3dbdf",
        "row_id": "289eb40b-cd25-47aa-b664-da35b4afa210",
        "created_at": "2019-12-12T01:06:52.013Z",
        "updated_at": "2019-12-12T01:06:52.013Z",
        "resolved": 0
    },
    {
        "id": 10,
        "author": "xiongchao.cheng@seafile.com",
        "comment": "test-comment-again-2",
        "dtable_uuid": "a57b56d31cc54ebd8a6ca1b28ac3dbdf",
        "row_id": "289eb40b-cd25-47aa-b664-da35b4afa210",
        "created_at": "2019-12-12T01:06:37.676Z",
        "updated_at": "2019-12-12T01:06:37.676Z",
        "resolved": 0
    }
]

```

**Errors**

* **400**: bad request
* **403**: permission denied
* **500**: internal server error

## Create a Comment

**POST** /dtable-server/api/v1/dtables/:dtable_uuid/comments/

**request query params**

* **row_id**: row id, required

**request json params**

* **comment**: comment content, required

**request sample**

```
curl -X POST \
  'https://cloud.seatable.io/dtable-server/api/v1/dtables/a57b56d31cc54ebd8a6ca1b28ac3dbdf/comments/?row_id=289eb40b-cd25-47aa-b664-da35b4afa210' \
  -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 532a7a07-74a1-db4b-4199-9f57193c891e' \
  -d '{
	"comment": "test-comment-again-after-changing"
}'

```

**response sample**

```
{
    "success": true
}

```

**Errors**

* **400**: bad request
* **403**: permission denied
* **500**: internal server error

## Update a Comment

**PUT** /dtable-server/api/v1/dtables/:dtable_uuid/comments/:comment_id/

**request json params**

* comment: new comment, optional
* resolved: set as resolved, optional

**request sample**

```
curl -X PUT \
  https://cloud.seatable.io/dtable-server/api/v1/dtables/a57b56d31cc54ebd8a6ca1b28ac3dbdf/comments/9/ \
  -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 65535e11-afe4-3870-e476-760dd54c771b' \
  -d '{
	"options": {
		"comment": "wowwwwwwww",
		"resolved": 1
	}
}'

```

**response sample**

```
{
    "success": true
}

```

**Errors**

* **400**: bad request
* **403**: permission denied
* **500**: internal server error

## Delete a Comment

**DELETE** /dtable-server/api/v1/dtables/:dtable_uuid/comments/:comment_id/

**request sample**

```
curl -X DELETE \
  https://cloud.seatable.io/dtable-server/api/v1/dtables/a57b56d31cc54ebd8a6ca1b28ac3dbdf/comments/7/ \
  -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' \
  -H 'cache-control: no-cache' \
  -H 'postman-token: 0eb3fafb-88cd-c41b-70b1-ff968a53c964'

```

**response sample**

```
{
    "success": true
}

```

**Errors**

* **400**: bad request
* **403**: permission denied
* **500**: internal server error

## Get Comment by ID

**GET** /dtable-server/api/v1/dtables/:dtable_uuid>/comments/:comment_id/

**request sample**

```
curl -X GET \
  https://cloud.seatable.io/dtable-server/api/v1/dtables/a57b56d31cc54ebd8a6ca1b28ac3dbdf/comments/8/ \
  -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' \
  -H 'cache-control: no-cache' \
  -H 'postman-token: 967ba77d-a72c-11c9-4ce9-a68ae7fd87b7'

```

**response sample**

```
{
    "id": 8,
    "author": "xiongchao.cheng@seafile.com",
    "dtable_uuid": "a57b56d31cc54ebd8a6ca1b28ac3dbdf",
    "row_id": "289eb40b-cd25-47aa-b664-da35b4afa210",
    "created_at": "2019-12-11T23:08:31.240Z",
    "updated_at": "2019-12-11T23:08:31.240Z",
    "resolved": 0
}

```

**Errors**

* **400**: bad request
* **403**: permission denied
* **500**: internal server error

## List Comments within Days

**GET** https\://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/comments-within-days/

**Request Parameters**

* days: the number of days that you will query comments within, default 3

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/dtable-server/api/v1/dtables/00390415b6dc416a8f2a70a3a1356a18/comments-within-days/?days=3' \
--header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1ODczNDk0NzQsImR0YWJsZV91dWlkIjoiMDAzOTA0MTViNmRjNDE2YThmMmE3MGEzYTEzNTZhMTgiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.BG55vZP0WMkM8cx_12aI-dNQiNp0l8kHlTqmErclX8Y'

```

**Sample Response**

```
{
    "comments": [
        {
            "id": 44,
            "author": "xiongchao.cheng@seafile.com",
            "comment": "4",
            "dtable_uuid": "00390415b6dc416a8f2a70a3a1356a18",
            "row_id": "U_eTV7mDSmSd-K2P535Wzw",
            "created_at": "2020-04-17T02:23:17.000Z",
            "updated_at": "2020-04-17T02:23:17.000Z",
            "resolved": 0
        },
        {
            "id": 43,
            "author": "xiongchao.cheng@seafile.com",
            "comment": "3",
            "dtable_uuid": "00390415b6dc416a8f2a70a3a1356a18",
            "row_id": "U_eTV7mDSmSd-K2P535Wzw",
            "created_at": "2020-04-17T02:23:16.000Z",
            "updated_at": "2020-04-17T02:23:16.000Z",
            "resolved": 0
        }
    ]
}

```

**Errors**

* **400**: Bad Request.
* **403**: Permission Denied.
* **404**: Not Found.
* **500**: Internal Server Error.




