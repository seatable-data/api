# Bases

## Get A Base's Information

Get the basic information of a base.

**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`


**Request Authentication**

> Base Access Token



**Sample Request**

Get the basic information of the base with the following `dtable_uuid` and its `access_token`:
> ```
> curl \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> "https://cloud.seatable.io/dtable-server/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5"
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.


**Return Values**

JSON-object with the basic infos of the base.


**Sample Response (200)**

> ```
> {"version":20,"format_version":7,"statistics":[],"links":[],"tables":[{"_id":"0000","name":"Table1","rows":[{"_id":"Qtf7xPmoRaiFyQPO1aNTjA","_participants":[],"_creator":"8cb2a6da6569491ba42905bf1647fd3f@auth.local","_ctime":"2020-11-18T12:42:14.779+00:00","_last_modifier":"8cb2a6da6569491ba42905bf1647fd3f@auth.local","_mtime":"2021-01-14T09:01:57.357+00:00","0000":"Meng","BydO":"2020-08-19"},{"_id":"V_jBEGOXQ3mC3rJkQi-DOQ","_participants":[],"_creator":"8cb2a6da6569491ba42905bf1647fd3f@auth.local","_ctime":"2021-01-14T08:56:05.666+00:00","_last_modifier":"8cb2a6da6569491ba42905bf1647fd3f@auth.local","_mtime":"2021-01-14T08:56:59.458+00:00","0000":"Bao","BydO":"2020-09-18"},{"_id":"HtZb516CTwCZRuBlY8d7Wg","_participants":[],"_creator":"8cb2a6da6569491ba42905bf1647fd3f@auth.local","_ctime":"2021-01-14T08:56:07.135+00:00","_last_modifier":"8cb2a6da6569491ba42905bf1647fd3f@auth.local","_mtime":"2021-01-14T08:57:04.073+00:00","0000":"Daniel","BydO":"2020-10-22"},{"_id":"fS8qtN6FQ1uPOaNAC0Locw","_participants":[],"_creator":"8cb2a6da6569491ba42905bf1647fd3f@auth.local","_ctime":"2021-01-14T08:56:08.259+00:00","_last_modifier":"8cb2a6da6569491ba42905bf1647fd3f@auth.local","_mtime":"2021-01-14T08:57:06.657+00:00","0000":"Jonas","BydO":"2021-01-20"}],"columns":[{"key":"0000","name":"Name","type":"text","width":200,"editable":true,"resizable":true},{"key":"BydO","type":"date","name":"Date","editable":true,"width":200,"resizable":true,"draggable":true,"data":{"format":"YYYY-MM-DD"},"permission_type":"","permitted_users":[]}],"views":[{"_id":"0000","name":"Default
> View","type":"table","is_locked":false,"rows":[],"formula_rows":{},"summaries":[],"filter_conjunction":"And","filters":[],"sorts":[],"hidden_columns":[],"groupbys":[],"groups":[]}],"id_row_map":{}}]}
> ```

**Possible Errors**

403 Forbidden: Probably is the `dtable_uuid` or the `access_token` wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

## Get A Base's Metadata

Get the metadata of a base.


**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/metadata


**Request Authentication**

> Base Access Token


**Sample Request**

> ```
> curl \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJkdGFibGVfdXVpZCI6IjVhNDBkZDhlNTliNzQ5ZmY4NGE3M2M5ZmI4YTBjZjYwIiwidXNlcm5hbWUiOiIxQDEuY29tIiwicGVybWlzc2lvbiI6InJ3In0.nbv_87zKSSw8A3dSTV5HVKcIbcNqmrlN-QtjihR_EUA' \
> "https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/metadata/"
> ```

**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.



**Return Values**

JSON-object with the metadata of the base.


**Sample Response (200)**

```
{
    "metadata": {
        "tables": [
            {
                "_id": "0000",
                "name": "Table1",
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
                        "key": "BydO",
                        "type": "date",
                        "name": "Date",
                        "editable": true,
                        "width": 200,
                        "resizable": true,
                        "draggable": true,
                        "data": {
                            "format": "YYYY-MM-DD"
                        },
                        "permission_type": "",
                        "permitted_users": []
                    }
                ],
                "views": [
                    {
                        "_id": "0000",
                        "name": "Default View",
                        "type": "table",
                        "is_locked": false,
                        "rows": [],
                        "formula_rows": {},
                        "summaries": [],
                        "filter_conjunction": "And",
                        "filters": [],
                        "sorts": [],
                        "hidden_columns": [],
                        "groupbys": [],
                        "groups": []
                    }
                ]
            }
        ]
    }
}
```

**Possible Errors**

403 Forbidden: Probably is the `dtable_uuid` or the `access_token` wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

## Create A Table by Uploading A CSV File

Inside a base, create a new table by uploading and importing a .csv file.


**URL Structure**

> **\[POST]** /dtable-server/api/v1/`<dtable_uuid>`/import-csv/


**Request Authentication**

> Base Access Token



**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1ODM4MzA4MTUsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.hY_dMfsfWa2iO9U0MxPhdQA_v6E7LB55uVAKKAn7kX8' \
> 'https://cloud.seatable.io/dtable-server/api/v1/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/import-csv/' \
> -H 'content-type: multipart/form-data' \
> -H 'enctype: multipart/form-data' \
> -F csv_file=@yt_2018-03-01-2.csv \
> -F table_name=Table2 
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**csv_file** _\[file, required]_
> The .csv file to be uploaded/imported.

**table_name** _\[string, required]_
> The name of the new table.

**lang** _\[string, optional]_
> The language of the imported .csv file, e.g. "zh-cn" for Chinese or "de-de" for German.



**Sample Response**

> ```
> {
>     "success": true
> }
> ```

**Possible Errors**

400 Bad Request: Table name was missing:
> ```
> {
>     "error_msg": "table_name is invalid."
> }
> ```

400 Bad Request: Forgot to include the file in the request:
> ```
> {
>     "error_msg": "File is empty."
> }
> ```

403 Forbidden: With the access token, you don't have permission to change this base:
> ```
> {
>     "error_msg": "You don't have permission to import table"
> }
> ```

## Upload A CSV File to Append Rows in A Table

In an existing table, you can upload a .csv file with the same headers to append its content below the existing rows. A .csv file with different headers cannot be appended to an existing table.


**URL Structure**

> **\[POST]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/append-csv/


**Request Authentication**

> Base Access Token


**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> -H "Content-type: application/json" \
> https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/append-csv/ \
> -d "table_name=Table2" \
> -F "csv_file=@/tmp/test.csv" 
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**csv_file** _\[file, required]_
> The .csv file to be appended.

**table_name** _\[string, required]_
> The name of the existing table.


**Return Values**

JSON-object with the number of rows appended.



**Sample Response (200)**

> ```
> {
>     "inserted_row_count": 5
> }
> ```


**Possible Errors**

400 Bad Request: The format or header of the .csv file is incorrect:
> ```
> {
>     "error_msg": "File error"
> }
> ```

403 Forbidden: The access was not granted to change this base:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```


