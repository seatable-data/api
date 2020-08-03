# Common Dataset

## List common dataset a user can access

**GET** api/v2.1/dtable/common-datasets/

**Sample request**

```
curl -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/dtable/common-datasets/"

```

**Sample response**

```json
{
    "dataset_list": [
        {
            "id": 26,
            "org_id": -1,
            "dtable_uuid": "32b1e77a-3a4f-45fa-b420-6c231b20d4d2",
            "table_id": "0000",
            "view_id": "0000",
            "created_at": "2020-07-13T09:01:20+00:00",
            "creator": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
            "dataset_name": "w2",
            "can_manage": true
        }
    ]
}

```

## List common dataset a base can access

**GET** api/v2.1/dtable/common-datasets/

**Request parameters**

* dst_dtable_uuid

**Sample request**

```
curl -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/dtable/common-datasets/?dst_dtable_uuid=32b1e77a3a4f45fab4206c231b20d4d2"

```

**Sample response**

```json
{
    "dataset_list": [
        {
            "id": 26,
            "org_id": -1,
            "dtable_uuid": "32b1e77a-3a4f-45fa-b420-6c231b20d4d2",
            "table_id": "0000",
            "view_id": "0000",
            "created_at": "2020-07-13T09:01:20+00:00",
            "creator": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
            "dataset_name": "w2",
            "can_manage": true
        }
    ]
}

```

## Publish a common dataset from a view

**POST** api/v2.1/dtable/common-datasets/

**Request parameters**

* dataset_name
* workspace_id
* dtable_name
* table_name
* view_name

**Sample request**

```
curl -H -X POST -d 'dataset_name=test1&workspace_id=1&dtable_name=t1&table_name=Table1&view_name=test_view' 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/dtable/common-datasets/"

```

**Sample response**

```json
{
    "id": 26,
    "org_id": -1,
    "dtable_uuid": "32b1e77a-3a4f-45fa-b420-6c231b20d4d2",
    "table_id": "0000",
    "view_id": "0000",
    "created_at": "2020-07-13T09:01:20+00:00",
    "creator": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
    "dataset_name": "test1",
}

```

## Get contents of a common dataset

**GET** api/v2.1/dtable/common-datasets/:dataset_id/

**Sample request**

```
curl -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/dtable/common-datasets/26/"

```

**Sample response**

```json
{
    "rows": [
        {
            "_id": "Sn7svBUYTTmup7WuMsJhGw",
            "Name": "11"
        }
    ],
    "columns": [
        {
            "key": "0000",
            "name": "Name",
            "type": "text",
            "width": 200,
            "editable": true,
            "resizable": true
        }
    ],
    "related_user_list": [
        {
            "email": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
            "name": "admin",
            "contact_email": "foo@foo.com",
            "avatar_url": "http://127.0.0.1:8000/media/avatars/default.png"
        }
    ]
}

```

## Delete a common dataset

**DELETE** api/v2.1/dtable/common-datasets/:dataset_id/

**Sample request**

```
curl -X DELETE 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/dtable/common-datasets/26/"

```

**Sample response**

```json
{
    "success": true
}

```

## Import a common dataset

**POST** api/v2.1/dtable/common-datasets/:dataset_id/import/

**required params**

* dataset_id, target dataset you want to import
* dst_dtable_uuid, destination dtable uuid

**sample request**

```
curl -X POST -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "http://cloud.seatable.io/api/v2.1/dtable/common-datasets/:dataset_id/import/?dst_dtable_uuid=fb2f26130f604bada1b6c8665479ba7c"

```

**sample response**

```
{
    "success": true
}

```

## Sync imported common dataset

**POST** api/v2.1/dtable/common-datasets/:dataset_id/sync/

**required params**

* dataset_id, target dataset you want to import
* dst_dtable_uuid, destination dtable uuid
* dst_table_id, e.g. "JU8K"

**sample request**

```
curl -X POST -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "http://cloud.seatable.io/api/v2.1/dtable/common-datasets/:dataset_id/import/?dst_dtable_uuid=fb2f26130f604bada1b6c8665479ba7c&is_sync=true&dst_table_id=JU8K&dst_view_id=0000"

```

**sample response**

```
{
    "success": true
}

```

## List common dataset sync record

**GET** api/v2.1/dtable/common-datasets/syncs/

**required params**

* dst_dtable_uuid, destination dtable uuid

**sample request**

```
curl -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "http://cloud.seatable.io/api/v2.1/dtable/common-datasets/?dst_dtable_uuid=fb2f26130f604bada1b6c8665479ba7c

```

**sample response**

```
{
    "dataset_sync_list": [
        {
            "id": 1,
            "dataset_id": 5,
            "dst_dtable_uuid": "fb2f2613-0f60-4bad-a1b6-c8665479ba7c",
            "dst_table_id": "6vBH",
            "created_at": "2020-05-19T03:15:11+00:00",
            "creator": "f91a9c820b284249b3bb3396dc65bd64@auth.local",
            "last_sync_time": "2020-05-19T03:15:11+00:00"
        }
    ]
}

```


