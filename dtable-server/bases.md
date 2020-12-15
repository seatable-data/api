# Bases

## Get a base

**GET** /dtable-server/api/v1/dtables/:dtable_uuid

**Request parameters**

* dtable_uuid

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs'
 "https://cloud.seatable.io/dtable-server/dtables/622f1e6d337449e49b429f2253037a76"

```

**Sample Response (200)**

```
"{\"tables\":[{\"_tid\":\"0000\",\"title\":\"Table1\",\"columns\":[{\"key\":\"0000\",\"name\":\"Name\",\"type\":\"\",\"width\":142,\"editable\":true,\"resizable\":true},{\"key\":\"vd8m\",\"name\":\"Media\",\"type\":\"image\",\"editable\":true,\"width\":137,\"resizable\":true,\"draggable\":true,\"data\":null},{\"key\":\"QzuD\",\"name\":\"Label\",\"type\":\"single-select\",\"editable\":true,\"width\":200,\"resizable\":true,\"draggable\":true,\"data\":{\"options\":[{\"name\":\"good\",\"color\":\"#DDFFE6\",\"ID\":\"935357\"}]}}],\"rows\":[{\"_id\":\"0a4852c0-1f14-40f0-9cc7-722892f3f5b9\",\"vd8m\":[],\"QzuD\":\"935357\",\"0000\":\"hello\"}],\"views\":[{\"_vid\":\"0000\",\"type\":\"table\",\"name\":\"默认视图\",\"rows\":[],\"summaries\":{\"0000\":{},\"vd8m\":{},\"QzuD\":{}},\"filters\":[]}],\"Id2Row\":{\"0a4852c0-1f14-40f0-9cc7-722892f3f5b9\":{\"_id\":\"0a4852c0-1f14-40f0-9cc7-722892f3f5b9\",\"vd8m\":[],\"QzuD\":\"935357\",\"0000\":\"hello\"}}}]}"

```

**Errors**

* Permission Denied.
* Not Found.
* Internal Server Error.

## Get a base's metadata

**GET** /dtable-server/api/v1/dtables/:dtable_uuid/metadata

**Request parameters**

* dtable_uuid

**Sample request**

```
curl -H 'Accept: application/json; charset=utf-8; indent=4' -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJkdGFibGVfdXVpZCI6IjVhNDBkZDhlNTliNzQ5ZmY4NGE3M2M5ZmI4YTBjZjYwIiwidXNlcm5hbWUiOiIxQDEuY29tIiwicGVybWlzc2lvbiI6InJ3In0.nbv_87zKSSw8A3dSTV5HVKcIbcNqmrlN-QtjihR_EUA' "https://cloud.seatable.io/dtable-server/api/v1/dtables/5a40dd8e59b749ff84a73c9fb8a0cf60/metadata/"

```

**Sample Response (200)**

```
{
    "metadata": {
        "tables": [
            {
                "_id": "0000",
                "name": "Good",
                "is_header_locked": false,
                "columns": [
                    {
                        "key": "0000",
                        "name": "Name",
                        "type": "text",
                        "width": 200,
                        "editable": true,
                        "resizable": true
                    },
                    {
                        "key": "5sec",
                        "type": "long-text",
                        "name": "Introduce",
                        "editable": true,
                        "width": 200,
                        "resizable": true,
                        "draggable": true,
                        "data": null
                    }
                ],
                "views": [
                    {
                        "_id": "0000",
                        "type": "table",
                        "name": "Default",
                        "is_locked": true,
                        "rows": [],
                        "summaries": {
                            "0000": {}
                        },
                        "sorts": [],
                        "filters": []
                    }
                ]
            },
            {
                "_id": "4AeY",
                "name": "Nice",
                "is_header_locked": true,
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
                "views": [
                    {
                        "_id": "0000",
                        "type": "table",
                        "name": "boy",
                        "is_locked": false,
                        "rows": [],
                        "summaries": {
                            "0000": {}
                        },
                        "filter_conjunction": "And",
                        "filters": [
                            {
                                "column_key": "Fbgg",
                                "filter_predicate": "is",
                                "filter_term": "950539",
                                "filter_term_modifier": ""
                            }
                        ],
                        "sorts": []
                    },
                    {
                        "_id": "J9VE",
                        "summaries": {
                            "0000": {},
                            "EIFc": {
                                "sum": 18
                            }
                        },
                        "is_locked": false,
                        "filters": [
                            {
                                "column_key": "Fbgg",
                                "filter_predicate": "is",
                                "filter_term": "968434",
                                "filter_term_modifier": ""
                            }
                        ],
                        "sorts": [],
                        "rows": [],
                        "name": "girl",
                        "type": "table",
                        "filter_conjunction": "And"
                    }
                ]
            }
        ]
    }
}

```

**Errors**

* Permission Denied.
* Not Found.
* Internal Server Error.

## Import a table by uploading a csv file

**POST** /dtable-server/api/v1/:dtable_uuid/import-csv/

**Request parameters**

* csv_file: the file to upload, required
* table_name: new table name required
* lang: the language, required

**Request Sample**

```
curl -X POST 'https://cloud.seatable.io/dtable-server/api/v1/a57b56d31cc54ebd8a6ca1b28ac3dbdf/import-csv/' -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1ODM4MzA4MTUsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.hY_dMfsfWa2iO9U0MxPhdQA_v6E7LB55uVAKKAn7kX8' -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' -H 'enctype: multipart/form-data' -F csv_file=@yt_2018-03-01-2.csv -F table_name=yt-2 -F lang=zh-cn

```

**Response Sample**

```
{
    "success": true
}

```

**Errors**

* Not Found.
* Permission Denied.
* Internal Server Error.

## Append a table by uploading a csv file

**POST** /dtable-server/api/v1/dtables/:dtable_uuid/append-csv/﻿

* dtable_uuid
* table_name
* csv_file

**Sample request**

```
curl -X POST -d "table_name=Table1" -F "csv_file=@/tmp/test.csv" -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' -H "Content-type: application/json" https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/append-csv/

```

**Sample Response (200)**

```
{    
    "success": true
}

```


