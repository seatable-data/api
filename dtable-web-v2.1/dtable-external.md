# dtable-external

## Download DTable Through External Link

**get** dtable/external-links/\<token>/download-zip/

**Request parameters**

* token, external link token

**Sample request**

```
curl GET -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' -H "Content-Type: multipart/form-data" https://cloud.seatable.io/dtable/external-links/8720e55e17a44aa89990/download-zip/

```

**Sample response**

xxx.dtable zip file

## Copy a DTable from an External Link

POST /api/v2.1/dtable-external-link/dtable-copy/

**Request form data**

* **link**: an external link, required
* **dst_workspace_id**: target workspace id, required

**Request Sample**

```
curl -X POST \
  https://cloud.seatable.io/api/v2.1/dtable-external-link/dtable-copy/ \
  -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' \
  -H 'postman-token: a77f88a9-ab23-028c-67bc-aa1f61ef87cb' \
  -F link=http://127.0.0.1:8000/dtable/external-links/0ada5e1226d343c4a71a/ \
  -F dst_workspace_id=77

```

**Response Sample**

```
{
    "dtable": {
        "id": 226,
        "workspace_id": 77,
        "uuid": "fb62ed48-37ac-45b8-925f-bb00790ac6fe",
        "name": "first",
        "creator": "Big Boss",
        "modifier": "Big Boss",
        "created_at": "2020-03-06T01:36:31+00:00",
        "updated_at": "2020-03-06T01:36:31+00:00"
    }
}

```

**Errors**

* 404 Not Found.
* 403 Permission Denied.
* 500 Internal Server Error.




