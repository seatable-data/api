# Users

## List Users

List all the users in the current system.


**URL Structure**

> \[**GET**] /api/v2.1/admin/users/


**Request Authentication**

> Admin Authentication (Token)



**Sample Request**

List two users in the current system:

>```
>curl --request GET \
>--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
>'https://cloud.seatable.io/api/v2.1/admin/users/?page=1&per_page=2' 
>```

**Input Parameters**

**page** _\[numeric, optional, 1 by default]_ 
> Page number of the returned user list.

**per_page** _\[numeric, optional, 25 by default]_
> Number of users displayed on each page.


**Return Values**

JSON-object with the list of users.


**Response Sample**

The response from the sample request lists two users with details, and the returned "total_count" value indicates there are 209 users in the current system:

>```
>{
>    "data": [
>        {
>            "email": "111b8c1666874f15bd5b17afc3527754@auth.local",
>            "name": "admin",
>            "contact_email": "admin@example.com",
>            "login_id": "",
>            "is_staff": true,
>            "is_active": true,
>            "create_time": "2019-11-13T11:07:24+00:00",
>            "last_login": "2020-12-04T16:10:20+00:00",
>            "role": "default",
>            "storage_usage": 2853,
>            "rows_count": 6
>        },
>        {
>            "email": "66ff22ke9f1e4c8d8e1c31415867317c@auth.local",
>            "name": "Daniel",
>            "contact_email": "daniel@example.com",
>            "login_id": "",
>            "is_staff": false,
>            "is_active": true,
>            "create_time": "2019-11-14T02:25:39+00:00",
>            "last_login": "2020-12-03T08:21:22+00:00",
>            "role": "guest",
>            "storage_usage": 1721496,
>            "rows_count": 142
>        }
>    ],
>    "total_count": 209
>}
>```

**Possible Errors**:

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```


## Add A User

Add a user with specified details.


**URL Structure**

> **\[POST]** /api/v2.1/admin/users/


**Request Authentication**

> Admin Authentication (Token)



**Sample Request**

Add a new user with their email address, password and name:
>```
>curl --request POST \
>--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
>'https://cloud.seatable.io/api/v2.1/admin/users/' \
>--form 'email=new-user@seafile.com' \
>--form 'password=123456' \
>--form 'name=New-User'
>```


**Input Parameters**

**email** _\[string,required]_ 
> This is the real email address of the user. SeaTable will save this value as `contact_email`.


**password** _\[string,required]_
> The user's password. Minimum length: 6 characters.


**name** _\[string,required]_ 
> Surname and lastname of the user.


**is_staff** _\[enum(`false`, `true`), optional]_ 
> Determine if the user is a staff:
> * `false` = normal user
> * `true` = user becomes an admin
> * default value is `false`

**is_active** _\[enum(`false`, `true`), optional]_ 
> Determine if the user is added as active:
> * `false` = user is deactivated and can not login
> * `true` = user is activated
> * default value is `true`

**role** _\[string, optional]_ 

> Define the user's role. SeaTable comes with two built-in roles `default` and `guest`, and this can be customized / extended. For more details, refer to the article [Roles and Permissions Support.](https://docs.seatable.io/published/seatable-manual/config/enterprise/roles_permissions.md)


**Return Values**

JSON-object with new user's info and a response `add_user_tip`. The `email` (user's ID in the system) is generated automatically.



**Response Sample**

> ```
> {             
>     "email": "0ef256cb715841dd81b147b2530c2904@auth.local",
>     "name": "New-User",
>     "contact_email": "new-user@example.com",
>     "login_id": "",
>     "is_staff": false,
>     "is_active": true,
>     "create_time": "2020-04-07T07:51:33+00:00",
>     "role": "default",
>     "add_user_tip": "Successfully added user new-user@example.com. An email notification has been sent."
> }
> ```

**Possible Errors**

400 Bad Request: User already exists:
> ```
> {
>     "error_msg": "User existing-user@example.com already exists."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```

## Delete A User

Delete a user permanently.

**URL Structure**

> **\[DELETE]** /api/v2.1/admin/users/`<email>`/


**Request Authentication**

> Admin Authentication (Token)



**Sample Request**

Delete the user with the ID (`email`) `2fca46c0eaa8499cb4aa9871cc7d9560@auth.local`: 

> ```
> curl --request DELETE \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/users/2fca46c0eaa8499cb4aa9871cc7d9560@auth.local/' 
> ```

**Input Parameters**

**email** _\[string, required]_
> The ID of the user (not the email address).

**Return Values**

JSON-object with the result of the operation.


**Sample Response**

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

403 Forbidden: The user doesn't have admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```

404 Not Found: User's ID is not found:
> ```
> {
>     "error_msg": "User 2fca46c0eaa8499cb4aa9871cc7d9560@auth.local not found."
> }
> ```

404 Not Found: User's email address was used instead of ID by mistake:
> ```
> {
>     "error_msg": "User existing-user@example.com not found."
> }
> ```

## Update A User

Update the details of a user, which includes permission, role, row limit etc.


**URL Structure**

> **\[PUT]** /api/v2.1/admin/users/`<email>`/


**Request Authentication**

> Admin Authentication (Token)


**Sample Request**

Update the permission level and the row limit of the user with ID `5bc29d150e874522a2a0563ca2dc5fb4@auth.local`:

> ```
> curl --request PUT \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/users/5bc29d150e874522a2a0563ca2dc5fb4@auth.local/' \
> --form 'is_staff=true' \ 
> --form 'row_limit=10'
> ```


**Input Parameters**

**is_staff** _\[enum(`false`, `true`), optional]_ 
> Set the user as staff or normal:
> * `false` = user becomes normal
> * `true` = user becomes an admin

**is_active** _\[enum(`false`, `true`), optional]_ 
> Set the user as active or inactive:
> * `false` = user is deactivated and can not login
> * `true` = user is activated


**role** _\[string, optional]_ 

> Define the user's role. SeaTable comes with two built-in roles `default` and `guest`, and this can be customized / extended. For more details, refer to the article [Roles and Permissions Support.](https://docs.seatable.io/published/seatable-manual/config/enterprise/roles_permissions.md)


**row_limit** _\[numeric, optional]_
> Set the new limit of rows.


**asset_quota_mb** _\[numeric, optional]_
> Set the limit of user's asset quota in Mb


**Return Values**

JSON-object with the updated details as well as an `update_status_tip`.


**Response Sample**

> ```
> {
>     "email": "5bc29d150e874522a2a0563ca2dc5fb4@auth.local",
>     "name": "Max Teamleader",
>     "contact_email": "teamleader@example.de",
>     "login_id": "",
>     "is_staff": true,
>     "is_active": true,
>     "org_id": 999,
>     "org_name": "Beef Test",
>     "create_time": "2020-11-06T09:36:39+00:00",
>     "role": "default",
>     "update_status_tip": "Edit succeeded, an email has been sent."
> }
> ```

**Possible Errors**

400 Bad Request: The given parameter was not valid:
> ```
> {
>     "error_msg": "role must be in ['default', 'guest']."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```

404 Not Found: The user's ID was not found:
> ```
> {
>     "error_msg": "User 26815cfaf1154efba122f92359f4e581@auth.local not found."
> }
> ```

404 Not Found: User's email address was used instead of ID by mistake:
> ```
> {
>     "error_msg": "User existing-user@example.com not found."
> }
> ```

## Reset Password

**PUT** api/v2.1/admin/users/:email/reset-password/

**Request Sample**

```
curl --request PUT 'https://cloud.seatable.io/api/v2.1/admin/users/5a96afda39ec4bf4805d884588d44f7f@auth.local/reset-password/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Response Sample**

```
{
    "new_password": "sC8INE9MdW",
    "reset_tip": "Successfully reset password to sC8INE9MdW, an email has been sent to None."
}

```

**Errors**

* **403**: Permission Denied.
* **404**: User Not Found.
* **500**: Internal Server Error.

## List Admin Users

**GET** api/v2.1/admin/admin-users/

**Request Sample**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/admin/admin-users/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Response Sample**

```
{
    "admin_user_list": [
        {
            "email": "test@seafiletest.com",
            "name": "test",
            "contact_email": null,
            "login_id": "",
            "is_staff": true,
            "is_active": true,
            "create_time": "2019-11-04T02:23:22+00:00",
            "last_login": "2020-03-06T09:49:59+00:00",
            "admin_role": "default_admin"
        },
        {
            "email": "admin@seafiletest.com",
            "name": "admin",
            "contact_email": "admin@seafiletest.com",
            "login_id": "",
            "is_staff": true,
            "is_active": true,
            "create_time": "2019-11-04T02:24:40+00:00",
            "last_login": "2020-04-07T03:51:51+00:00",
            "admin_role": "default_admin"
        }
    ]
}

```

**Errors**

* **403**: Permission Denied.
* **500**: Internal Server Error.


