# Columns

## List columns of a table's view

GET /api/v1/dtables/:dtable_uuid/columns/

Request Query Params:

* table_name: name of table of base, optional
* view_name: name of view of table of base, optional
* table_id: id of table of base, optional
* view_id: id of view of table of base, optional

Sample Request

```
curl --request GET 'https://cloud.seatable.io/dtable-server/api/v1/dtables/626e40fa76304a4fb7641b71efab4795/columns/?table_name=Table1' --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU'

```

Sample Response

```
{
    "columns": [
        {
            "key": "0000",
            "name": "name",
            "type": "text",
            "width": 200,
            "editable": true,
            "resizable": true
        },
        {
            "key": "g4s1",
            "type": "number",
            "name": "api3",
            "editable": true,
            "width": 200,
            "resizable": true,
            "draggable": true,
            "data": null,
            "permission_type": "",
            "permitted_users": []
        }
    ]
}

```

## Insert a column

POST /api/v1/dtables/:dtable_uuid/columns/

Request Params

* table_name: name of table of base, required
* column_name: new column name, required
* column_type: column's type, required
* column_key: key of column which you want to insert new column after, default insert at the end if null, optional

Sample Request

```
curl --request POST 'https://cloud.seatable.io/dtable-server/api/v1/dtables/626e40fa76304a4fb7641b71efab4795/columns/' --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' --header 'Content-Type: application/json' --data-raw '{
    "table_name": "Table1",
    "column_name": "api3",
    "column_type": "number",
    "column_key": "0000"
}'

```

## Rename a column

PUT /api/v1/dtables/:dtable_uuid/columns/

Request Params:

* op_type: "rename_column", required
* table_name: name of table of base, required
* column_key: key of column to update, required,
* new_column_name: new name of column, required

Sample Request

```
curl --request POST 'https://cloud.seatable.io/dtable-server/api/v1/dtables/626e40fa76304a4fb7641b71efab4795/columns/' --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' --header 'Content-Type: application/json' --data-raw '{
    "op_type": "rename_column",
    "table_name": "Table1",
    "column_key": "61Lc",
    "new_column_name": "api4"
}'

```

## Resize a column

PUT /api/v1/dtables/:dtable_uuid/columns/

Request Params:

* op_type: "resize_column", required
* table_name: name of table of base, required
* column_key: key of column to update, required
* new_column_width: new width of column, required

Sample Request

```
curl --request POST 'https://cloud.seatable.io/dtable-server/api/v1/dtables/626e40fa76304a4fb7641b71efab4795/columns/' --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' --header 'Content-Type: application/json' --data-raw '{
    "op_type": "resize_column",
    "table_name": "Table1",
    "column_key": "0000",
    "new_column_width": 200
}'

```

## Freeze a column

PUT /api/v1/dtables/:dtable_uuid/columns/

Request Params:

* op_type: "freeze_column", required
* table_id: id of table of base, required
* column_key: key of column to update, required
* forzen: true/false, required

Sample Request

```
curl --request POST 'https://cloud.seatable.io/dtable-server/api/v1/dtables/626e40fa76304a4fb7641b71efab4795/columns/' --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' --header 'Content-Type: application/json' --data-raw '{
    "op_type": "freeze_column",
    "table_name": "Table1",
    "column_key": "VnTa",
    "frozen": false
}'

```

## Move a column

PUT /api/v1/dtables/:dtable_uuid/columns/

Request Params:

* op_type: "move_column", required
* table_name: name of table of base, required
* column_key: key of column to move, required
* target_column_key: key of target column, column will be moved after target column, required

Sample Request

```
curl --location --request PUT 'https://cloud.seatable.io/dtable-server/api/v1/dtables/626e40fa76304a4fb7641b71efab4795/columns/' --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDI1MjU5NjUsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.V_qYR7Mk1Wt4_5n2dAM2fP_CWWwibokWlUX1-OfBn4s' --header 'Content-Type: application/json' --data-raw '{
    "op_type": "move_column",
    "table_name": "Table1",
    "column_key": "0bp2",
    "target_column_key": "0000"
}'

```

## Modify a column type

PUT /api/v1/dtables/:dtable_uuid/columns/

Request Params:

* op_type: "modify_column_type", required
* table_name: name of table of base, required
* column_key: key of column to modify, required
* new_column_type: new column type, required

Column type:

```
'number', 'text', 'checkbox', 'date', SINGLE_SELECT = 'single-select', 'long-text', 'image', 'file', 'multiple-select', 'collaborator', 'link', 'formula', 'creator', 'ctime', 'last-modifier', 'mtime', 'geolocation', 'auto-number', 'url'

```

Sample Request

```
curl --request PUT 'https://cloud.seatable.io/dtable-server/api/v1/dtables/626e40fa76304a4fb7641b71efab4795/columns/' --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDI1MjU5NjUsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.V_qYR7Mk1Wt4_5n2dAM2fP_CWWwibokWlUX1-OfBn4s' --header 'Content-Type: application/json' --data-raw '{
    "op_type": "modify_column_type",
    "table_name": "Table1",
    "column_key": "EGS5",
    "new_column_type": "number"
}'

```

## Delete a column

DELETE /api/v1/dtables/:dtable_uuid/columns/

Request Params:

* table_name: id of table of base, required,
* column_key: key of column to delete, required

Sample Request

```
curl --request DELETE ''https://cloud.seatable.io/dtable-server/api/v1/dtables/626e40fa76304a4fb7641b71efab4795/columns/' --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' --header 'Content-Type: application/json' --data-raw '{
    "table_name": "Table1",
    "column_key": "wYVM"
}'

```


