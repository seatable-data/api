# Sharing Bases to Users

## List Bases Shared to Me

This request lists off all the bases currently shared to me.


**URL Structure**

> **\[GET]** /api/v2.1/dtables/shared/


**Request Authentication**

> User Authentication (Token)

**Sample Request**

> ```
> curl \
> -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/dtables/shared/"
> ```

**Input Parameters**

None.


**Return Values**

JSON-object with the list of shared bases.


**Sample Response (200)**

The response shows there're two bases shared to me:

```
{
    "table_list": [
        {
            "id": 2311,
            "workspace_id": 1,
            "uuid": "8e36ghv5-9d94-4f97-b6fe-8b5509a5aa87",
            "name": "old",
            "creator": "Max Teamleader",
            "modifier": "Max Teamleader",
            "created_at": "2020-11-06T09:54:01+00:00",
            "updated_at": "2020-11-06T09:54:01+00:00",
            "permission": "rw",
            "from_user": "oe9304faf1154efba122f92359f4e580@auth.local",
            "from_user_name": "Max Teamleader"
        },
        {
            "id": 3399,
            "workspace_id": 12,
            "uuid": "ld93urb3-fcd0-489f-b0eb-bdda6aeeb3e6",
            "name": "test",
            "creator": "Max Teamleader",
            "modifier": "Max Teamleader",
            "created_at": "2020-12-15T13:00:02+00:00",
            "updated_at": "2020-12-15T13:00:02+00:00",
            "permission": "rw",
            "from_user": "oe9304faf1154efba122f92359f4e580@auth.local",
            "from_user_name": "Max Teamleader"
        }
    ]
}
```

**Possible Errors**

401 Unauthorized: The auth token was invalid:
> ```
> {
>     "detail": "Invalid token"
> }
> ```

## List Users Sharing A Base

This request returns a list of all the users who are sharing a certain base. Groups sharing the base, including members of these groups, are not listed in the returned response. The user self is also not listed.


**URL Structure**

> **\[GET]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/share/


**Request Authentication**

> User Authentication (Token)



**Sample Request**

List all the users who are sharing the base `Reports` from workspace `1`:

> ```
> curl \
> -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "http://cloud.seatable.io/api/v2.1/workspace/1/dtable/Reports/share/"
> ```

**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.


**Sample Response (200)**

The response returns one user sharing the base with me:
> ```
> {
>     "user_list": [
>         {
>             "email": "oe3jr7v949b946a3b200555db5de1d23@auth.local",
>             "name": "Robert Teamplayer",
>             "contact_email": "teamplayer@example.com",
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
>             "permission": "rw"
>         }
>     ]
> }
> ```
If no user is sharing the base with me, an empty list will be returned without error message.


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

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable ol not found."
> }
> ```

## Share A Base to Another User in the Organization

Using the ID of another user in the same organization, share a base with them.


**URL Structure**

> **\[POST]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/share/


**Request Authentication**

> User Authentication (Token)




**Sample Request**

Share the base `Reports` in the workspace `1` to the user with the ID as follows with read and write permission:

> ```
> curl -X POST \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Reports/share/" \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -d "permission=rw&email=2436ce64315b4b4azfcff9e5491db296@auth.local"
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.

**permission** _\[string(`r` or `rw`), required]_
> Define the sharing permission: read-only(`r`), or read and write(`rw`).

**email** _\[string, required]_
> This is not the contact email, but the user's ID ending with @auth.local.



**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

> ```
> {
>     "success":true
> }
> ```

**Errors**

400 Bad Request: The permission parameter was wrong:
> ```
> {
>     "error_msg": "permission invalid."
> }
> ```

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

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Report not found."
> }
> ```

404 Not Found: The user wasn't found:
> ```
> {
>     "error_msg": "User 2436ce64315b4b4abfcff9e5491db296@auth.loca not found."
> }
> ```

409 Conflict: The base is already shared to the user:
> ```
> {
>     "error_msg": "table Reports already shared to 2436ce64315b4b4abfcff9e5491db296@auth.local."
> }
> ```

## Change A Base's Sharing Permission to A User

When you have shared one of your bases to another user, you can change the sharing permission.


**URL Structure**

> **\[PUT]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/share/



**Request Authentication**

> User Authentication (Token)



**Sample Request**

Change the `Report` base's permission to read only to the user as follows:

> ```
> curl -X PUT \
> -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Reports/share/" \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> -d "permission=r&email=2436ce64315b4b4azfcff9e5491db296@auth.local" 
> ```



**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.

**permission** _\[string(`r` or `rw`), required]_
> Change the sharing permission: read-only(`r`), or read and write(`rw`).

**email** _\[string, required]_
> This is not the contact email, but the user's ID ending with @auth.local.


**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

> ```
> {
>     "success":true
> }
> ```

**Possible Errors**

400 Bad Request: The permission parameter was wrong:
> ```
> {
>     "error_msg": "permission invalid."
> }
> ```

400 Bad Request: The permission was not changed:
> ```
> {
>     "error_msg": "table Reports already has r share permission."
> }
> ```

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

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Report not found."
> }
> ```

404 Not Found: The user wasn't found:
> ```
> {
>     "error_msg": "User 2436ce64315b4b4abfcff9e5491db296@auth.loca not found."
> }
> ```



## Stop Sharing A Base to A User

Cancel the sharing of a base to a user. This operation can be carried out by both the sharing user and the shared user.


**URL Structure**

> **\[DELETE]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/share/



**Request Authentication**

> User Authentication (Token of the sharing user or the shared user)



**Sample Request**

Stop sharing the base `Report` in workspace `1` to the user with the following ID:

> ```
> curl -X DELETE \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Reports/share/" \
> -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> -d "email=2436ce64315b4b4azfcff9e5491db296@auth.local" 
> ```



**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.

**email** _\[string, required]_
> This is not the contact email, but the user's ID ending with @auth.local.



**Sample Response (200)**

> ```
> {
>     "success":true
> }
> ```

**Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have permission to carry out this operation:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not shared to the user:
> ```
> {
>     "error_msg": "table Reports not shared to 2436ce64315b4b4azfcff9e5491db296@auth.local."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Report not found."
> }
> ```


