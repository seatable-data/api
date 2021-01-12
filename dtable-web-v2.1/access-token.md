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
>
> ```

**Input Parameters**

**workspace_id** _\[int, required]_

> The ID of the workspace where the base is located.

**dtable_name** _\[string, required]_

> The name of the base.

**Return Values**

JSON-object with the access token and other infos of the base.

**Sample Response (200)**

The access token and other details of the base are returned:

> ```
> {
>    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkdGFibGVfdXVpZCI6IjIwMDRjZWIzZDQyZDRiMDI5YTkzYjFkOWEwOWQxZTYxIiwiZXhwIjoxNTY1NTg5NjI5fQ.PdzbZKoEFQ2zONPwX9ouMdzM4GAzD5xAhxtGkmr4P9M",
>    "dtable_uuid": "a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf"
>    "dtable_server": "https://cloud.seatable.io/dtable-server/",
>    "dtable_socket": "https://cloud.seatable.io/"
> }
>
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have access to the requested base (workspace):

> ```
> {
>     "error_msg": "Permission denied."
> }
>
> ```

404 Not Found: The base cannot be found under the given name:

> ```
> {
>     "error_msg": "dtable Hallo not found."
> }
>
> ```

## Get A Base's Access Token via Invite Link

Get the access token to a base via its invite link token.

**URL Structure**

> **\[GET]** /api/v2.1/dtable/share-link-access-token/

**Request Authentication**

None.

**Sample Request**

> ```
> curl \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/dtable/share-link-access-token/?token=d64ec2886e9e45b696d9"
>
> ```

**Input Parameters**

**share_link_access_token** _\[string, required]_

> A base's share link access token is the suffix to its invite link, i.e. 'https\://cloud.seatable.io/dtable/links/`<share link token>`/'

**Return Values**

JSON-object with the access token and the ID of the base.

**Sample Response (200)**

> ```
> {
>     "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkdGFibGVfdXVpZCI6IjIwMDRjZWIzZDQyZDRiMDI5YTkzYjFkOWEwOWQxZTYxIiwiZXhwIjoxNTY1NTg5NjI5fQ.PdzbZKoEFQ2zONPwX9ouMdzM4GAzD5xAhxtGkmr4P9M",
>     "dtable_uuid": "a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf"
> }
>
> ```

**Possible Errors**

* 400 Bad Request.
* 403 Permission Denied.
  404 Not Found: The share link token is not valid:

  > ```
  > {
  >     "error_msg": "Share link e3dab1cd248c488bbfdf not found."
  > }
  >
  > ```


