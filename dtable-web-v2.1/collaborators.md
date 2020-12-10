# Collaborators

## List Collaborators of A Base

Users who have read & write permission to a base are the collaborators, or related users, to this base. This API request lists all the collaborators of a base and returns their basic information.


**URL Structure**

> **\[GET]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/related-users/



**Request Authentication**

> User Authentication (Token)



**Sample Request**

List all the collaborators to the base `Teamwork` in the workspace `1`:

```
curl \
-H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
-H 'Accept: application/json; charset=utf-8; indent=4' \
"http://cloud.seatable.io/api/v2.1/workspace/1/dtable/Teamwork/related-users/"
```

**Input Parameters**

**workspace_id** _\[numeric, required]_
> The ID of the workspace where the target base is stored.

**name** _\[string, required]_
> The name of the target base.


**Return Values**

JSON-object with related user list.


**Sample Response**

The returned user list includes the basic information of the base's collaborators:

> ```
> {
>     "user_list": [
>         {
>             "email": "12345cfaf1154efba122f92359f4e580@auth.local",
>             "name": "Max Teamleader",
>             "contact_email": "teamleader@example.com",
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png"
>         },
>         {
>             "email": "9idjfkeh49b946a3b200555db5de1d23@auth.local",
>             "name": "Robert Teamplayer",
>             "contact_email": "teamplayer@example.com",
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png"
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

404 Not Found: The base with the given `name` was not found:
> ```
> {
>     "error_msg": "dtable Teamwood not found."
> }
> ```