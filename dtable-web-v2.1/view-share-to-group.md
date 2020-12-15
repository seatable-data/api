# View Share to Group

## Group User Get Shared View‘s Access Token

**GET **/api/v2.1/workspace/:workspace_id/dtable/:dtable_name/group-view-share-access-token/

**Request Params**

* group_view_share_id

**Sample request**

```
curl -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/:workspace_id/dtable/:dtable_name/group-view-share-access-token/?group_view_share_id=1

```

**Sample Response (200)**

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1OTE2OTE2OTYsImR0YWJsZV91dWlkIjoiMDJhOWUwMDg2MGYyNGIyYjllNjg0OGQ5NDk4NjlhMGMiLCJ1c2VybmFtZSI6IjZmNDY1ODEwODU4MzQwMTJhYmMwYWQyMGE1ZTg1YjhhQGF1dGgubG9jYWwiLCJwZXJtaXNzaW9uIjoicnciLCJ0YWJsZV9pZCI6IjAwMDAiLCJ2aWV3X2lkIjoiMDAwMCJ9.pDi4oHdfKUeImLacMpASvCX7MOXmjKCFkkrQzDt8xZI",
    "dtable_uuid": "02a9e00860f24b2b9e6848d949869a0c",
    "dtable_server": "https://cloud.seatable.io:5000/",
    "dtable_socket": "https://cloud.seatable.io:5000/"
}

```

## List Shared Views By ToUser

**GET** /api/v2.1/dtables/view-shares-group-shared/

**Sample request**

```
curl -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/dtables/view-shares-group-shared/

```

**Sample Response (200)**

```
{
   "group_shared_views":{
      "27":[
         {
            "id":1,
            "workspace_id":1,
            "uuid":"02a9e008-60f2-4b2b-9e68-48d949869a0c",
            "name":"t1",
            "creator":"admin",
            "modifier":"admin",
            "created_at":"2020-02-20T03:45:13+00:00",
            "updated_at":"2020-04-16T07:05:49+00:00",
            "view_share_id":2,
            "color":null,
            "text_color":null,
            "icon":null
         },
         {
            "id":1,
            "workspace_id":1,
            "uuid":"02a9e008-60f2-4b2b-9e68-48d949869a0c",
            "name":"t1",
            "creator":"admin",
            "modifier":"admin",
            "created_at":"2020-02-20T03:45:13+00:00",
            "updated_at":"2020-04-16T07:05:49+00:00",
            "view_share_id":3,
            "color":null,
            "text_color":null,
            "icon":null
         }
      ]
   }
}

```

## ToUser Leave Shared Views

**DELETE** /api/v2.1/dtables/view-shares-group-shared/:view_share_id/

**Sample request**

```
curl -X DELETE -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/dtables/view-shares-group-shared/1/

```

**Sample Response (200)**

```
{
  "success": true
}

```

## List Shared Views By FromUser

**GET** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/group-view-shares/

this api default return view shares filter by dtable and from_user. You can add 'table_id', 'view_id', or both too get filterd results.

**Request Params**

* workspace_id
* dtable_name
* table_id, optional
* view_id, optional

**Sample request**

```
curl -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/group-view-shares/

```

**Sample Response (200)**

```
{
    "group_view_share_list": [
        {
            "id": 3,
            "dtable_name": "t1",
            "from_user": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
            "from_user_name": "admin",
            "to_group_id": 27,
            "to_group_name": "g1",
            "permission": "rw",
            "table_id": "0000",
            "view_id": "0000"
        },
        {
            "id": 2,
            "dtable_name": "t1",
            "from_user": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
            "from_user_name": "admin",
            "to_group_id": 27,
            "to_group_name": "g1",
            "permission": "rw",
            "table_id": "0000",
            "view_id": "7NgV"
        }
    ]
}

```

## Add View Share By FromUser

**POST** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/group-view-shares/

**Request Params**

* workspace_id
* dtable_name
* permission
* to_group_id
* table_id
* view_id

**Sample request**

```
curl -X POST -d "permission=rw&to_user=6f46581085834012abc0ad20a5e85b8a@auth.local&table_id=0000&view_id=0000" -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/group-view-shares/

```

**Sample Response (200)**

```
{
    "id": 3,
    "dtable_name": "t1",
    "from_user": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
    "from_user_name": "admin",
    "to_group_id": "27",
    "to_group_name": "g1",
    "permission": "rw",
    "table_id": "0000",
    "view_id": "0000"
}

```

## Update View Share Permission By FromUser

**PUT** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/group-view-shares/1/

**Request Params**

* workspace_id
* dtable_name
* group_view_share_id
* permission

**Sample request**

```
curl -X PUT -d "permission=r" -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/group-view-shares/1/

```

**Sample Response (200)**

```
{
    "id": 1,
    "dtable_name": "t1",
    "from_user": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
    "from_user_name": "admin",
    "to_group_id": 27,
    "to_group_name": "g1",
    "permission": "r",
    "table_id": "0000",
    "view_id": "7NgV"
}

```

## Delete View Share Permission By FromUser

**DELETE** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/group-view-shares/1/

**Request Params**

* workspace_id
* dtable_name
* group_view_share_id

**Sample request**

```
curl -X PUT -d "permission=r" -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/group-shares/1/

```

**Sample Response (200)**

```
{
	"success": true
}

```


