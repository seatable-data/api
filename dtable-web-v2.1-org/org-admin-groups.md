# Org admin groups

## Add a group

POST api/v2.1/org/{org_id}/admin/groups/ 

**Request Params**

* **group_name:** group name
* **group_owner:** group owner

**Request Sample**

```
curl --request POST "https://cloud.seatable.io/api/v2.1/org/4/admin/groups/" --header 'Authorization: Token b6720d34395851f7bada7d86d8f121936b727391' --form 'group_name=Microsoft' --form 'group_owner=7c1d2ea7cc15425889d557e0c99efcf3@auth.local'

```

**Response Sample**

```
{
	"id": 23,
	"group_name": "Microsoft",
	"ctime": "2020-11-20T10:28:22+00:00",
	"creator_email": "7c1d2ea7cc15425889d557e0c99efcf3@auth.local",
	"creator_name": "yufeng1",
	"creator_contact_email": "yufeng1@qq.com"
}

```

**Errors**

* 400 Bad Request.
* 403 Permission Denied.
* 404 Not Found.
* 500 Internal Server Error.

## List members of a group

 GET api/v2.1/org/{org_id}/admin/groups/{group_id}/members/

**Request Sample**

```
curl --request GET "https://cloud.seatable.io/api/v2.1/org/4/admin/groups/19/members/" --header 'Authorization: Token b6720d34395851f7bada7d86d8f121936b727391' 

```

**Response Sample**

```none
{
    "group_id": 19,
    "group_name": "web deploy",
    "members": [
        {
            "group_id": 19,
            "name": "ORG_ADMIN",
            "email": "bf3d4645e57346a6bc061929f2715b81@auth.local",
            "contact_email": "super_org@admin.com",
            "login_id": "",
            "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
            "is_admin": false,
            "role": "Member"
        },
        {
            "group_id": 19,
            "name": "yufeng1",
            "email": "7c1d2ea7cc15425889d557e0c99efcf3@auth.local",
            "contact_email": "yufeng1@qq.com",
            "login_id": "",
            "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
            "is_admin": true,
            "role": "Admin"
        },
        {
            "group_id": 19,
            "name": "yufeng",
            "email": "5f11c0e0b9ba4c50b5ecc1f231a6ea1d@auth.local",
            "contact_email": "r350178982@163.com",
            "login_id": "",
            "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
            "is_admin": true,
            "role": "Owner"
        }
    ]
}

```

**Errors**

* 400 Bad Request.
* 403 Permission Denied.
* 404 Not Found.
* 500 Internal Server Error.

## Batch add members to a group

POST api/v2.1/org/{org_id}/admin/groups/{group_id}/members/

**Request Params**

* **email**: menber's email, multiple

**Request Sample**

```
curl --request POST "https://cloud.seatable.io/api/v2.1/org/4/admin/groups/19/members/" --header 'Authorization: Token b6720d34395851f7bada7d86d8f121936b727391' --form 'email=7c1d2ea7cc15425889d557e0c99efcf3@auth.local' --form 'email=5f11c0e0b9ba4c50b5ecc1f231a6ea1d@auth.local' --form 'email=dfc3bfdf9aa9451bb544428fc8486fc4@auth.local' 

```

**Response Sample**

```none
{
    "failed": [
        {
            "email": "7c1d2ea7cc15425889d557e0c99efcf3@auth.local",
            "error_msg": "User yufeng1 is already a group member."
        },
        {
            "email": "5f11c0e0b9ba4c50b5ecc1f231a6ea1d@auth.local",
            "error_msg": "User yufeng is already a group member."
        }
    ],
    "success": [
        {
            "group_id": 19,
            "name": "yufeng2",
            "email": "dfc3bfdf9aa9451bb544428fc8486fc4@auth.local",
            "contact_email": "yufeng2@1.com",
            "login_id": "",
            "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
            "is_admin": false,
            "role": "Member"
        },
    ]
}

```

**Errors**

* 400 Bad Request.
* 403 Permission Denied.
* 404 Not Found.
* 500 Internal Server Error.

## Manage member of a group

PUT api/v2.1/org/{org_id}/admin/groups/{group_id}/members/{member_email}/ 

**Request Params**

* **is_admin**: 'true' of 'false'

**Request Sample**

```
curl --request PUT "https://cloud.seatable.io/api/v2.1/org/4/admin/groups/19/members/dfc3bfdf9aa9451bb544428fc8486fc4@auth.local/" --header 'Authorization: Token b6720d34395851f7bada7d86d8f121936b727391' --form 'is_admin=true'

```

**Response Sample**

```
{
    "group_id": 19,
    "name": "yufeng2",
    "email": "dfc3bfdf9aa9451bb544428fc8486fc4@auth.local",
    "contact_email": "yufeng2@1.com",
    "login_id": "",
    "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
    "is_admin": true,
    "role": "Admin"
}

```

**Errors**

* 400 Bad Request.
* 403 Permission Denied.
* 404 Not Found.
* 500 Internal Server Error.

## Delete member of a group

DELETE api/v2.1/org/{org_id}/admin/groups/{group_id}/members/{member_email}/ 

**Request Sample**

```
curl --request DELETE "https://cloud.seatable.io/api/v2.1/org/4/admin/groups/19/members/dfc3bfdf9aa9451bb544428fc8486fc4@auth.local/" --header 'Authorization: Token b6720d34395851f7bada7d86d8f121936b727391' 

```

**Response Sample**

```none
{
    "success": true
}

```

**Errors**

* 403 Permission Denied.
* 404 Not Found.
* 500 Internal Server Error.


