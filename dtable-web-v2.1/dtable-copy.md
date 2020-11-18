# DTable copy

## Copy a dtable from a workspace

**POST** /api/v2.1/dtable-copy/

**Request form data**

* **src_workspace_id**: source workspace id, int, required
* **dst_workspace_id**: destination workspace, int, required
* **name**: source table name

**Request sample**

```
curl -X POST https://cloud.seatable.io/api/v2.1/dtable-copy/ -H 'authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' -F src_workspace_id=1 -F name=test-dtable -F dst_workspace_id=80

```

**Response sample**

```
{
    "dtable":{
        "id":978,
        "workspace_id":80,
        "uuid":"9e214427-cddd-425a-bc11-1dcbba93ebcd",
        "name":"test-dtable",
        "creator":"foo",
        "modifier":"foo",
        "created_at":"2020-10-27T16:08:46+08:00",
        "updated_at":"2020-10-27T16:08:46+08:00",
        "color":null,
        "text_color":null,
        "icon":null
    }
}

```

**Errors**

* **400**: Bad Request
* **403**: Permission denied
* **500**: Internal Server Error

## Copy a dtable from external link

**POST** /api/v2.1/dtable-external-link/dtable-copy/

**Request form data**

* **link**: external link, string, required
* **dst_workspace_id**: destination workspace, int, required

**Request sample**

```
curl -X POST https://cloud.seatable.io/api/v2.1/dtable-external-link/dtable-copy/ -H 'authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' -F link='https://cloud.seatable.io/dtable/external-links/6be92845836f41febafe/' -F dst_workspace_id=80

```

**Response sample**

```
{
    "dtable":{
        "id":978,
        "workspace_id":80,
        "uuid":"9e214427-cddd-425a-bc11-1dcbba93ebcd",
        "name":"test-dtable",
        "creator":"foo",
        "modifier":"foo",
        "created_at":"2020-10-27T16:08:46+08:00",
        "updated_at":"2020-10-27T16:08:46+08:00",
        "color":null,
        "text_color":null,
        "icon":null
    }
}

```

**Errors**

* **400**: Bad Request
* **403**: Permission denied
* **500**: Internal Server Error


