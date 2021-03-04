# Base External Link

External links let external anonymous users visit your bases in read-only mode. 

## Add An External Link

Use this request to generate an external link for a base, optionally set a password, an expiration date, or a custom token.

**URL Structure**

> **\[POST]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<base_name>`/external-links/


**Request Authentication**

> User Authentication (Token)

**Sample Request**

> ```
> curl -X -POST \
> -H 'Authorization: Token a407800e307ee8eb545fab94e2d22bb37944661f' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/test/external-links/' \
> --form 'password="12345678"' \
> --form 'expire_days="30"' \
> --form 'token="fleischkaesebroetchen"'
> ```

**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is located.

**base_name** _\[string, required]_
> The name of the base.

**password** _\[string, optional]_
> Add a password for protection. Once an external link is password protected, it cannot be downloaded with the API request **Download A Base Through its External Link** (see below).

**expire_days** _\[int, optional]_
> When given a number of days here, the external link will expire after that time.

**token** _\[string, optional]_
> Custom the suffix of the generated external link. Use only the numbers (0-9) and letters (a-z, A-Z) here.



**Return Values**

JSON-object with the details of the generated external link.


**Sample Response**

> ```
> {
>     "url": "https://cloud.seatable.io/dtable/external-links/custom/fleischkaesebroetchen/",
>     "token": "fleischkaesebroetchen",
>     "is_custom": true,
>     "permission": "read-only",
>     "is_expired": false,
>     "expire_date": "2021-04-03T11:11:18+00:00"
> }
> ```


**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have access to the workspace or the base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The named base was not found:
> ```
> {
>     "error_msg": "SeaTable {{base_name}} not found."
> }
> ```


## Download A Base Through its External Link

Use this request to download a base through its external link.


**URL Structure**

> **\[GET]** /dtable/external-links/<token>/download-zip/


**Request Authentication**

None.



**Sample Request**

Download the base through the external link with the token `8720e55e17a44aa89990`:

> ```
> curl GET \
> https://cloud.seatable.io/dtable/external-links/8720e55e17a44aa89990/download-zip/
> ```


**Input Parameters**

**token** _\[string, required]_
> As an external link is generated, its token is used as the suffix to its link. For example: https\://cloud.seatable.io/dtable/external-links/`<token>`/



**Return Values**

.dtable file.


**Sample Response (200)**

A .dtable zip file is downloaded.


**Possible Errors**

404 Not Found: The external link token is not valid:
> ```
> Sorry, but the requested page could not be found.
> ```