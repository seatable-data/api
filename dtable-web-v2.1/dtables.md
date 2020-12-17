# Bases (DTables)

## Create A Base

Use this request to create a new base in your workspace or in a group.


**URL Structure**

> **\[POST]** /api/v2.1/dtables/


**Request Authentication**

> User Authentication (Token)

**Sample Request**

Use this request to create a new base named `Pricing` in the workspace of the user with the following ID and give it a symbol color of `7626FD`:

> ```
> curl -X POST \
> "https://cloud.seatable.io/api/v2.1/dtables/" \
> -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; indent=4' \
> -d 'name=Pricing&owner=5758ecdce3e741ad81293a304b6d3388@auth.local&color=#7626FD' 
> ```


**Input Parameters**

**owner** _\[string, required]_
> The ID of the owner (xxxx@auth.local) to create the base in your own "My Bases" library, or of a group to create the base into the group.

**name** _\[string, required]_
> The name of the base.

**color** _\[HEX, optional]_
> The color of the base, defined by a hexadecimal code. When left blank, SeaTable gives it a default orange color.

**icon** _\[string, optional]_
> The icon (symbol) of the base, chosen from the list of SeaTable Base Symbols. When left blank, SeaTable gives it a default icon.

**text_color** _\[HEX, optional, not supported yet]_
> The color of the name text of the base, defined by a hexadecimal code. When left blank, SeaTable gives it the default text color.



**Return Values**

JSON-object with the details of the created base.



**Sample Response (201)**

> ```
> {
>     "table": {
>         "id": 407,
>         "workspace_id": 377,
>         "uuid": "476ea18d-78cb-47b8-be2d-2cbce36ea220",
>         "name": "Pricing",
>         "creator": "Robert Teamplayer",
>         "modifier": "Robert Teamplayer",
>         "created_at": "2020-12-17T15:52:28+00:00",
>         "updated_at": "2020-12-17T15:52:28+00:00",
>         "color": "#7626FD",
>         "text_color": null,
>         "icon": null
>     }
> }
> ```

**Possible Errors**

400 Bad Request: The required parameter was missing:
> ```
> {
>     "error_msg": "name invalid."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have the permission to assign the owner or group of the base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```


## Update A Base

Use this request to rename, change color and icon of a base.


**URL Structure**

> **\[PUT]** /api/v2.1/workspace/`<workspace_id>`/dtable/



**Request Sample**

Change the name of the base `Pricing` to `Offering`:
> ```
> curl --request PUT \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/' \
> --form 'name=Pricing' \
> --form 'new_name=Offering' \
> ```


**Input Parameters**

**name** _\[string, required]_
> The current name of the base.

**new_name** _\[string, optional]_
> The new name of the base.

**color** _\[HEX, optional]_
> The new color of the base, defined by a hexadecimal code. When left blank, SeaTable gives it a default orange color.

**icon** _\[string, optional]_
> The new icon (symbol) of the base, chosen from the list of SeaTable Base Symbols. When left blank, SeaTable gives it a default icon.

**text_color** _\[HEX, optional, not supported yet]_
> The new color of the name text of the base, defined by a hexadecimal code. When left blank, SeaTable gives it the default text color.



**Return Values**

JSON-object with the details of the updated base.

**Sample Response (200)**

The returned values indicate that the name has been changed:

> ```
> {
>     "table": {
>         "id": 407,
>         "workspace_id": 377,
>         "uuid": "476ea18d-78cb-47b8-be2d-2cbce36ea220",
>         "name": "Offering",
>         "creator": "Robert Teamplayer",
>         "modifier": "Robert Teamplayer",
>         "created_at": "2020-12-17T15:52:28+00:00",
>         "updated_at": "2020-12-17T15:52:28+00:00",
>         "color": "#7626FD",
>         "text_color": null,
>         "icon": null
>     }
> }
> ```

**Possible Errors**

400 Bad Request: The target name already exists in the target workspace:
> ```
> {
>     "error_msg": "Offering exists."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the requested base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Pricingg not found."
> }
> ```

## Delete A Base

Use this request to delete an existing base.


**URL Structure**

> **\[DELETE]** /api/v2.1/workspace/`<workspace_id>`/dtable/


**Request Authentication**

> User Authentication (Token)




**Sample Request**

Delete the base `Pricing` from the workspace `1`:

> ```
> curl -X DELETE \
> -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; indent=4' \
> "http://cloud.seatable.io/api/v2.1/workspace/1/dtable/"
> -d "name=Pricing" 
> ```



**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.



**Return Values**

JSON-object with the result of the operation.



**Sample Response (200)**

> ```
> {
>     "success":"true"
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the requested base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found (probably already deleted):
> ```
> {
>     "error_msg": "dtable Pricing not found."
> }
> ```

