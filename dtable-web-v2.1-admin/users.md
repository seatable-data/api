# Users

## List Users

**GET** api/v2.1/admin/users/

**Request Params**

* **page**: page number, default 1
* **per_page**: the number of users per page, default 25

**Request Sample**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/admin/users/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Response Sample**

```
{
    "data": [
        {
            "email": "xiongchao.cheng@seafile.com",
            "name": "cheng",
            "contact_email": "xiongchao.cheng@seafile.com",
            "login_id": "",
            "is_staff": true,
            "is_active": true,
            "create_time": "2019-10-31T07:50:32+00:00",
            "last_login": "2020-04-07T08:35:07+00:00",
            "role": "default",
            "storage_usage": 0
        },
        {
            "email": "test@seafiletest.com",
            "name": "test",
            "contact_email": null,
            "login_id": "",
            "is_staff": true,
            "is_active": true,
            "create_time": "2019-11-04T02:23:22+00:00",
            "last_login": "2020-03-06T09:49:59+00:00",
            "role": "default",
            "storage_usage": 0
        }
    ],
    "total_count": 2
}

```

**Errors**:

* **400**: Bad Request.
* **500**: Internal Server Error.

## Add User

**POST** api/v2.1/admin/users/

**Request Params**

* **email**: user's email, required
* **name**: user's name
* **is_staff**: whether is an admin user, default false
* **is_active**: whether the user is active, default true
* **role**: the user's role, default None meaning default role
* **password**: the user's password

**Request Sample**

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/admin/users/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
--form 'email=for-add@seafile.com' \
--form 'password=123' \
--form 'name=for-add'

```

**Response Sample**

```
{
    "email": "0ef256cb715841dd81b147b2530c2904@auth.local",
    "name": "for-add",
    "contact_email": "for-add@seafile.com",
    "login_id": "",
    "is_staff": false,
    "is_active": true,
    "create_time": "2020-04-07T07:51:33+00:00",
    "role": "default",
    "add_user_tip": "Successfully added user for-add@seafile.com. An email notification has been sent."
}

```

**Errors**

* **400**: Bad Requst.
* **403**: Permission Denied.
* **500**: Internal Server Error.

## Delete User

**DELETE** api/v2.1/admin/users/:email/

**Request Sample**

```
curl --request DELETE 'https://cloud.seatable.io/api/v2.1/admin/users/0ef256cb715841dd81b147b2530c2904@auth.local/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Response Sample**

```
{
    "success": true
}

```

**Errors**

* **403**: Permission Denied.
* **404**: User Not Found.
* **500**: Internal Server Error.

## Update User

**PUT** api/v2.1/admin/users/:email/

**Request Params**

* **is_staff**: whether is an admin user, optional
* **is_active**: whether the user is active, optional
* **role**: the user's role, optional

**Request Smaple**

```
curl --request PUT 'https://cloud.seatable.io/api/v2.1/admin/users/5bc29d150e874522a2a0563ca2dc5fb4@auth.local/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
--form 'is_staff=true'

```

**Response Sample**

```
{
    "email": "5bc29d150e874522a2a0563ca2dc5fb4@auth.local",
    "name": "for-add",
    "contact_email": "for-add@seafile.com",
    "login_id": "",
    "is_staff": true,
    "is_active": true,
    "create_time": "2020-04-07T10:46:41+00:00",
    "role": "default",
    "update_status_tip": ""
}

```

**Errors**

* **400**: Bad Requst.
* **403**: Permission Denied.
* **404**: User Not Found.
* **500**: Internal Server Error.

## Reset Password

**PUT** api/v2.1/admin/users/:email/reset-password/

**Request Sample**

```
curl --request PUT 'https://cloud.seatable.io/api/v2.1/admin/users/5a96afda39ec4bf4805d884588d44f7f@auth.local/reset-password/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

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
curl --request GET 'https://cloud.seatable.io/api/v2.1/admin/admin-users/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

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


