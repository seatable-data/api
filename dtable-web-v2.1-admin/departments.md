# Departments

## List Departments

List all the departments in the current level.

**URL Structure**

> **\[GET]** /api/v2.1/admin/address-book/groups/`<parent_department_id>`

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl -X GET \
> -H 'Authorization: Token 60ba962845e8380d25948b95c3c439165fafbff1' \
> 'https://cloud.seatable.io/api/v2.1/admin/address-book/groups/' 
> ```

**Input Parameters**

**parent_department_id** _\[int, optional, `-1` by default]
> The ID of the parent department. If not given, the departments in the root directory (-1) will be returned.

**Return Values**

JSON-object with the list of departments' details.

**Sample Response (200)**

> ```
> {
>     "data": [
>         {
>             "id": 9,
>             "name": "sys-dep-1",
>             "owner": "system admin",
>             "created_at": "2021-02-02T02:10:50+00:00",
>             "parent_group_id": -1,
>             "quota": -2
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

403 Forbidden: The current user doesn't have admin clearance:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```

404 Not Found: The parent department does not exist:
> ```
> {
>     "error_msg": "Group 100 not found."
> }
> ```

## Add A Department

Add a new department with specified name and parent department.

**URL Structure**

> **\[POST]** /api/v2.1/admin/address-book/groups/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token 60ba962845e8380d25948b95c3c439165fafbff1' \
> 'https://cloud.seatable.io/api/v2.1/admin/address-book/groups/' \
> -F 'group_name=sys-dep-1'
> ```

**Input Parameters**

**group_name** _\[str, required]_

> The name of new department.

**parent_group** _\[int, optional, `-1` by default]_

> The ID of parent department.

**Return Values**

JSON-object of the department' details.

**Sample Response (200)**

> ```
> {
>     "id": 9,
>     "name": "sys-dep-1",
>     "owner": "system admin",
>     "created_at": "2021-02-02T02:10:50+00:00",
>     "parent_group_id": -1,
>     "quota": -2
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The current user doesn't have admin clearance:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```

500 Internal Server Error: Probably was the parent department not found:
> ```
> {
>     "error_msg": "Internal Server Error"
> }
> ```

## Get Department Info

Get the information of a certain department with its ID.

**URL Structure**

> **\[GET]** /api/v2.1/admin/address-book/groups/`<group_id>`/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl -X GET \
> -H 'Authorization: Token 60ba962845e8380d25948b95c3c439165fafbff1' \
> 'https://cloud.seatable.io/api/v2.1/admin/address-book/groups/16/?return_ancestors=true'
> ```

**Input Parameters**

**group_id** _\[int, required]_
> The ID of department.

**return_ancestors** _\[enum(`true`, `false`), optional, `false` by default]_
> Indicates whether the ancestor departments should be returned.

**Return Values**

JSON-object with the department's details.

**Sample Response (200)**

> ```
> {
>     "id": 16,
>     "name": "Test department",
>     "owner": "system admin",
>     "created_at": "2021-02-03T03:04:56+00:00",
>     "parent_group_id": 9,
>     "quota": -2,
>     "groups": [],
>     "members": [],
>     "ancestor_groups": [
>         {
>             "id": 9,
>             "name": "sys-dep-1",
>             "owner": "system admin",
>             "created_at": "2021-02-02T02:10:50+00:00",
>             "parent_group_id": -1,
>             "quota": -2
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

403 Forbidden: The current user doesn't have admin clearance:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```

404 Not Found: The queried department does not exist:
> ```
> {
>     "error_msg": "Group 100 not found."
> }
> ```

## Delete A Department

Delete an existing department by its ID.

**URL Structure**

> **\[DELETE]** /api/v2.1/admin/address-book/groups/`<group_id>`/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl -X DELETE \
> -H 'Authorization: Token 60ba962845e8380d25948b95c3c439165fafbff1' \
> 'https://cloud.seatable.io/api/v2.1/admin/address-book/groups/16/'
> ```

**Input Parameters**

**group_id** _\[int, required]_
> The ID of department.


**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```
If the department was not found or already deleted, the same response is returned without error message.

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The current user doesn't have admin clearance:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```


