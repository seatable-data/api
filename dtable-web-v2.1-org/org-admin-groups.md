# Org Admin Groups

## Add A Group

Add a new empty group in the current organization.


**URL Structure**

> **\[POST]** /api/v2.1/org/`<org_id>`/admin/groups/ 


**Request Authentication**

> Org-admin Authentication (Token)


**Sample Request**

As the org-admin of the organization with `org_id` 4, add a new group with the `group_name` of "SeaTable" and appoint the user with ID `7c1d2ea7cc15425889d557e0c99efcf3@auth.local` as owner of the group:


> ```
> curl --request POST \
> --header 'Authorization: Token b6720d34395851f7bada7d86d8f121936b727391' \
> "https://cloud.seatable.io/api/v2.1/org/4/admin/groups/" \
> --form 'group_name=SeaTable' \
> --form 'group_owner=7c1d2ea7cc15425889d557e0c99efcf3@auth.local'
> ```



**Input Parameters**

**group_name** _\[string, required]_
> Name of the new group.

**group_owner** _\[string, optional]_
> The owner of the group:
> * This user has to be a member in this organization.
> * Group owner can rename the group, manage members, transfer, and delete the group.
> * If not given, the newly added group will not be visible to any user in the base library, but only appears in the organization administration page.


**Return Values**

JSON-object with the group details. The group's `id` is automatically generated. 


**Sample Response (200)**

A group `id` and other details are returned in the response to the sample request:

> ```
> {
>     "id": 23,
>     "group_name": "SeaTable",
>     "ctime": "2020-12-08T13:30:26+00:00",
>     "creator_email": "7c1d2ea7cc15425889d557e0c99efcf3@auth.local",
>     "creator_name": "Max Teamleader",
>     "creator_contact_email": "teamleader@example.com"
> }
> ```

**Possible Errors**

400 Bad Request: The group's name already exists:
> ```
> {
>     "error_msg": "There is already a group with that name."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have org-admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```


404 Not Found: The assigned `group_owner` was not found, possible causes are:
* The user's ID was given correctly, but the user is not in the current organization;
* The user's ID (ending with `@auth.local`) was mistaken by email address.
> ```
> {
>     "error_msg": "User correct-user@example.com not found."
> }
> ```

## List Members of A Group

List the details of all the members of a given group.


**URL Structure**

> **\[GET]** /api/v2.1/org/`<org_id>`/admin/groups/`<group_id>`/members/


**Request Authentication**

> Org-admin Authentication (Token)

**Sample Request**

List the members of the group with ID of `19` in the organization with `org_id` of `4`:

>```
> curl --request GET \
> --header >'Authorization: Token b6720d34395851f7bada7d86d8f121936b727391' \
> "https://cloud.seatable.io/api/v2.1/org/4/admin/groups/19/members/" 
>```


**Input Parameters**

**org_id** _\[int, required]_
> The ID of the organization where the group is.

**group_id** _\[int, required]_
> The ID of the group.


**Return Values**

JSON-object with the details of the group members.



**Sample Response (200)**

The response to the sample request returns two members in this group:

> ```
> {
>     "group_id": 19,
>     "group_name": "Sample group",
>     "members": [
>         {
>             "group_id": 19,
>             "name": "Robert Teamplayer",
>             "email": "9f11ca9949b946a3b200555db5d38fd7@auth.local",
>             "contact_email": "teamplayer@example.com",
>             "login_id": "",
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
>             "is_admin": false,
>             "role": "Member"
>         },
>         {
>             "group_id": 19,
>             "name": "Max Teamleader",
>             "email": "26815cfaf1154efba122f92359ffj4g6@auth.local",
>             "contact_email": "teamleiter@example.com",
>             "login_id": "",
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
>             "is_admin": true,
>             "role": "Owner"
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

403 Forbidden: The user doesn't have org-admin permission:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The group was not found in the given organization:
> ```
> {
>     "error_msg": "Group 9 not found."
> }
> ```


## Batch Add Members to A Group

Add multiple members to a group in one request.


**URL Structure**

> **\[POST]** /api/v2.1/org/`<org_id>`/admin/groups/`<group_id>`/members/


**Request Authentication**

> Org-admin Authentication (Token)



**Sample Request**

Add the users with the following IDs to the group `19` in the organization `4`:

> ```
> curl --request POST \
> --header 'Authorization: Token b6720d34395851f7bada7d86d8f121936b727391' \
> "https://cloud.seatable.io/api/v2.1/org/4/admin/groups/19/members/" \
> --form 'email=7c1d2ea7cc15425889d557e0c99efcf3@auth.local' \
> --form 'email=dfc3bfdf9aa9451bb544428fc8486fc4@auth.local' \
> --form 'email=5f11c0e0b9ba4c50b5ecc1f231a6ea1d@auth.local' 
> ```


**Input Parameters**

**org_id** _\[int, required]_
> The ID of the organization where the group is.

**group_id** _\[int, required]_
> The ID of the group.

**email** _\[string, multiple, required]_
> The ID(s) of the user(s) being added to the group.



**Return Values**

JSON-object with the list of existing (if any) and added members.



**Sample Response (200)**

> ```
> {
>     "failed": [
>         {
>             "email": "7c1d2ea7cc15425889d557e0c99efcf3@auth.local",
>             "error_msg": "User Max Teamleader is already a group member."
>         },
>         {
>             "email": "dfc3bfdf9aa9451bb544428fc8486fc4@auth.local",
>             "error_msg": "User Robert Teamplayer is already a group member."
>         }
>     ],
>     "success": [
>         {
>             "group_id": 49,
>             "name": "Karlheinz Teamplayer",
>             "email": "5f11c0e0b9ba4c50b5ecc1f231a6ea1d@auth.local",
>             "contact_email": "teamplayer2@example.com",
>             "login_id": "",
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
>             "is_admin": false,
>             "role": "Member"
>         }
>     ]
> }
> ```
If all the users are already in the group, the above response returns a list of "failed" and an empty list of "success" without error message. Similarly, if the user's ID was not found or was mistaken by their contact email address, the response will list them in the "failed" object without error message:
> ```
> {
>     "failed": [
>         {
>             "email": "wumeng@outlook.com",
>             "error_msg": "User teamplayer@example.com not found."
>         }
>     ],
>     "success": []
> }
> ```



**Possible Errors**

400 Bad Request: The parameter `email` was not written correctly (e.g. 'Email' or 'e-mail' are not accepted):
> ```
> {
>     "error_msg": "Email invalid."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have org-admin permission:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ``` 

403 Forbidden: The user doesn't have permission to operate the current organization or group, or has given a group ID that doesn't exist in the current organization:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```



## Change Admin of A Group

There are three types of roles in a group: `Owner`, `Admin`, or `Member`. As org-admin, you can use this API request to change a member's role to `Admin` or reversed. For more details to these roles, refer to the [SeaTable Manual - Groups](https://seatable.io/en/docs/user-manual/zusammenarbeit/gruppen/).


**URL Structure**

> **\[PUT]** /api/v2.1/org/`<org_id>`/admin/groups/`<group_id>`/members/`<email>`/ 


**Request Authentication**

> Org-admin Authentication (Token)





**Sample Request**

In the group `19` of the organization `4`, make followin user `Admin` of the group:
> ```
> curl --request PUT \
> --header 'Authorization: Token b6720d34395851f7bada7d86d8f121936b727391' \
> "https://cloud.seatable.io/api/v2.1/org/4/admin/groups/19/members/dfc3bfdf9aa9451bb544428fc8486fc4@auth.local/" \ 
> --form 'is_admin=true'
> ```


**Input Parameters**

**org_id** _\[int, required]_
> The ID of the organization where the group is.

**group_id** _\[int, required]_
> The ID of the group.

**email** _\[string, required]_
> The ID of the user, ending with @auth.local. This is not the user's contact email address.

**is_admin** _\[enum(true, false), required]_
> If `true`, the user becomes an admin of the group.



**Return Values**

JSON-object with the details of the updated user.



**Sample Response (200)**

The user has been successfully made admin of the group:
> ```
> {
>     "group_id": 19,
>     "name": "Robert Teamplayer",
>     "email": "dfc3bfdf9aa9451bb544428fc8486fc4@auth.local",
>     "contact_email": "Teamplayer@example.com",
>     "login_id": "",
>     "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
>     "is_admin": true,
>     "role": "Admin"
> }
> ```
If the user is already admin of the group, the same response will be returned without error message. The same also applies for the case, if the user isn't an admin of the group.

**Possible Errors**

400 Bad Request: The `is_admin` parameter was missing, or incorrectly given:
> ```
> {
>     "error_msg": "is_admin invalid."
> }
> ```

400 Bad Request: The user is not in the current group:
> ```
> {
>     "error_msg": "Email 9eit7667d1754bb4afa2c2cb7369d244@auth.local invalid."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Permission Denied: The user doesn't have permission to perform this request:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```

404 Not Found: The given user's ID was wrong, or not found:
> ```
> {
>     "error_msg": "User Teamplayer@example.com not found."
> }
> ```




## Remove A Member from A Group

Move a member out of a certain group.


**URL Structure**

> **\[DELETE]** /api/v2.1/org/`<org_id>`/admin/groups/`<group_id>`/members/`<email>`/ 


**Request Authentication**

> Org-admin Authentication (Token)



**Sample Request**

> ```
> curl --request DELETE \
> --header 'Authorization: Token b6720d34395851f7bada7d86d8f121936b727391' \
> "https://cloud.seatable.io/api/v2.1/org/4/admin/groups/19/members/dfc3bfdf9aa9451bb544428fc8486fc4@auth.local/" 
> ```


**Input Parameters**

**org_id** _\[int, required]_
> The ID of the organization where the group is.

**group_id** _\[int, required]_
> The ID of the group.

**email** _\[string, required]_
> The ID of the user, ending with @auth.local. This is not the user's contact email address.


**Return Values**

JSON-object with the result of the operation.




**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```
This request makes sure the user is out of the group. If the user is already removed (or perhaps doesn't belong to the organization, or even doesn't exist), the above response will also be returned without error message.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Permission Denied: The user doesn't have permission to perform this request:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```


