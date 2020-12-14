# Workspaces

A workspace is a collection of DTables. It also stores the assets (files and images) of dtables.

## Get Workspaces detail

**GET** /api/v2.1/workspaces/

**Request parameters**

* detail: 'true' or 'false', default 'true'

**Sample request**

```
curl -H 'Authorization: Token 6e44903481adbe2c404bb075a6d4ac6be00a44b4' -H 'Accept: application/json; charset=utf-8; indent=4' 'http://127.0.0.1:8001/api/v2.1/workspaces/'

```

**Sample response**

detail=false

```
{
    "workspace_list": [
        {
            "id": "",
            "name": "starred",
            "type": "starred"
        },
        {
            "id": "",
            "name": "shared",
            "type": "shared"
        },
        {
            "id": 1,
            "name": "personal",
            "type": "personal"
        },
        {
            "id": 5,
            "name": "my group",
            "type": "group"
        }
    ]
}

```

detail=true

```
{
    "workspace_list": [
        {
            "id": "",
            "name": "starred",
            "type": "starred",
            "table_list": [
                {
                    "id": 3,
                    "workspace_id": 5,
                    "uuid": "64155cad-ee23-4752-9f56-1773ddc15d92",
                    "name": "nice",
                    "creator": "Alex",
                    "modifier": "Alex",
                    "created_at": "2019-12-28T01:56:08+08:00",
                    "updated_at": "2019-12-28T01:56:08+08:00",
                    "color": null,
                    "text_color": null,
                    "icon": null,
                    "starred": true
                }
            ]
        },
        {
            "id": "",
            "name": "shared",
            "type": "shared",
            "shared_table_list": [
                {
                    "id": 2,
                    "workspace_id": 2,
                    "uuid": "3af86401-f477-4fd4-b9b5-bda49e6a5238",
                    "name": "good",
                    "creator": "Bob",
                    "modifier": "Bob",
                    "created_at": "2019-11-30T07:58:04+08:00",
                    "updated_at": "2020-03-30T06:35:03+08:00",
                    "color": null,
                    "text_color": null,
                    "icon": null,
                    "from_user": "2@2.com",
                    "permission": "rw",
                    "from_user_avatar": "http://127.0.0.1:8001/media/avatars/1/e/6fd8e56879c84999cd481255530592/resized/80/1ae78cb64ba5442c2929247926af0e6f.png",
                    "from_user_name": "Bob",
                    "starred": false
                }
            ],
            "shared_view_list": [
                {
                    "id": 1,
                    "dtable_name": "nice",
                    "from_user": "2@2.com",
                    "from_user_name": "Bob",
                    "to_user": "1@1.com",
                    "to_user_name": "Alex",
                    "permission": "rw",
                    "table_id": "0000",
                    "view_id": "0000",
                    "from_user_avatar": "http://127.0.0.1:8001/media/avatars/1/e/6fd8e56879c84999cd481255530592/resized/80/1ae78cb64ba5442c2929247926af0e6f.png",
                    "workspace_id": 2,
                    "color": null,
                    "text_color": null,
                    "icon": null
                }
            ]
        },
        {
            "id": 1,
            "name": "personal",
            "type": "personal",
            "table_list": [
                {
                    "id": 1,
                    "workspace_id": 1,
                    "uuid": "46620d70-c8e5-49ab-8874-9d4a2dc4608c",
                    "name": "hello",
                    "creator": "Alex",
                    "modifier": "Alex",
                    "created_at": "2020-02-26T03:34:08+08:00",
                    "updated_at": "2020-11-28T04:03:09+08:00",
                    "color": "#FF8000",
                    "text_color": null,
                    "icon": "icon-worksheet",
                    "starred": false
                },
                {
                    "id": 216,
                    "workspace_id": 1,
                    "uuid": "35484f72-3973-4a6d-9515-81d18a8c3b64",
                    "name": "Vlogger Bibliothek",
                    "creator": "Alex",
                    "modifier": "Alex",
                    "created_at": "2020-11-28T05:06:29+08:00",
                    "updated_at": "2020-11-28T05:06:29+08:00",
                    "color": null,
                    "text_color": null,
                    "icon": null,
                    "starred": false
                }
            ]
        },
        {
            "id": 5,
            "name": "\u6211\u7684\u7fa4\u7ec4",
            "type": "group",
            "group_id": 22,
            "group_owner": "1@1.com",
            "group_admins": [
                "1@1.com",
                "2@2.com"
            ],
            "group_member_count": 2,
            "table_list": [
                {
                    "id": 3,
                    "workspace_id": 5,
                    "uuid": "64155cad-ee23-4752-9f56-1773ddc15d92",
                    "name": "nice",
                    "creator": "Alex",
                    "modifier": "Alex",
                    "created_at": "2019-12-28T01:56:08+08:00",
                    "updated_at": "2019-12-28T01:56:08+08:00",
                    "color": null,
                    "text_color": null,
                    "icon": null,
                    "starred": true
                }
            ],
            "group_shared_dtables": [
                {
                    "id": 1,
                    "workspace_id": 1,
                    "uuid": "46620d70-c8e5-49ab-8874-9d4a2dc4608c",
                    "name": "hello",
                    "creator": "Alex",
                    "modifier": "Alex",
                    "created_at": "2020-02-26T03:34:08+08:00",
                    "updated_at": "2020-11-28T04:03:09+08:00",
                    "color": "#FF8000",
                    "text_color": null,
                    "icon": "icon-worksheet",
                    "starred": false
                }
            ],
            "group_shared_views": [
                {
                    "id": 216,
                    "workspace_id": 1,
                    "uuid": "35484f72-3973-4a6d-9515-81d18a8c3b64",
                    "name": "Vlogger Bibliothek",
                    "creator": "Alex",
                    "modifier": "Alex",
                    "created_at": "2020-11-28T05:06:29+08:00",
                    "updated_at": "2020-11-28T05:06:29+08:00",
                    "color": null,
                    "text_color": null,
                    "icon": null,
                    "view_share_id": 1
                }
            ]
        }
    ]
}

```

**Errors**

* 400 Bad Request
* 500 Internal Server Error


