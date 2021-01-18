# Columns

## List Columns of A Table's View

In a table, threre can be multiple views in which some columns are hidden. Use this API request to list all the columns visible in a certain view.


**URL Structure**

> **\[GET]** /api/v1/dtables/`<dtable_uuid>`/columns/


**Request Authentication**

> Base Access Token




**Sample Request**

List all columns visible in the default view in `Table1` in the following base:
> ```
> curl --request GET \
> --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/columns/?table_name=Table1'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**table_name** _\[string, optional]_
> Name of the table. Although optional, either `table_name` or `table_id` has too be given in order to identify the table.

**table_id** _\[string, optional]_
> ID of the table. Although optional, either `table_name` or `table_id` has too be given in order to identify the table.

**view_name** _\[string, optional]_
> Name of the view. When neither `view_name` nor `view_id` is given, the default view will be taken.

**view_id** _\[string, optional]_
> ID of the view. When neither `view_name` nor `view_id` is given, the default view will be taken.




**Return Values**

JSON-object with the list of columns. The columns are identified with their `key` values.


**Sample Response (200)**

```
{
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

**Possible Errors**

400 Bad Request: Missing table parameters (at least one of `table_name` and `table_id` should be given):
> ```
> {
>     "error_msg": "params invalid"
> }
> ```

403 Forbidden: Probably is the `dtable_uuid` or the `access_token` wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

404 Not Found: The table was not found (same applies also for view):
> ```
> {
>     "error_msg": "table not found"
> }
> ```

## Insert A Column

Create a new column and insert it to the desired position.


**URL Structure**

> **\[POST]** /api/v1/dtables/`<dtable_uuid>`/columns/



**Request Authentication**

> Base Access Token



**Sample Request**

> ```
> curl --request POST \
> --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' \
> --header 'Content-Type: application/json' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/columns/' \
> --data-raw '{
>     "table_name": "Table1",
>     "column_name": "API test",
>     "column_type": "number",
>     "column_key": "0000"
> }'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**table_name** _\[string, required]_
> Name of the table. 

**column_name** _\[string, required]_
> Name of the new column.

**column_type** _\[string, required]_
> Choose one of the following strings to define the column type:
> ```
> 'number'              // For the column type Number.
> 'checkbox'            // For the column type Checkbox.
> 'date'                // For the column type Date.
> 'text'                // For the column type Text.
> 'single-select'       // For the column type Single Select.
> 'long-text'           // For the column type Long Text.
> 'image'               // For the column type Image.
> 'file'                // For the column type File.
> 'multiple-select'     // For the column type Multiple Select.
> 'collaborator'        // For the column type Collaborator.
> 'link'                // For the column type Link Other Records.
> 'formula'             // For the column type Formula.
> 'creator'             // For the column type Creator.
> 'ctime'               // For the column type Created Time.
> 'last-modifier'       // For the column type Last Modifier.
> 'mtime'               // For the column type Last Modified Time.
> 'geolocation'         // For the column type Geolocation.
> 'auto-number'         // For the column type Auto Number.
> 'url'                 // For the column type URL.
> 'email'               // For the column type Email.
> 'duration'            // For the column type Duration.
> ```
> For more details, refer to [SeaTable Manual - Column Types](https://seatable.io/en/docs/user-manual/datenmanagement/feld-typen/).



**column_key** _\[string, optional]_
> If you would like to insert this column behind a specified column, give its `key` here. Otherwise the new column will be appended after the last column.


**Return Values**

JSON-object with the details of the new column. The column's `key` is automatically generated.


**Sample Response (200)**

> ```
> {
>     "key": "Xj0j",
>     "type": "text",
>     "name": "Short name",
>     "editable": true,
>     "width": 200,
>     "resizable": true,
>     "draggable": true,
>     "data": null,
>     "permission_type": "",
>     "permitted_users": []
> }
> ```
If the `column_type` was not one from the list above, a new column with empty column type will be created without returning error message.


**Possible Errors**

400 Bad Request: The table name was missing, or not found:
> ```
> table_name invalid.
> ```

400 Bad Request: The column name already exists:
> ```
> Column Sunshine exists.
> ```

403 Forbidden: Probably is the `dtable_uuid` or the `access_token` wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

## Rename, Resize, Free/Unfreeze, Move, or Modify A Column

Use the various parameters in this API request to change the name of a column, resize it (change its width), freeze/unfreeze it, or modify its type.



**URL Structure**

> **\[PUT]** /api/v1/dtables/`<dtable_uuid>`/columns/


**Request Authentication**

> Base Access Token



**Sample Request 1: Rename A Column**

Rename the column with the key of `61Lc` to "API test":

> ```
> curl --request POST \
> --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' \
> --header 'Content-Type: application/json' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/columns/' \
> --data-raw '{
>     "table_name": "Table1",
>     "column_key": "61Lc",
>     "op_type": "rename_column",
>     "new_column_name": "API test"
> }'
> ```

**Sample Request 2: Change the Width of A Column**

Change the width of the column with the key of `3xdJ` to 400:

> ```
> curl --request POST \
> --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' \
>--header 'Content-Type: application/json' \
>'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/columns/' \
>--data-raw '{
>    "table_name": "Table1",
>    "column_key": "3xdJ",
>    "op_type": "resize_column",
>    "new_column_width": 400
>}'
>```

**Sample Request 3: Freeze A Column**

Freeze the column with the key of `0000`:

> ```
> curl --request POST \
> --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' \
> --header 'Content-Type: application/json' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/columns/' \
> --data-raw '{
>     "table_name": "Table1",
>     "column_key": "0000",
>     "op_type": "freeze_column",
>     "frozen": true
> }'
> ```

Similar requests can also be made to move a column or change column type by altering the parameters `op_type` and replacing the last parameter accordingly. Details see below.


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**table_name** _\[string, required]_
> The name of the table.

**column_key** _\[string, required]_
> The 4-digit key of the column.

**op_type** _\[string, required]_
> In a request, use one of the following types of operation: 
> * `'rename_column'` to rename a column, paired with the **new_column_name** parameter;
> * `'resize_column'` to resize a column, paired with the **new_column_width** parameter;
> * `'freeze_column'` to freeze or unfreeze a column, paired with the **frozen** parameter;
> * `'move_column'` to move a column, paired with the **target_column_key** parameter;
> * `'modify_column_type'` to modify the type of a column, paired with the **new_column_type** parameter.

**new_column_name** _\[string, optional]_
> When the `op_type` is `rename_column`, use this parameter to define the new column name.

**new_column_width** _\[int, optional]_
> When the `op_type` is `resize_column`, use this parameter to define the new column width (200 by default).

**frozen** _\[enum(`true`, `false`), optional]_
> When the `op_type` is `freeze_column`, use this parameter to freeze (`true`) or unfreeze (`false`) a column.

**target_column_key** _\[string, optional]_
> When the `op_type` is `move_column`, use this parameter to move the column to the right of the target column.

**new_column_type** _\[string, optional]_
> When the `op_type` is `modify_column_type`, use this parameter to define the new type of the column. For a list of available column types, refer to the section **Insert A Column**.



**Return Values**

JSON-object with the details of the modified column.


**Sample Response (200)**

A response to the sample request 1 could look like this:

> ```
> {
>     "key": "61Lc",
>     "type": "text",
>     "name": "API test",
>     "editable": true,
>     "width": 200,
>     "resizable": true,
>     "draggable": true,
>     "data": null,
>     "permission_type": "",
>     "permitted_users": []
> }
> ```


**Possible Errors**

400 Bad Request: The parameters were not correctly given:
> ```
> table_name invalid.
> ```

403 Forbidden: Probably is the `dtable_uuid` or the `access_token` wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```


## Delete A Column

Use this request to delete an existing column with its key.


**URL Structure**

> **\[DELETE]** /api/v1/dtables/`<dtable_uuid>`/columns/



**Request Authentication**

> Base Access Token





**Sample Request**

> ```
> curl --request DELETE \
> --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDE1MjA1OTYsImR0YWJsZV91dWlkIjoiNjI2ZTQwZmE3NjMwNGE0ZmI3NjQxYjcxZWZhYjQ3OTUiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.y8igfax5-SiDuaU_CQYj0_uMw8OgBeTfzTbxltdvVfU' \
> --header 'Content-Type: application/json' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/columns/' \
> --data-raw '{
>     "table_name": "Table1",
>     "column_key": "wYVM"
> }'
> ```


**Input Parameters**

**table_name** _\[string, required]_
> The name of the table.

**column_key** _\[string, required]_
> The 4-digit key of the column.



**Return Values**

Text 'OK'.


**Sample Response**

> ```
> OK
> ```


**Possible Errors**

400 Bad Request: The table doesn't exist:
> ```
> {
>     "error_type": "table_not_exist",
>     "error_message": "table Tabel1 not found"
> }
> ```

400 Bad Request: The column doesn't exist, probably already deleted:
> ```
> {
>     "error_type": "column_not_exist",
>     "error_message": "column wYVM not found"
> }
> ```

