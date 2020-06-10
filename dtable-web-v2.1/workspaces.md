# Workspaces

A workspace is a collection of DTables. It also stores the assets (files and images) of dtables.

## List All Workspaces

**GET **api/v2.1/workspaces/

**Sample request**

```
curl -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' "http://127.0.0.1:8000/api/v2.1/workspaces/"

```

**Sample response**

```
{
    "workspace_list": [
        {
            "repo_id": "a2ae53f1-5c93-459f-a0bc-e36a04b2dc1d",
            "id": 1,
            "owner_name": "one",
            "table_list": [
                {
                    "workspace_id": 1,
                    "uuid": "951b925d-0063-4fd2-96a8-7db3694a286f",
                    "creator": "one",
                    "created_at": "2019-06-25T06:46:43+00:00",
                    "updated_at": "2019-06-25T06:47:49+00:00",
                    "modifier": "one",
                    "id": 3,
                    "name": "he"
                },
                {
                    "workspace_id": 1,
                    "uuid": "b406b9ba-b74e-49c8-aa4e-5567076e5c25",
                    "creator": "one",
                    "created_at": "2019-06-25T06:48:40+00:00",
                    "updated_at": "2019-06-25T07:01:07+00:00",
                    "modifier": "one",
                    "id": 4,
                    "name": "hello"
                }
            ]
        },
        {
            "repo_id": "f6b1d0fe-f467-48e4-9e3d-b6cdb7f558b2",
            "id": 2,
            "owner_name": "group one",
            "table_list": [
                {
                    "workspace_id": 2,
                    "uuid": "3a4f848c-5fc9-4cc8-bbda-96d7d49a944a",
                    "creator": "8",
                    "created_at": "2019-06-25T06:49:28+00:00",
                    "updated_at": "2019-06-25T06:53:20+00:00",
                    "modifier": "one",
                    "id": 5,
                    "name": "testing"
                }
            ]
        }
    ]
}

```

**Errors**

* 403 Permission Denied.
* 500 Internal Server Error.


