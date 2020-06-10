# Attachment

## Get DTable Attachment Upload Link

**GET **/api/v2.1/workspace/\<workspace_id>/dtable-asset-upload-link/?name=

* workspace_id
* name: the dtable name

**Sample request**

```
curl -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/1/dtable-asset-upload-link/?name=hello"

```

**Sample response**

```
{
    "parent_path": "/asset/f55180b6-8226-4746-b3fe-5bcd8c4108bc",
    "upload_link": "https://cloud.seatable.io/upload-api/d727507a-63e6-41de-aa52-c44ac0f21de8"
}

```

**Errors**

* 400 Bad Request.
* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## List DTable Asset Directories And Files

**GET** /api/v2.1/dtable-asset/:dtable_uuid/

**Request parameters**

* parent_dir: the path to list, default '/', optional

**Request Sample**

```
curl -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' 'https://cloud.seatable.io/api/v2.1/dtable-asset/e76bc522-a82d-4b74-9bf1-bfb01416d090/?parent_dir=/files/2020-03'

```

**Response Sample**

```
{
    "dirent_list": [
        {
            "is_file": true,
            "obj_name": "fb_2018-03-01.csv",
            "file_size": 1201,
            "last_update": "2020-03-02T03:06:16+00:00"
        },
        {
            "is_file": true,
            "obj_name": "xsy95830@qq.com-2018-05-15.csv",
            "file_size": 133,
            "last_update": "2020-03-02T03:05:08+00:00"
        }
    ]
}

```

**Errors**

* 400 Bad Request.
* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.

## Delete DTable Asset

**DELETE**  /api/v2.1/dtable-asset/:dtable_uuid/

**Request parameters**

* name: file/dir name
* parent_path: where file/dir is in

**Request Sample**

```
curl -X DELETE -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; indent=4' 'https://cloud.seatable.io/api/v2.1/dtable-asset/2e1fb433-836c-4a14-9d94-80d3ce7cfeac/?parent_path=/&name=files'

```

**Response Sample**

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

## Rotate Image

**POST** /api/v2.1/workspace/:workspace_id/dtable/:dtable_name/rotate-image/

**Request parameters**

* path: image path, like path in dtable's `asset` url, required
* angle: rotate angle, there are options 90 180 270 , mean rotate degrees counterclockwise, required

**Request Sample**

```
curl -X POST -H 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' -H 'Accept: application/json; indent=4' 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/first/rotate-image/' -F 'angle=90' -F 'path=images/2020-03/吐.png'

```

**Response Sample**

```
{
    "success": true
}

```

**Errors**

* **400** Bad Request.
* **403** Permission denied.
* **404** Workspace/Table/Asset not found.
* **500** Internal Server Error.


