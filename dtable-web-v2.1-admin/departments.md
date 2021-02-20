# Departments

## List departments

Admin list all departments.

**URL Structure**

> **\[GET]** api/v2.1/admin/address-book/groups/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl 
> -X GET 'https://cloud.seatable.io/api/v2.1/admin/address-book/groups/' \
> -H 'Authorization: Token 60ba962845e8380d25948b95c3c439165fafbff1'
>
> ```

**Return Values**

JSON-object with the list of departments' details.

**Sample Response (200)**

```
{
    "data": [
        {
            "id": 9,
            "name": "sys-dep-1",
            "owner": "system admin",
            "created_at": "2021-02-02T02:10:50+00:00",
            "parent_group_id": -1,
            "quota": -2
        }
    ]
}

```

## Add a department

Admin add a department.

**URL Structure**

> **\[POST]** /api/v2.1/admin/address-book/groups/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl 
> -X POST 'https://cloud.seatable.io/api/v2.1/admin/address-book/groups/' \
> -H 'Authorization: Token 60ba962845e8380d25948b95c3c439165fafbff1' \
> -F 'group_name=sys-dep-1'
>
> ```

**Input Parameters**

**group_name** _\[str, required]_

> The name of new department.

**parent_group** _\[int, optional_]

> The ID of parent department, default -1.

**Return Values**

JSON-object of the department' details.

**Sample Response (200)**

```
{
    "id": 9,
    "name": "sys-dep-1",
    "owner": "system admin",
    "created_at": "2021-02-02T02:10:50+00:00",
    "parent_group_id": -1,
    "quota": -2
}

```

## Get department info

Admin get department info

**URL Structure**

> **\[GET]** /api/v2.1/admin/address-book/groups/`<group_id>`/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl 
> -X GET 'https://cloud.seatable.io/api/v2.1/admin/address-book/groups/16/?return_ancestors=true' \
> -H 'Authorization: Token 60ba962845e8380d25948b95c3c439165fafbff1'
>
> ```

**Input Parameters**

**group_id** _\[int, required]_

> The ID of department.

**return_ancestors** _\[boolean, optional_]

> Indicates whether return ancestor departments, default false.

**Return Values**

JSON-object of the department' details.

**Sample Response (200)**

```
{
    "id": 16,
    "name": "sys-dep-1-sub-1",
    "owner": "system admin",
    "created_at": "2021-02-03T03:04:56+00:00",
    "parent_group_id": 9,
    "quota": -2,
    "groups": [],
    "members": [],
    "ancestor_groups": [
        {
            "id": 9,
            "name": "sys-dep-1",
            "owner": "system admin",
            "created_at": "2021-02-02T02:10:50+00:00",
            "parent_group_id": -1,
            "quota": -2
        }
    ]
}

```

## Delete a department

Admin delete a department

**URL Structure**

> **DELETE** /api/v2.1/admin/address-book/groups/`<group_id>`/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl -X DELETE 'https://cloud.seatable.io/api/v2.1/admin/address-book/groups/16/' \
> -H 'Authorization: Token 60ba962845e8380d25948b95c3c439165fafbff1'
>
> ```

**Input Parameters**

**group_id** _\[int, required]_

> The ID of department.

**Sample Response (200)**

```
{
    "success": true
}

```


