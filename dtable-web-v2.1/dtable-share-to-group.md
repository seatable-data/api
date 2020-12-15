# Sharing Bases to Groups

## List Bases Shared to My Groups

This request lists off all the bases shared by other users to the groups which I am in.


**URL Structure**

> **\[GET]** api/v2.1/dtables/group-shared/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

> ```
> curl --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/dtables/group-shared/' 
> ```


**Input Parameters**

None.


**Return Values**

JSON-object with the list of shared bases in groups.


**Sample Response (200)**

The response to the sample request lists off two bases `DataBase` and `Surveys` shared to me via the groups `162` and `165`, respectively.

> ```
> {
>     "group_shared_dtables": {
>         "162": [
>             {
>                 "id": 375,
>                 "workspace_id": 377,
>                 "uuid": "4b543a04-39b7-4ce7-aa08-7fe1f4dad0b5",
>                 "name": "DataBase",
>                 "creator": "Robert Teamplayer",
>                 "modifier": "Robert Teamplayer",
>                 "created_at": "2020-11-19T14:43:24+00:00",
>                 "updated_at": "2020-11-19T14:43:24+00:00",
>                 "color": "#7626FD",
>                 "text_color": "#7626FD",
>                 "icon": "icon-software-test-management",
>                 "starred": false
>             }
>         ],
>         "165": [
>             {
>                 "id": 355,
>                 "workspace_id": 377,
>                 "uuid": "03d8b71c-84c7-4a16-b314-94c886dc170p",
>                 "name": "Surveys",
>                 "creator": "Robert Teamplayer",
>                 "modifier": "Robert Teamplayer",
>                 "created_at": "2020-11-17T15:39:26+00:00",
>                 "updated_at": "2020-12-14T14:26:29+00:00",
>                 "color": null,
>                 "text_color": null,
>                 "icon": null,
>                 "starred": false
>             }
>         ]
>     }
> }
> ```
If no bases have been shared to me via groups, an empty list will be returned without error message.

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

## Share A Base to A Group

Share a base from My Bases to a group that I'm in.


**URL Structure**

> **\[POST]** api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/group-shares/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

Share the base `Reports` from My Bases (which is in the workspace `1`) to the group with ID of `64` and read-only permission:

> ```
> curl --request POST \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Reports/group-shares/' \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> --form 'group_id=64' \
> --form 'permission=r'
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.

**group_id** _\[int, required]_
> The ID of the group you are sharing your base to.

**permission** _\[string(`r` or `rw`), required]_
> Define the sharing permission: read-only(`r`), or read and write(`rw`).



**Return Values**

JSON-object with summarization of the sharing.



**Sample Response (200)**

> ```
> {
>     "dtable_group_share": {
>         "group_id": "64",
>         "group_name": "SeaTable QA",
>         "permission": "r"
>     }
> }
> ```

**Possible Errors**

400 Bad Request: A base with the identical name already exists in the target group:
> ```
> {
>     "error_msg": "table Reports already shared to the group."
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
>     "error_msg": "Table Projects not found."
> }
> ```



## Update A Base's Sharing Permission to A Group

Change the sharing permission (read-only or read and write) of a base shared to a group.


**URL Structure**

> **\[PUT]** api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/group-shares/`<group_id>`/


**Request Authentication**

> User Authentication (Token)



**Sample Request**

Change the sharing permission of the base `Reports` I'm sharing from My Bases (which is in the workspace `1`) to the group `64` from read-only to read and write:

> ```
> curl --location --request PUT \
> -h 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Reports/group-shares/64/' \
> --form 'permission=rw'
> ```



**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.

**group_id** _\[int, required]_
> The ID of the group you are sharing your base to.

**permission** _\[string(`r` or `rw`), required]_
> Update the sharing permission: read-only(`r`), or read and write(`rw`).


**Return Values**

JSON-object with the result of the operation.


**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```

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

404 Not Found: No bases from the current workspace are shared in the target group:
> ```
> {
>     "error_msg": "There isn't share to group 64"
> }
> ```

## List All Groups A Base is Shared to

Use this request to list all the groups a particular base is being shared to.


**URL Structure**

> **\[GET]** api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/group-shares/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

List all the groups that the base `Reports` (in the workspace `1`) is being shared to:

> ```
> curl --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Reports/group-shares/' 
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.


**Return Values**

JSON-object with the list of groups the base is shared to.

**Sample Response (200)**

Returned response shows, the base has been shared to two groups:

> ```
> {
>     "dtable_group_share_list": [
>         {
>             "group_id": 62,
>             "group_name": "Customer Service",
>             "permission": "r"
>         },
>         {
>             "group_id": 65,
>             "group_name": "SeaTable",
>             "permission": "rw"
>         }
>     ]
> }
> ```
If a base isn't shared to any groups, an empty list will return without error message.

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
>     "error_msg": "Table DtableTestBae not found."
> }
> ```

## Stop Sharing A Base to A Group

Cancel the sharing of a base to a certain group.


**URL Structure**

> **\[DELETE]** api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/group-shares/`<group_id>`/



**Request Authentication**

> User Authentication (Token)

**Sample Request**

Stop sharing the base `Reports` (which is in the workspace `1`) to the group with ID of `64`:

> ```
> curl --request DELETE \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Reports/group-shares/64/' 
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.

**group_id** _\[int, required]_
> The ID of the group you are sharing your base to.



**Return Values**

JSON-object with the result of the operation.




**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```




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

404 Not Found: No bases from the current workspace are shared in the target group (or the share has already been cancelled):
> ```
> {
>     "error_msg": "There isn't share to group 64"
> }
> ```

