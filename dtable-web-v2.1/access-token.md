# Access Token

In this article, methods of getting a base's access token via user's auth token and via share link are covered. One further way to get a base's access token is to get it via the base's API token, for more details refer to [APIs reading/writing a single base](https://docs.seatable.io/published/seatable-api/home.md).

## Get A Base's Access Token

Get a base's access token with the user's auth token. 


**URL Structure**

> **\[GET]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<dtable_name>`/access-token/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

With the user's auth token, get the access token of the base "Hello" in the workspace 1:

> ```
> curl 
> -H 'Authorization: Token 57782e1e42a7fefc6a5026e00c6a62c9d249e760' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Hello/access-token/"
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is located.

**dtable_name** _\[string, required]_
> The name of the base.


**Return Values**

JSON-object with the access token and other infos of the base.



**Sample Response**

The access token and other details of the base are returned:
>```
>{
>    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkdGFibGVfdXVpZCI6IjIwMDRjZWIzZDQyZDRiMDI5YTkzYjFkOWEwOWQxZTYxIiwiZXhwIjoxNTY1NTg5NjI5fQ.PdzbZKoEFQ2zONPwX9ouMdzM4GAzD5xAhxtGkmr4P9M",
>    "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60"
>    "dtable_server": "https://cloud.seatable.io/dtable-server/",
>    "dtable_socket": "https://cloud.seatable.io/"
>}
>```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the requested base (workspace):
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base cannot be found under the given name:
> ```
> {
>     "error_msg": "dtable Hallo not found."
> }
> ```


## Get A Base's Read-only Access Token via Share Link

Get the read-only access token to a base via its external share link token.


**URL Structure**

> **\[GET]** /api/v2.1/dtable/share-link-access-token/


**Request Authentication**

None.


**Sample Request**

> ```
> curl \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/dtable/share-link-access-token/?token=d64ec2886e9e45b696d9"
> ```

**Input Parameters**

**share_link_access_token** _\[string, required]_
> A base's share link access token is the suffix to its share link, i.e. 'https\://cloud.seatable.io/dtable/external-links/`<share link token>`/'


**Sample Response**

> ```
> {
>     "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkdGFibGVfdXVpZCI6IjIwMDRjZWIzZDQyZDRiMDI5YTkzYjFkOWEwOWQxZTYxIiwiZXhwIjoxNTY1NTg5NjI5fQ.PdzbZKoEFQ2zONPwX9ouMdzM4GAzD5xAhxtGkmr4P9M",
>     "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60"
> }
> ```

**Possible Errors**

* 400 Bad Request.
* 403 Permission Denied.


