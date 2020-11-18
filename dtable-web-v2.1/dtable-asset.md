# Dtable Asset

## DTable Asset Exists

**GET** /api/v2.1/workspace/:workspace_id/dtable/:name/asset-exists/

**Request Parameters**

* wordspace_id
* name
* path

**Sample request**

```
curl -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.com/api/v2.1/workspace/1/dtable/t1/asset-exists/?path=files/2020-04/apple.png"

```

**Sample response**

```
{
    "is_exist": true
}

```

**Errors**

* 403 permission denied.
* 404 not found.
* 500 Internal Server Error.

## Zip Asset Files

**POST** /api/v2.1/dtable-asset/:dtable_uuid/zip-task/ 

**Request Params** 	

* **file**: file to export, support multi-files like following example  

**Sample Request **

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/dtable-asset/00390415b6dc416a8f2a70a3a1356a18/zip-task/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' --form 'file=images/2020-04/00000000000000000000000000000011.jpg' --form 'file=images/2020-04/dcced81d4fee390e13e3254c7858da68.jpg' --form 'file=images/2020-06/touxiang.jpg'

```

 Sample Response 

```
{
    "task_id": "1591853930601"
}

```

After request, use task_id to query [task-status](https://docs.seatable.io/published/seatable-api/dtable-web-v2.1/dtable-import-export.md#user-content-Query%20Import/Export%20Status). When it finished, GET following URL to download. 

```
/dtable-export-asset-files/?task_id=:task_id&dtable_uuid=:dtable_uuid

```


