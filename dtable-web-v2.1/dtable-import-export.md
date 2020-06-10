# dtable-import-export

## Import DTable

**POST** api/v2.1/workspace/\<workspace_id>/import-dtable/

**Request parameters**

* workspace_id
* dtable, xxx.dtable zip file

**Sample request**

```
curl -X POST -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' -H "Content-Type: multipart/form-data" -F "dtable=@/home/t1.dtable" https://cloud.seatable.io/api/v2.1/workspace/1/import-dtable/

```

**Sample response**

```
{
   "task_id":"1582970303923",
   "table":{
      "id":87,
      "workspace_id":22,
      "uuid":"d09b6bcc-b6e5-4b8c-b9e2-c4329a8af482",
      "name":"t1",
      "creator":"a",
      "modifier":"a",
      "created_at":"2020-02-29T09:58:23+00:00",
      "updated_at":"2020-02-29T09:58:23+00:00"
   }
}

```

## Import DTable (From *.csv)

**POST** api/v2.1/workspace/\<workspace_id>/import-dtable/

**Request parameters**

* workspace_id
* dtable, xxx.csv file

**Sample request**

```
curl -X POST -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' -H "Content-Type: multipart/form-data" -F "dtable=@/home/t1.csv" https://cloud.seatable.io/api/v2.1/workspace/1/import-dtable/

```

**Sample response**

```
{
   "table":{
      "id":87,
      "workspace_id":22,
      "uuid":"d09b6bcc-b6e5-4b8c-b9e2-c4329a8af482",
      "name":"t1",
      "creator":"a",
      "modifier":"a",
      "created_at":"2020-02-29T09:58:23+00:00",
      "updated_at":"2020-02-29T09:58:23+00:00"
   }
}

```

## Export DTable

**GET** api/v2.1/workspace/\<workspace_id>/dtable/\<name>/export-dtable/

**Sample request**

```
curl -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/export-dtable/

```

**Sample response**

```
{
   "task_id":"1582970303923",
   "table":{
      "id":87,
      "workspace_id":22,
      "uuid":"d09b6bcc-b6e5-4b8c-b9e2-c4329a8af482",
      "name":"t1 (2)",
      "creator":"a",
      "modifier":"a",
      "created_at":"2020-02-29T09:58:23+00:00",
      "updated_at":"2020-02-29T09:58:23+00:00"
   }
}

```

## Query Import/Export Status

**GET** api/v2.1/dtable-io-status/

**Request parameters**

* task_id

**Sample request**

```
curl -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" https://cloud.seatable.io/api/v2.1/dtable-io-status/?task_id=1582970303923

```

**Sample response**

```
{"is_finished":false}

```

## Get Export Content

**GET** api/v2.1/dtable-export-content/

**Request parameters**

* task_id
* dtable_uuid

**Sample request**

```
curl -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" https://cloud.seatable.io/api/v2.1/dtable-export-content/?task_id=1582970912441&dtable_uuid=
d09b6bcc-b6e5-4b8c-b9e2-c4329a8af482

```

**Sample response**

 .dtable zip file

## Cancel Task

**DELETE** api/v2.1/dtable-io-status/

**Request parameters**

* task_id
* task_type, "export" or "import"
* dtable_uuid

**Sample request**

```
curl -X DELETE -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" https://cloud.seatable.io/api/v2.1/dtable-export-content/?task_id=1582970912441&dtable_uuid=
d09b6bcc-b6e5-4b8c-b9e2-c4329a8af482&task_type=export

```

**Sample response**

```
{'success': true}

```


