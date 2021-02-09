# Related Users

## Get User List by User ID List

List the basic information of other users in your organization.

**URL Structure**

> **\[POST]** /api/v2.1/user-list/


**Request Authentication**

> User Authentication (Token)

**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization:Token e1518ab0624eed78ab9456d207e312666fcaf748' \
> -H 'Content-type: application/json' \
> -H 'Accept: application/json; indent=4' \
> 'https://cloud.seatable.io/api/v2.1/user-list/' \
> -d '{ \
>     "user_id_list": [ \
>         "5758ecdce3e741ad81293a304b6d3388@auth.local", \
>         "5ed78cb2cd264b0e8c400f131bc5c4c8@auth.local"  \
>     ] \
> }' 
>
> ```

**Input Parameters**

**user_id_list** _\[array, required]_
> In this object, list the users' IDs ending with `@auth.local`.

**Return Values**

JSON-object with the list of users.

**Sample Response (200)**

> ```
> {
>     "user_list": [
>         {
>             "email": "244b43hr6fy54bb4afa2c2cb7369d244@auth.local",
>             "name": "Ginger Ale",
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png"
>         },
>         {
>             "email": "8cb2a6da656876hgf42905bf1647fd3f@auth.local",
>             "name": "Jasmin Tee",
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png"
>         }
>     ]
> }
>
> ```

**Errors**

* 400 Bad Request.
* 500 Internal Server Error.


