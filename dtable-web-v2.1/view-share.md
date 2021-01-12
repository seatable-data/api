# View Share

## ToUser Get Shared View‘s Access Token

**GET **/api/v2.1/workspace/:workspace_id/dtable/:dtable_name/user-view-share-access-token/

**Request params**

* user_view_share_id

**Sample request**

```
curl -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/:workspace_id/dtable/:dtable_name/user-view-share-access-token/?user_view_share_id=1

```

**Sample Response (200)**

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1OTE2OTE2OTYsImR0YWJsZV91dWlkIjoiMDJhOWUwMDg2MGYyNGIyYjllNjg0OGQ5NDk4NjlhMGMiLCJ1c2VybmFtZSI6IjZmNDY1ODEwODU4MzQwMTJhYmMwYWQyMGE1ZTg1YjhhQGF1dGgubG9jYWwiLCJwZXJtaXNzaW9uIjoicnciLCJ0YWJsZV9pZCI6IjAwMDAiLCJ2aWV3X2lkIjoiMDAwMCJ9.pDi4oHdfKUeImLacMpASvCX7MOXmjKCFkkrQzDt8xZI",
    "dtable_uuid": "a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf",
    "dtable_server": "https://cloud.seatable.io:5000/",
    "dtable_socket": "https://cloud.seatable.io:5000/"
}

```

## List Shared Views By ToUser

**GET** /api/v2.1/dtables/view-shares-user-shared/

**Sample request**

```
curl -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/dtables/view-shares-user-shared/

```

**Sample Response (200)**

```
{
   "view_share_list":[
      {
         "id":2,
         "dtable_name":"t1",
         "from_user":"f91a9c820b284249b3bb3396dc65bd64@auth.local",
         "from_user_name":"admin",
         "to_user":"6f46581085834012abc0ad20a5e85b8a@auth.local",
         "to_user_name":"a",
         "permission":"rw",
         "table_id":"0000",
         "view_id":"0000",
         "workspace_id":1,
         "color":null,
         "text_color":null,
         "icon":null
      },
      {
         "id":3,
         "dtable_name":"t1",
         "from_user":"f91a9c820b284249b3bb3396dc65bd64@auth.local",
         "from_user_name":"admin",
         "to_user":"6f46581085834012abc0ad20a5e85b8a@auth.local",
         "to_user_name":"a",
         "permission":"rw",
         "table_id":"0000",
         "view_id":"7NgV",
         "workspace_id":1,
         "color":null,
         "text_color":null,
         "icon":null
      }
   ]
}

```

## ToUser Leave Shared Views

**DELETE** /api/v2.1/dtables/view-shares-user-shared/:view_share_id/

**Sample request**

```
curl -X DELETE -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/dtables/view-shares-user-shared/1/

```

**Sample Response (200)**

```
{
  "success": true
}

```

## List Shared Views By FromUser

**GET** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/user-view-shares/

this api default return view shares filter by dtable and from_user. You can add 'table_id', 'view_id', or both too get filterd results.

**Request params**

* workspace_id
* dtable_name
* table_id, optional
* view_id, optional

**Sample request**

```
curl -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/user-view-shares/

```

**Sample Response (200)**

```
{
    "user_view_share_list": [
        {
            "id": 1,
            "dtable_name": "t1",
            "from_user": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
            "from_user_name": "admin",
            "to_user": "6f46581085834012abc0ad20a5e85b8a@auth.local",
            "to_user_name": "a",
            "permission": "rw",
            "table_id": "0000",
            "view_id": "0000"
        }
    ]
}

```

## Add View Share By FromUser

**POST** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/user-view-shares/

**Request params**

* workspace_id
* dtable_name
* permission
* to_user, user email
* table_id
* view_id

**Sample request**

```
curl -X POST -d "permission=rw&to_user=6f46581085834012abc0ad20a5e85b8a@auth.local&table_id=0000&view_id=0000" -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/user-view-shares/

```

**Sample Response (200)**

```
{
    "id": 1,
    "dtable_name": "t1",
    "from_user": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
    "from_user_name": "admin",
    "to_user": "6f46581085834012abc0ad20a5e85b8a@auth.local",
    "to_user_name": "a",
    "permission": "rw",
    "table_id": "0000",
    "view_id": "0000"
}

```

## Update View Share Permission By FromUser

**PUT** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/user-view-shares/10/

**Request params**

* workspace_id
* dtable_name
* user_view_share_id
* permission

**Sample request**

```
curl -X PUT -d "permission=r" -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/user-view-shares/1/

```

**Sample Response (200)**

```
{
    "id": 1,
    "dtable_name": "t1",
    "from_user": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
    "from_user_name": "admin",
    "to_user": "6f46581085834012abc0ad20a5e85b8a@auth.local",
    "to_user_name": "a",
    "permission": "r",
    "table_id": "0000",
    "view_id": "0000"
}

```

## Delete View Share Permission By FromUser

**DELETE** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/user-view-shares/10/

**Request params**

* workspace_id
* dtable_name
* user_view_share_id

**Sample request**

```
curl -X PUT -d "permission=r" -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/view-shares/10/

```

**Sample Response (200)**

```
{
	"success": true
}

```

## Delete all user view shares in a view

**DELETE** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/user-view-shares/﻿

**Request params**

* workspace_id
* dtable_name
* table_id
* view_id

**Sample request**

```
curl -X DELETE -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/user-view-shares/?table_id=0000&view_id=0000

```

**Sample Response (200)**

```
{
	"success": true
}

```

## Delete all group view shares in a view

**DELETE** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/group-view-shares/﻿

**Request params**

* workspace_id
* dtable_name
* table_id
* view_id

**Sample request**

```
curl -X DELETE -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/group-view-shares/?table_id=0000&view_id=0000

```

**Sample Response (200)**

```
{
	"success": true
}

```


