# DTable API Token

## Create a DTable API Token

**POST** /api/v2.1/workspace/:workspace_id/dtable/:name/api-tokens/

**Sample request**

```
curl -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8000/api/v2.1/workspace/1/dtable/test/api-tokens/"
-X POST -d "app_name=gmail&permission=rw"

```

**Sample response**

```
{
    "app_name": "gmail",
    "api_token": "d66f83fccd0299f0dfe70e1ca807f05921f2de5f",
    "generated_by": "123@qq.com",
    "generated_at": "2019-09-19T02:41:53+00:00",
    "last_access": "2019-09-19T03:56:13+00:00",
    "permission": "rw"
}

```

**Errors**

* 400 bad request.
* 404 not found.
* 403 permission denied.
* 500 Internal Server Error.

## List DTable API Tokens

**GET** /api/v2.1/workspace/:workspace_id/dtable/:name/api-tokens/

**Sample request**

```
curl -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/test/api-tokens/"

```

**Sample response**

```
{
    "api_tokens": [
        {
            "app_name": "gmail",
            "api_token": "d66f83fccd0299f0dfe70e1ca807f05921f2de5f",
            "generated_by": "123@qq.com",
            "generated_at": "2019-09-19T02:41:53+00:00",
            "last_access": "2019-09-19T03:56:13+00:00",
            "permission": "rw"
        },
        {
            "app_name": "mail",
            "api_token": "4351cacae2c504e6a8ce5a75e95ae769629a70a2",
            "generated_by": "123@qq.com",
            "generated_at": "2019-09-19T03:01:58+00:00",
            "last_access": "2019-09-19T03:01:58+00:00",
            "permission": "rw"
        }
    ]
}

```

**Errors**

* 400 bad request.
* 404 not found.
* 403 permission denied.
* 500 Internal Server Error.

## Update DTable API Token

**PUT** /api/v2.1/workspace/:workspace_id/dtable/:name/api-tokens/:app_name/

**Sample request**

```
curl -X PUT -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/test/api-tokens/gmail/ -d "permission=r"

```

**Sample response**

```
{
    "app_name": "gmail",
    "api_token": "d66f83fccd0299f0dfe70e1ca807f05921f2de5f",
    "generated_by": "123@qq.com",
    "generated_at": "2019-09-19T02:41:53+00:00",
    "last_access": "2019-09-19T03:56:13+00:00",
    "permission": "r"
}

```

**Errors**

* 400 bad request.
* 404 not found.
* 403 permission denied.
* 500 Internal Server Error.

## Delete a DTable API Token

**DELETE** /api/v2.1/workspace/:workspace_id/dtable/:name/api-tokens/:app_Name/

**Sample request**

```
curl -X DELETE -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/test/api-tokens/gmail/

```

**Sample response**

```
{"success": true}

```

**Errors**

* 400 bad request.
* 404 not found.
* 403 permission denied.
* 500 Internal Server Error.

## Get JWT Token by DTable API Token

**GET** /api/v2.1/dtable/app-access-token/

**Sample request**

```
curl -H 'Accept: application/json; charset=utf-8; indent=4' 
'Authorization: Token 8g971000df0d6fbntc59580766329a5b37adfh'
"https://cloud.seatable.io/api/v2.1/dtables/app-access-token/"

```

**Sample response**

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjkyMjYxNzEsImR0YWJsZV91dWlkIjoiYjFjYWViNjFjZThmNDhiOWFlY2ZkNDZkNDI5OGM2MmQiLCJ1c2VybmFtZSI6IjEyM0BxcS5jb20iLCJwZXJtaXNzaW9uIjoiciIsImFwcF9uYW1lIjoicnR5dSJ9.pUn_HtrNwISji0nOe0_-0b5JyXN0yEIwzhdIaju-8VE",
    "dtable_uuid": "b1caeb61ce8f48b9aecfd46d4298c62d"
    "dtable_server": 'https://cloud.seatable.io/dtable-server/',
    "dtable_socket: 'https://cloud.seatable.io/'
}

```

**Errors**

* 400 bad request.
* 404 not found.
* 403 permission denied.
* 500 Internal Server Error.

## Get File Upload Link by API Token

**GET **/api/v2.1/dtable/app-upload-link/

* workspace_id
* name

**Sample request**

```
curl -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' -H 'Accept: application/json; indent=4' "https://cloud.seatable.io/api/v2.1/dtable/app-upload-link/"

```

**Sample response**

```
{
    "upload_link": "https://cloud.seatable.io/seafhttp/upload-api/047537b8-833d-4c05-bf5e-4ddbe8e408e3",
    "parent_path": "/asset/5a40dd8e-59b7-49ff-84a7-3c9fb8a0cf60"
}

```

**Errors**

* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## Get File Download Link by API Token

**GET **/api/v2.1/dtable/app-download-link/

* path, asset path inside /asset/dtable_uuid/ folder

**Sample request**

```
curl -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' -H 'Accept: application/json; indent=4' "https://cloud.seatable.io/api/v2.1/dtable/app-download-link/?path=/images/2020-02/test_pic.jpg"

```

**Sample response**

```
{
    "download_link": "https://cloud.seatable.io/seafhttp/files/498fe8b6-68f4-4878-8ce7-91517b9c6e1c/test_pic.jpg"
}

```

**Errors**

* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## List DTable API Tokens Status

**GET** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/api-tokens-status/

**Request Sample**

```
curl -H 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' -H 'Accept: application/json; indent=4' 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/for-license/api-tokens-status/' 

```

**Response Sample**

```
{
    "app_status": [
        {
            "app_name": "app-1",
            "connected": true,
            "last_access": "2020-03-18T02:14:53.587149"
        },
        {
            "app_name": "app-2",
            "connected": false,
            "last_access": "2020-03-18T02:14:53.587149"
        }
    ]
}

```

**Errors**

* **400 **Bad Request**.**
* **404** Not Found.
* **403** Permission Denied.
* **500** Internal Server Error.


