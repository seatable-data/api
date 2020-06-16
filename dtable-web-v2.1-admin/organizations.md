# Organizations

## List Organizations

**GET** api/v2.1/admin/organizations/

**Request Params**

* **page**: page number, default 1
* **per_page**: the number of users per page, default 25

**Request Sample**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/admin/organizations/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Response Sample**

```
{
    "organizations": [
        {
            "org_id": 1,
            "org_name": "org",
            "ctime": "2020-01-11T07:58:25+00:00",
            "org_url_prefix": "org_icveztvq1k9gfo9olksp",
            "role": "org_default",
            "creator_email": "cf7c011380904d1b8beeeaad5234eb0c@auth.local",
            "creator_name": "456",
            "creator_contact_email": "456@qq.com",
            "quota": -2,
            "storage_usage": 1426,
            "max_user_number": 5
        },
        {
            "org_id": 2,
            "org_name": "org-test",
            "ctime": "2020-05-20T03:36:12+00:00",
            "org_url_prefix": "org_0hht0tv6dmy2ibv6rhop",
            "role": "org_default",
            "creator_email": "585dd653ccbf4552ba69c3f04e6be2b6@auth.local",
            "creator_name": "321org",
            "creator_contact_email": "321@qq.com",
            "quota": -2,
            "storage_usage": 0,
            "max_user_number": 5
        }
    ],
    "count": 2
}

```

**Errors**:

* **400**: Bad Request.
* **500**: Internal Server Error.

## Add Organization

**POST** api/v2.1/admin/organizations/

**Request Params**

* **org_name:** org's name, required
* **admin_email**: org admin's email, required
* **admin_name**: org admin's name, optional
* **password**: the org admin's password, required

**Request Sample**

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/admin/organizations/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
--form 'org_name=org-for-add' \
--form 'admin_email=for-add@seafile.com' \
--form 'admin_name=for-add' \
--form 'password=123'

```

**Response Sample**

```
{
    "org_id": 3,
    "org_name": "org-for-add",
    "ctime": "2020-05-20T03:36:12+00:00",
    "org_url_prefix": "org_0hht0tv6dmy2ibv6rhop",
    "role": "org_default",
    "creator_email": "585dd653ccbf4552ba69c3f04e6be2b6@auth.local",
    "creator_name": "for-add",
    "creator_contact_email": "for-add@seafile.com",
    "quota": -2,
    "storage_usage": 0,
    "max_user_number": 5
}

```

**Errors**

* **400**: Bad Requst.
* **403**: Permission Denied.
* **500**: Internal Server Error.

## Delete Organization

**DELETE** api/v2.1/admin/organizations/:org_id/

**Request Sample**

```
curl --request DELETE 'https://cloud.seatable.io/api/v2.1/admin/organizations/3/' \
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

## Update Organization

**PUT** api/v2.1/admin/organizations/:org_id/

**Request Params**

* **org_name**: org name, optional
* **max_user_number**: max user number, optional
* **role**: role of organization, optional
* **row_limit**: the limit of tables' row, optional
* **asset_quota_mb**: the limit of user's asset quota in Mb, optional

**Request Sample**

```
curl --request PUT 'https://cloud.seatable.io/api/v2.1/admin/organizations/1/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
--form 'org_name=rename-org' \
--form 'role=guest' \
--form 'row_limit=100'

```

**Response Sample**

```
{
    "org_id": 1,
    "org_name": "rename-org",
    "ctime": "2020-01-11T07:58:25+00:00",
    "org_url_prefix": "org_icveztvq1k9gfo9olksp",
    "role": "guest",
    "creator_email": "cf7c011380904d1b8beeeaad5234eb0c@auth.local",
    "creator_name": "456",
    "creator_contact_email": "456@qq.com",
    "quota": -2,
    "storage_usage": 1426,
    "max_user_number": 5,
    "rows_count":34,
    "row_limit":100,
}

```

**Errors**

* **400**: Bad Requst.
* **403**: Permission Denied.
* **404**: User Not Found.
* **500**: Internal Server Error.


