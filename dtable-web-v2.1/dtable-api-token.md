# Base API Token Operations

## Create A Base API Token

This API request creates a base's API token with read-only (`r`) or read & write (`rw`) permission.



**URL Structure**

> **\[POST]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/api-tokens/


**Request Authentication**

> User Authentication (Token)

**Sample Request**

Create a read & write API token "Google" for the base `Test` in the workspace `1`:


> ```
> curl -X POST \
> -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "http://cloud.seatable.io/api/v2.1/workspace/1/dtable/Test/api-tokens/" \
> -d "app_name=Google&permission=rw"
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the target base is stored.

**name** _\[string, required]_
> The name of the target base.

**app_name** _\[string, required]_
> The name of the App to be connected to this API.

**permission** _\[string(`r` or `rw`), required]_
> Set the permission: `r` for read-only and `rw` for read & write.


**Return Values**

JSON-object with the API token and other details.



**Sample Response (201)**

The desired API token has been created:

> ```
> {
>     "app_name": "Google",
>     "api_token": "d66f83fccd0299f0dfe70e1ca807f05921f2de5f",
>     "generated_by": "12345cfaf1154efba122f92359f4e580@auth.local",
>     "generated_at": "2019-09-19T02:41:53+00:00",
>     "last_access": "2019-09-19T03:56:13+00:00",
>     "permission": "rw"
> }
> ```

**Possible Errors**

* 400 bad request.
* 404 not found.
* 403 permission denied.
* 500 Internal Server Error.


## List A Base's API Tokens

Return the list of all the API tokens of a base.


**URL Structure**

> **\[GET]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/api-tokens/



**Request Authentication**

> User Authentication (Token)


**Sample Request**

List all the API tokens of the base `Test` in the workspace `1`:

> ```
> curl \
> -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Test/api-tokens/"
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the target base is stored.

**name** _\[string, required]_
> The name of the target base.


**Return Values**

JSON-object with the list of API tokens and their details.


**Sample Response (200)**

Returned list indicates there are two existing API tokens in this base:

> ```
> {
>     "api_tokens": [
>         {
>             "app_name": "Google",
>             "api_token": "d66f83fccd0299f0dfe70e1ca807f05921f2de5f",
>             "generated_by": "12345cfaf1154efba122f92359f4e580@auth.local",
>             "generated_at": "2019-09-19T02:41:53+00:00",
>             "last_access": "2019-09-19T03:56:13+00:00",
>             "permission": "rw"
>         },
>         {
>             "app_name": "Postman",
>             "api_token": "4351cacae2c504e6a8ce5a75e95ae769629a70a2",
>             "generated_by": "12345cfaf1154efba122f92359f4e580@auth.local",
>             "generated_at": "2019-09-19T03:01:58+00:00",
>             "last_access": "2019-09-19T03:01:58+00:00",
>             "permission": "rw"
>         }
>     ]
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the workspace or the base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```



404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Fest not found."
> }
> ```


## Update A Base's API Token

Change the permission of a base's API token.


**URL Structure**

> **\[PUT]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/api-tokens/`<app_name>`/



**Request Authentication**

> User Authentication (Token)

**Sample Request**

Change the permission of the API token "Google" of the base `Test` in the workspace `1` to read-only:


> ```
> curl -X PUT \
> -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Test/api-tokens/Google/ \
> -d "permission=r"
> ```


**Input Parameters**


**workspace_id** _\[int, required]_
> The ID of the workspace where the target base is stored.

**name** _\[string, required]_
> The name of the target base.

**app_name** _\[string, required]_
> The name of the App to be connected to this API.

**permission** _\[string(`r` or `rw`), required]_
> Set the permission: `r` for read-only and `rw` for read & write.


**Return Values**

JSON-object with the details of the updated API token.


**Sample Response (200)**

The updated details of the API token "Google" are returned:

> ```
> {
>     "app_name": "Google",
>     "api_token": "d66f83fccd0299f0dfe70e1ca807f05921f2de5f",
>     "generated_by": "12345cfaf1154efba122f92359f4e580@auth.local",
>     "generated_at": "2020-11-10T10:24:14+00:00",
>     "last_access": "2020-11-10T10:24:14+00:00",
>     "permission": "r"
> }
> ```
An updated API token is practically newly generated, so the `generated_at` value indicates the time of change, but not the time of the initial creation.


**Possible Errors**

400 Bad Request: The parameter `permission` was not correctly typed in:
> ```
> {
>     "error_msg": "permission invalid."
> }
> ```

400 Bad Request: The parameter `permission` was not changed:
> ```
> {
>     "error_msg": "api token already has r permission."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the workspace or the base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Fest not found."
> }
> ```


## List Base API Tokens Status

Get the status of the API tokens in a base.


**URL Structure**

> **\[GET]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/api-tokens-status/


**Request Authentication**

> User Authentication (Token)


**Request Sample**

Request the tokens' status of the base `Test` in the workspace `1`:

> ```
> curl \
> -H 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> -H 'Accept: application/json; indent=4' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Test/api-tokens-status/' 
> ```

**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the target base is stored.

**name** _\[string, required]_
> The name of the target base.


**Return Values**

JSON-object with the API status list. The `connected` value indicates if the API has been connected (`true`) or not.


**Response Sample**

Status of the two API tokens in the base `Test` is returned, the returned `connected` value indicates that the API "Postman" has been connected:

> ```
> {
>     "api_status_list": [
>         {
>             "app_name": "Google",
>             "connected": false,
>             "last_access": "2020-11-10T10:24:14+00:00"
>         },
>         {
>             "app_name": "Postman",
>             "connected": true,
>             "last_access": "2020-11-10T08:33:57+00:00"
>         }
>     ]
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the workspace or the base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Fest not found."
> }
> ```


## Delete a DTable API Token

Delete one of the API tokens in a base.

**URL Structure**

> **\[DELETE]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/api-tokens/`<app_name>`/



**Request Authentication**

> User Authentication (Token)


**Sample Request**

Delete the API token "Google" from the base `Test` in the workspace `1`:

> ```
> curl -X DELETE \
> -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Test/api-tokens/Google/
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the target base is stored.

**name** _\[string, required]_
> The name of the target base.

**app_name** _\[string, required]_
> The name of the App to be connected to this API.



**Return Values**

JSON-object with the result of the operation.


**Sample Response (200)**

The result indicates the delete was successful:

> ```
> {
>        "success": true
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the workspace or the base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The API token was not found (wrong, or already deleted):
> ```
> {
>     "error_msg": "api token not found."
> }
> ```

## Get A Base's Access Token with its API Token

With the base API token, you can get its access token to execute base related operations.


**URL Structure**

> **\[GET]** /api/v2.1/dtable/app-access-token/


**Request Authentication**

> Base API Token



**Sample Request**

With the base API token `8g971000df0d6fbntc59580766329a5b37adfh`, request its access token:

> ```
> curl \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> -H 'Authorization: Token 8g971000df0d6fbntc59580766329a5b37adfh' \
> "https://cloud.seatable.io/api/v2.1/dtable/app-access-token/"
> ```

**Input Parameters**

None.


**Return Values**

JSON-object with access token and other details of the base.


**Sample Response (200)**

The response returns the access token of the base among other details:

> ```
> {
>     "app_name": "Postman",
>     "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NjkyMjYxNzEsImR0YWJsZV91dWlkIjoiYjFjYWViNjFjZThmNDhiOWFlY2ZkNDZkNDI5OGM2MmQiLCJ1c2VybmFtZSI6IjEyM0BxcS5jb20iLCJwZXJtaXNzaW9uIjoiciIsImFwcF9uYW1lIjoicnR5dSJ9.pUn_HtrNwISji0nOe0_-0b5JyXN0yEIwzhdIaju-8VE",
>     "dtable_uuid": "b1caeb61ce8f48b9aecfd46d4298c62d",
>     "dtable_server": "https://cloud.seatable.io/dtable-server/",
>     "dtable_socket": "https://cloud.seatable.io/",
>     "workspace_id": 1,
>     "dtable_name": "Test"
> }
> ```

**Possible Errors**

403 Forbidden: The API token was not found or invalid:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

## Get File Upload Link by API Token

Get the file upload link to a base by its API token.


**URL Structure**

> **\[GET]** /api/v2.1/dtable/app-upload-link/



**Request Authentication**

> Base API Token

**Sample Request**

Request the file upload link for the base with API token of `0303f89b3607fb86039fdffcf1be6383797b437f`:

> ```
> curl \
> -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' \
> -H 'Accept: application/json; indent=4' \
> "https://cloud.seatable.io/api/v2.1/dtable/app-upload-link/"
> ```


**Input Parameters**

None.


**Return Values**

JSON-object with upload link and parent path.


**Sample Response (200)**

> ```
> {
>     "upload_link": "https://cloud.seatable.io/seafhttp/upload-api/047537b8-833d-4c05-bf5e-4ddbe8e408e3",
>     "parent_path": "/asset/5a40dd8e-59b7-49ff-84a7-3c9fb8a0cf60"
> }
> ```

**Possible Errors**

403 Forbidden: The API token was not found or invalid:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

## Get File Download Link by API Token

Get the file download link to a base by its API token.

**URL Structure**

> **\[GET]** /api/v2.1/dtable/app-download-link/


**Request Authentication**

> Base API Token

* path, asset path inside /asset/dtable_uuid/ folder

**Sample Request**

Get the download link of the image `/images/2020-02/test_pic.jpg`:

> ```
> curl \
> -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' \
> -H 'Accept: application/json; indent=4' \
> "https://cloud.seatable.io/api/v2.1/dtable/app-download-link/?path=/images/2020-02/test_pic.jpg"
> ```


**Input Parameters**

**path** _\[string, required]_
> Asset path inside the `/asset/<dtable_uuid>/` folder.



**Return Values**

JSON-object with the download link.



**Sample Response (200)**

> ```
> {
>     "download_link": "https://cloud.seatable.io/seafhttp/files/498fe8b6-68f4-4878-8ce7-91517b9c6e1c/test_pic.jpg"
> }
> ```

**Possible Errors**

400 Bad Request: The given path/file was not found:
> ```
> {
>     "error_msg": "path /images/2020-11/jasmintee.jp not found."
> }
> ```

403 Forbidden: The API token was not found or invalid:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

