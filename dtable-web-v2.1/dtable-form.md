# Forms

## Get a DTable's Forms

**GET** api/v2.1/forms/

**Request parameters**

* workspace_id
* name

**Sample request**

```
curl -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8001/api/v2.1/forms/?workspace_id=1&name=hello"

```

**Sample response**

```
{
    "form_list": [
        {
            "id": 1,
            "username": "1@1.com",
            "workspace_id": 1,
            "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60",
            "form_id": "0KOJ",
            "form_config": "{...}",
            "token": "2571d001-6bab-40ed-a335-173fe398cfe8",
            "form_link": "http://127.0.0.1:8001/dtable/forms/2571d001-6bab-40ed-a335-173fe398cfe8"
        },
        {
            "id": 2,
            "username": "1@1.com",
            "workspace_id": 1,
            "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60",
            "form_id": "1KOJ",
            "form_config": "{...}",
            "token": "d76d7428-ba53-4628-8a5b-2e090d693fbf",
            "form_link": "http://127.0.0.1:8001/dtable/forms/d76d7428-ba53-4628-8a5b-2e090d693fbf"
        }
    ]
}

```

**Errors**

* 400 Bad Request.
* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## Create a DTable Form

**POST** api/v2.1/forms/

**Request parameters**

* workspace_id
* name
* form_id
* form_config

**Sample request**

```
curl -X POST -d 'workspace_id=1&name=hello&form_id=1KOJ&form_config={...}' -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8001/api/v2.1/forms/"

```

**Sample response**

```
{
    "form": {
        "id": 2,
        "username": "1@1.com",
        "workspace_id": "1",
        "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60",
        "form_id": "1KOJ",
        "form_config": "{...}",
        "token": "d76d7428-ba53-4628-8a5b-2e090d693fbf",
        "form_link": "http://127.0.0.1:8001/dtable/forms/d76d7428-ba53-4628-8a5b-2e090d693fbf"
    }
}

```

**Errors**

* 400 Bad Request.
* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## Update a DTable Form

**PUT** api/v2.1/forms/\<token>/

**Request parameters**

* token
* form_config

**Sample request**

```
curl -X PUT -d 'form_config={...}' -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8001/api/v2.1/forms/d76d7428-ba53-4628-8a5b-2e090d693fbf/"

```

**Sample response**

```
{
    "form": {
        "id": 2,
        "username": "1@1.com",
        "workspace_id": "1",
        "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60",
        "form_id": "1KOJ",
        "form_config": "{...}",
        "token": "d76d7428-ba53-4628-8a5b-2e090d693fbf",
        "form_link": "http://127.0.0.1:8001/dtable/forms/d76d7428-ba53-4628-8a5b-2e090d693fbf"
    }
}

```

**Errors**

* 400 Bad Request.
* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## Delete a DTable Form

**DELETE** api/v2.1/forms/\<token>/

**Request parameters**

* token

**Sample request**

```
curl -X DELETE -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8001/api/v2.1/forms/d76d7428-ba53-4628-8a5b-2e090d693fbf/"

```

**Sample response**

```
{
    "success": true
}

```

**Errors**

* 400 Bad Request.
* 403 Permission Denied.
* 500 Internal Server Error.

## Get an Upload Link by a Form Token

**GET** api/v2.1/forms/\<token>/upload-link/

**Sample request**

```
curl http://127.0.0.1:8001/api/v2.1/forms/5ac7517a-6315-410f-ac70-a7e02593faf9/upload-link/

```

**Sample response**

```
{
    "upload_link": "http://127.0.0.1:8082/upload-api/d3f91d16-88e9-494d-8402-78260eb82d65",
    "parent_path": "/asset/a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf"
}

```

**Errors**

* 500 Internal Server Error

## List forms by user

**GET** api/v2.1/forms/

**Request parameters**

* null

**Sample request**

```
curl -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/forms/"

```

**Sample response**

```
{
    "form_list": [
        {
            "id": 18,
            "username": "1ed53263f17645c78dd3f57314051ea0@auth.local",
            "workspace_id": 2,
            "dtable_uuid": "38fd2617961f496595c9c26e201f5d47",
            "form_id": "lzhT",
            "form_config": "{...}",
            "token": "b5c511c7-d011-46b1-9806-7027481e1d0d",
            "form_link": "https://cloud.seatable.io/dtable/forms/b5c511c7-d011-46b1-9806-7027481e1d0d/",
            "share_type": "anonymous",
            "group_name": "群组1",
            "group_id": 1
        },
        {
            "id": 20,
            "username": "1ed53263f17645c78dd3f57314051ea0@auth.local",
            "workspace_id": 1,
            "dtable_uuid": "c18e0ffce1ea4157ae5da32bdb36e676",
            "form_id": "u3QF",
            "form_config": "{...}",
            "token": "95fcefb7-7d6c-4e61-a397-6871611e90a0",
            "form_link": "https://cloud.seatable.io/dtable/forms/95fcefb7-7d6c-4e61-a397-6871611e90a0/",
            "share_type": "anonymous"
        }
    ]
}

```

**Errors**

* 403 Permission Denied.
* 500 Internal Server Error.

## Form share

**POST** api/v2.1/forms/\<token>/share/

**Request parameters**

* token
* share_type
* group_ids

**Sample request**

```
curl -X POST -d 'share_type='group' group_ids=[1, 3, 17]' -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' 
"https://cloud.seatable.io/api/v2.1/forms/d76d7428-ba53-4628-8a5b-2e090d693fbf/share/"

```

**Sample response**

```
{
   "success": true
}

```

**Errors**

* 400 Bad Request.
* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## List shared forms

**GET** api/v2.1/forms/shared/

**Request parameters**

* null

**Sample request**

```
curl -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/forms/shared/"

```

**Sample response**

```
{
    "shared_list": [
        {
            "id": 23,
            "username": "1ed53263f17645c78dd3f57314051ea0@auth.local",
            "workspace_id": 2,
            "dtable_uuid": "38fd2617961f496595c9c26e201f5d47",
            "form_id": "3qq3",
            "form_config": "{...}",
            "token": "04b327f5-10c6-4324-a828-e9ffbea3c9f6",
            "form_link": "https://cloud.seatable.io/dtable/forms/04b327f5-10c6-4324-a828-e9ffbea3c9f6/",
            "share_type": "shared_groups",
            "group_name": "群组1",
            "group_id": 1
        },
        {
            "id": 28,
            "username": "1ed53263f17645c78dd3f57314051ea0@auth.local",
            "workspace_id": 1,
            "dtable_uuid": "c18e0ffce1ea4157ae5da32bdb36e676",
            "form_id": "0DV9",
            "form_config": "{...}",
            "token": "92f35372-0e43-4a90-b978-ef604b0567ce",
            "form_link": "https://cloud.seatable.io/dtable/forms/92f35372-0e43-4a90-b978-ef604b0567ce/",
            "share_type": "shared_groups",
            "group_name": "群组3",
            "group_id": 3
        }
    ]
}

```

**Errors**

* 403 Permission Denied.
* 500 Internal Server Error.


