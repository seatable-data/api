# Rows

In SeaTable, each row is considered as a record. For details about the data format, refer to [SeaTable Data Structure](https://docs.seatable.io/published/dtable-sdk/data-structure.md).

## List Rows

### List Rows in A View

List all the rows visible in a specific view.

**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/rows/

**Request Authentication**

> Base Access Token

**Sample Request**

List all the rows in the `Table1` in the following base, in the view `completed`:

> ```
> curl \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/rows/?table_name=Table1&view_name=completed'
>
> ```

**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**table_name** _\[string, required]_

> The name of the table.

**view_name** _\[string, optional]_

> The name of the view. If left blank, "Default View" will be applied.

**Return Values**

JSON-object with the list of rows.

**Sample Response (200)**

> ```
> {
>     "rows": [
>         {
>             "_id": "V_jBEGOXQ3mC3rJkQi-DOQ",
>             "_mtime": "2021-01-21T09:15:22.546+00:00",
>             "Name": "Bao",
>             "Date": "2020-09-18",
>             "checkbox": true
>         },
>         {
>             "_id": "HtZb516CTwCZRuBlY8d7Wg",
>             "_mtime": "2021-01-19T14:19:22.435+00:00",
>             "Name": "Daniel",
>             "Date": "2020-10-22",
>             "checkbox": true
>         }
>     ]
> }
>
> ```

**Possible Errors**

400 Bad Request: Parameters were not correctly given:

> ```
> {
>     "error_msg": "params invalid"
> }
>
> ```

403 Forbidden: The permission to the table was denied:

> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
>
> ```

404 Not Found: The table was not found under the given `table_name`:

> ```
> {
>     "error_msg": "table not found"
> }
>
> ```

### List Rows by Filters

Apply filtering conditions when listing the rows. A filter contains four fields `column_name` , `filter_predicate` , `filter_term` , and `filter_term_modifier` . For different column types, different `filter_predicate`, `filter_term` , and `filter_term_modifier` are supported.

**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/filtered-rows/

**Request Authentication**

> Base Access Token

**Sample Request**

In this sample request, try to filter out the records in the "Name" column, which is a text type, all the entries that contains the letters "a" and "b":

> ```
> curl \
> -H "Content-Type: application/json" \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/filtered-rows/?table_name=Table1' \
> -d `{
> 	"filters":[
> 		{
> 			"column_name": "Name",
> 			"filter_predicate": "contains",
> 			"filter_term": "a",
> 			"filter_term_modifier": ""	
> 		},
> 		{
> 			"column_name": "Name",
> 			"filter_predicate": "contains",
> 			"filter_term": "b",
> 			"filter_term_modifier": ""	
> 		}
> 	],
> 	"filter_conjunction": "Or"
> }`
>
> ```

**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**table_name** _\[string, required]_

> The name of the table.

**view_name** _\[string, optional]_

> The name of the view. If left blank, "Default View" will be applied.

**filters** _\[list, required]_

> In this list, compose one or more filter conditions. For each specific column type, these conditions can be:
>
> **For the column types Text、Geolocation**
>
> * `filter_predicate`: contains, does_not_contain, is, is_not, is_empty, is_not_empty
> * `filter_term`: a string or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column type Number**
>
> * `filter_predicate`: equal, not_equal, less, greater, less_or_equal, greater_or_equal, is_empty, > is_not_empty
> * `filter_term`: a string containing the number  (like "10") or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column type Checkbox**
>
> * `filter_predicate`: is
> * `filter_term`: true or false
> * `filter_term_modifier`: an empty string
>
> **For the column type Single-select**
>
> * `filter_predicate`: is, is_not, is_empty, is_not_empty
> * `filter_term`: a string containing the name of option (like "seaTable") or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column type Multiple-select**
>
> * `filter_predicate`: has_any_of, has_all_of, has_none_of, is_exactly, is_empty, is_not_empty
> * `filter_term`: an array that some items are the names of options or an empty array or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column types Date、Ctime、Mtime**
>
> * `filter_predicate`: is, is_within, is_before, is_after, is_on_or_before, is_on_or_after, is_not, > is_empty, is_not_empty
> * `filter_term`: a date string (like "2020-10-27 12:00") or an empty string
> * `filter_term_modifier`: changes with the change of `filter_predicate`
>   * if `filter_predicate` is 'is_within', it can be one of the_past_week, the_past_month, the_past_year, this_week, this_month,    this_year, the_next_week, the_next_month, the_next_year, the_next_numbers_of_days, the_past_numbers_of_days.
>   * if `filter_predicate` is 'is_empty' or 'is_not_empty', it is an empty string.
>   * Otherwise,  it can be one of today, tomorrow, yesterday, one_week_ago, one_week_from_now, one_month_ago, one_month_from_now, number_of_days_ago, number_of_days_from_now, exact_date or an empty string.
>
> **For the column type Collaborator**
>
> * `filter_predicate`:  has_any_of, has_all_of, has_none_of, is_exactly, is_empty, is_not_empty, include_me
> * `filter_term`: an array or an empty array or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column types Creator、Last_modifier**
>
> * `filter_predicate`: contains, dost_not_contain, include_me, is, is_not
> * `filter_term`: an array or an empty array or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column type Formula**
>
> * If the result type is 'string' or 'bool', process according to the text column type.
> * If the result type is 'date', process according to the date column type.
> * If the result type is 'number', process according to the number column type.
>
> **For the column type Link**
>
> * `filter_predicate`: contains, dost_not_contain, is_empty, is_not_empty
> * `filter_term`: a string or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column type Auto-number**
>
> * `filter_predicate`: contains, dost_not_contain, is, is_not
> * `filter_term`: a string or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column types File、Image、Long_text、URL**
>
> * not support 

**filter_conjunction** _\[enum(__`And`__, __`Or`__), optional]_

> The conjunction type of multiple filter conditions. 

**Sample Response (200)**

Three records were found according to the filter condition in the sample request:

> ```
> {
>     "rows": [
>         {
>             "_id": "V_jBEGOXQ3mC3rJkQi-DOQ",
>             "_mtime": "2021-01-21T09:15:22.546+00:00",
>             "Name": "Bao",
>             "Date": "2020-09-18",
>             "checkbox": true
>         },
>         {
>             "_id": "HtZb516CTwCZRuBlY8d7Wg",
>             "_mtime": "2021-01-19T14:19:22.435+00:00",
>             "Name": "Daniel",
>             "Date": "2020-10-22",
>             "checkbox": true
>         },
>         {
>             "_id": "V_jBEGOXQ3mC3rJkQi-DOQ",
>             "_mtime": "2021-01-26T13:52:49.957+00:00",
>             "Name": "Bob",
>             "Date": "2020-09-18",
>         }
>     ]
> }
>
> ```
>
> When no record can be displayed (also because of wrong filter conditions), an empty list is returned without error message.

**Possible Errors**

400 Bad Request: The filter conjunction was not correctly given:

> ```
> {
>     "error_msg": "filter_conjunction invalid"
> }
>
> ```

403 Forbidden: The permission to the table was denied:

> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
>
> ```

404 Not Found: The column was not found:

> ```
> {
>     "error_msg": "column Names not found"
> }
>
> ```

### List Grouped Rows in A View

If the rows in a certain view are grouped, this request can return the details of these rows also in a grouped manner.

**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/rows/

**Request Authentication**

> Base Access Token

**Sample Request**

> ```
> curl \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/rows/?table_name=Table1&view_name=Sex&grouping=true'
>
> ```

**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**table_name** _\[string, required]_

> The name of the table.

**view_name** _\[string, optional]_

> The name of the view. If left blank, "Default View" will be applied.

**grouping** _\[enum(__`true`__, __`false`__), required]_

> To return a grouped object, use `grouping=true`. If not used or `false` is used, the returned rows are not grouped, although they might be grouped in the view.

**Return Values**

JSON-object with grouped rows and their details. The returned `cell_value` is the grouping label and the `column_key` is the column of the grouping label.

**Sample Response (200)**

> ```
> {
>     "groups": [
>         {
>             "column_name": "Name",
>             "column_key": "0000",
>             "cell_value": "Men",
>             "rows": [
>                 {
>                     "_id": "NwI3PS_KTY-DtTqxo6n9_g",
>                     "Name": "Ali"
>                 },
>                 {
>                     "_id": "C6GXtPi7RJS80bQQcrLkmw",
>                     "Name": "Bob"
>                 }
>             ]
>         },
>         {
>             "column_name": "Name",
>             "column_key": "0000",
>             "cell_value": "Women",
>             "rows": [
>                 {
>                     "_id": "ELtcMWQOQm2qbJEn56QW9A",
>                     "Name": "Lisa"
>                 }
>             ]
>         }
>     ]
> }
>
> ```

**Possible Error**

400 Bad Request: The current view is not grouped, while `grouping=true`:

> ```
> {
>     "error_msg": "table not support group"
> }
>
> ```

400 Bad Request: Parameter not correct (probably wrong table name?):

> ```
> {
>     "error_msg": "params invalid"
> }
>
> ```

403 Forbidden: The permission to the table was denied:

> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
>
> ```

404 Not Found: The view was not found:

> ```
> {
>     "error_msg": "view not found"
> }
>
> ```

## Append A Row

Append a new row below the last record.

**URL Structure**

> **\[POST]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/rows/

**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> -H "Accept: application/json" \
> -H "Content-type: application/json" \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/rows/' \
> -d '{ \
> 	"row": {"Name": "I'm a new Row"}, \
> 	"table_name": "Table1" \
> }' 
>
> ```

**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**table_name** _\[string, required]_

> The name of the table.

**row** _\[array, required]_

> In this JSON array of objects, fill in the details of the row in the format of `"coloum name": "Content"`.

**Return Values**

JSON-object with the details of the newly appended row. In the response, the column(s)' name will be replaced by their `key`.

**Sample Response (200)**

> ```
> {
>     "0000": "A new row",
>     "_id": "VNe7qciMTEKaIb56Hykixg",
>     "_creator": "8cb2a6da6568fu47ry2905bf1647fd3f@auth.local",
>     "_last_modifier": "8cb2a6da6568fu47ry2905bf1647fd3f@auth.local"
> }
>
> ```
>
> If the `row` parameter was not correctly configured, an empty row might be added without returning error message.

**Possible Errors**

400 Bad Request: The table name was probably wrong:

> ```
> {
>     "error_type": "table_not_exist",
>     "error_message": "table Table11 not found"
> }
>
> ```

403 Forbidden: The permission to the table was denied:

> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
>
> ```

## Insert A Row

Insert a new row above or below an existing row.

**URL Structure**

> **\[POST]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/rows/

**Request Authentication**

> Base Access Token

**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> -H "Accept: application/json" \
> -H "Content-type: application/json" \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/rows/' \
> -d '{
>     "row": {"Name": "I am new Row"}, \
>     "table_name": "Table1", \
>     "anchor_row_id": "HT5R_PjVQrOyX3_5O-t6Aw", \
>     "row_insert_position": "insert_above" \
>     }' 
>
> ```

**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**table_name** _\[string, required]_

> The name of the table.

**row** _\[array, required]_

> In this JSON array of objects, fill in the details of the row in the format of `{"coloum name": "Content"}`.

**anchor_row_id** _\[string, required]_

> Reference row of the insertion.

**row_insert_position** _\[enum(`insert_above`, `insert_below`), optional, `insert_below` by default]_

> To insert the new row above or below the anchor row.

**Return Values**

JSON-object with the details of the newly inserted row.

**Sample Response (200)**

> ```
> {
>     "0000": "I am new Row",
>     "_id": "a1lxcEYGRZ2z6nZfFzdygw",
>     "_creator": "8e02ebc52ff0484d9f15b50904a98d2f@auth.local",
>     "_last_modifier": "8e02ebc52ff0484d9f15b50904a98d2f@auth.local"
> }
>
> ```

**Possible Errors**

400 Bad Request: The table's name was wrong:

> ```
> {
>     "error_type": "table_not_exist",
>     "error_message": "table Table11 not found"
> }
>
> ```

403 Forbidden: The permission to the table was denied:

> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
>
> ```

## Batch Append Rows

Append multiple rows in one request.

**URL Structure**

> **\[POST]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/batch-append-rows/

**Request Authentication**

> Base Access Token

**Sample Request**

> ```
> curl --request POST \
> --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDQxMTUwMTcsImR0YWJsZV91dWlkIjoiNDFjZDA1ZGFiMjlhNDQyOGJjMzFiZDY2ZjQ2MDA4MTciLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.jAIndSyeNivFnAb9f3nF8MENYK2I26JS8BLUyo7aJRw' \
> --header 'Content-Type: application/json' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/batch-append-rows/' 
> --data-raw '{ \
>     "rows": [{ \
>                 "Name": "Jasmin", \
>                 "Content": "Tea" \
>             }, { \
>                 "Name": "Ginger", \
>                 "Content": "Ale" \
>             }, { \
>                 "Name": "Matcha", \
>                 "Content": "Latte" \
>             }], \
>     "table_name": "Table6" \
> }'
>
> ```

**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**table_name** _\[string, required]_

> The name of the table.

**row** _\[array, required]_

> In this JSON array of objects, fill in the details of the row in the format of `{"coloum name": "Content"}`.

**Return Values**

JSON-object with the number of successfully added rows.

**Sample Response (200)**

> ```
> {
>     "inserted_row_count": 3
> }
>
> ```
>
> If one or more columns were not found in the table, they are ignored without returning an error message.

**Possible Errors**

403 Forbidden: The permission to the table was denied:

> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
>
> ```

404 Not Found: The table name was probably wrong:

> ```
> {
>     "error_msg": "table Table11 not found"
> }
>
> ```

## Update A Row

Change the records in an existing row.

**URL Structure**

> **\[PUT]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/rows/

**Request Authentication**

> Base Access Token

**Sample Request**

> ```
> curl -X PUT \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> -H "Accept: application/json" \
> -H "Content-type: application/json"  \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/rows/' \
> -d '{ \
> 	"row": {"Name": "NewName"}, \
> 	"table_name": "Table1", \
>   "row_id": "HT5R_PjVQrOyX3_5O-t6Aw" \
> }' 
>
> ```

**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**table_name** _\[string, required]_

> The name of the table.

**row** _\[array, required]_

> In this JSON array of objects, fill in the details of the row in the format of `{"coloum name": "Content"}`.

**row_id** _\[string, required]_

> ID of the row to be updated.

**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

> ```
> {
>     "success": true
> }
>
> ```

**Possible Errors**

400 Bad Request: The table's name was wrong:

> ```
> {
>     "error_type": "table_not_exist",
>     "error_message": "table Table11 not found"
> }
>
> ```

400 Bad Request: The row was not found, probably wrong `row_id`:

> ```
> {
>     "error_type": "row_not_exist",
>     "error_message": "Row does not exist."
> }
>
> ```

403 Forbidden: The permission to the table was denied:

> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
>
> ```

## Delete A Row

When a row is deleted, you can restore it within 7 days. To restore rows that are deleted in a longer time, restoring a snapshot could be an alternative. The length that a snapshot can be stored depends on your plan. For more details, refer to the [SeaTable Plans](https://seatable.io/en/pricing/).

**URL Structure**

> **\[DELETE]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/rows/

**Request Authentication**

> Base Access Token

**Sample Request**

> ```
> curl -X DELETE\
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> -H "Accept: application/json" \
> -H "Content-type: application/json"  \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/rows/'
> -d '{
> 	"table_name": "Table1", \
>     "row_id": "HT5R_PjVQrOyX3_5O-t6Aw" \
> }' 
>
> ```

**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**table_name** _\[string, required]_

> The name of the table.

**row_id** _\[string, required]_

> ID of the row to be deleted.

**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

> ```
> {
>     "success": true
> }
>
> ```

**Possible Errors**

400 Bad Request: The table was not found:

> ```
> {
>     "error_type": "table_not_exist",
>     "error_message": "table Table11 not found"
> }
>
> ```

403 Forbidden: The permission to the table was denied:

> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
>
> ```

500 Internal Server Error: The row was not found, probably already deleted:

> ```
> Internal Server Error
>
> ```

## Batch Delete Rows

Delete multiple rows in one request.

**URL Structure**

> **\[DELETE]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/batch-delete-rows/ 

**Request Authentication**

> Base Access Token

**Sample Request**

> ```
> curl -X DELETE \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> -H "Accept: application/json" \
> -H "Content-type: application/json"  \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/batch-delete-rows/' \
> -d '{ \
> 	"table_name": "Table1", \
>     "row_ids": ["HT5R_PjVQrOyX3_5O-t6Aw", "IjFAMS5jb20iLCJkdGweffe"] \
> }' 
>
> ```

**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**table_name** _\[string, required]_

> The name of the table.

**row_ids** _\[list, required]_

> A list of `row_id` to be deleted.

**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

> ```
> {
>     "success": true
> }
>
> ```

**Possible Errors**

400 Bad Request: The table was not found:

> ```
> {
>     "error_type": "table_not_exist",
>     "error_message": "table Table11 not found"
> }
>
> ```

403 Forbidden: The permission to the table was denied:

> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
>
> ```

500 Internal Server Error: At least one row was not found, probably already deleted:

> ```
> Internal Server Error
>
> ```

## Link A Row

Set up a link between two rows.

**URL Structure**

> **\[POST]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/links/



**Request Authentication**

> Base Access Token



**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> -H "Accept: application/json" \
> -H "Content-type: application/json"  \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/links/'
> -d '{ \
> 	"table_name": "Table1", \
>   "other_table_name": "Table2", \
>   "link_id": '1206' \
>   "table_row_id": "OkuYk0OWSIyi7zZKJ2NC4g", \
>   "other_table_row_id": "eyuMiAwaQlSSr983O03oUA" \
> }' 
>
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**link_id** _\[string, required]_

> The ID of this link, a 4-digit combination of numbers (0-9) and letters (a-z and A-Z).

**table_name** _\[string, required]_

> The name of the current table.

**other_table_name** _\[string, required]_

> The name of the table to be linked.

**table_row_id** _\[string, required]_

> The ID of the current row.

**other_table_row_id** _\[string, required]_

> The ID of the row to be linked.



**Return Values**

JSON-object with the result of the operation.



**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```



**Possible Errors**

400 Bad Request: At least one of the tables' names was not accepted:
> ```
> {
>     "error_type": "table_not_exist",
>     "error_message": "table table11 or Table1 not found"
> }
> ```

400 Bad Request: The row's ID was not accepted:
> ```
> {
>     "error_type": "row_not_exist",
>     "error_message": "Row does not exist."
> }
> ```

403 Forbidden: The access token was not accepted:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```




## Delete A Row Link

Delete an existing link between two rows.


**URL Structure**

> **\[DELETE]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/links/



**Request Authentication**

> Base Access Token



**Sample Request**

> ```
> curl -X DELETE \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> -H "Accept: application/json" \
> -H "Content-type: application/json" \
> https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/links/ \
> -d '{ \
> 	"table_name": "Table1", \
>     "other_table_name": "Table2", \
>     "link_id": '1206', \
>     "table_row_id": "OkuYk0OWSIyi7zZKJ2NC4g", \
>     "other_table_row_id": "eyuMiAwaQlSSr983O03oUA" \
> }' 
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_

> The ID of the base.

**link_id** _\[string, required]_

> The ID of the link to be deleted. This link can be found with the API request **Get A Base's Metadata**. 

**table_name** _\[string, required]_

> The name of the current table.

**other_table_name** _\[string, required]_

> The name of the linked table.

**table_row_id** _\[string, required]_

> The ID of the current row.

**other_table_row_id** _\[string, required]_

> The ID of the linked row.




**Return Values**

JSON-object with the result of the operation.


**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```


**Possible Errors**

400 Bad Request: At least one of the tables' names was not accepted:
> ```
> {
>     "error_type": "table_not_exist",
>     "error_message": "table table11 or Table1 not found"
> }
> ```

400 Bad Request: The row's ID was not accepted:
> ```
> {
>     "error_type": "row_not_exist",
>     "error_message": "Row does not exist."
> }
> ```

403 Forbidden: The access token was not accepted:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```




## List Deleted Rows

The deleted rows are kept in record for 7 days. Use this request to list these deleted rows. To find rows deleted longer than 7 days ago, use Snapshots as alternative.


**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/deleted-rows/



**Request Authentication**

> Base Access Token





**Sample Request**

> ```
> curl 
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ' \
> "https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/deleted-rows/"
> ```





**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned list. 

**per_page** _\[int, optional, 25 by default]_
> Number of deleted rows to be displayed per page.




**Return Values**

JSON-object with the list of deleted rows.




**Sample Response (200)**

> ```
> {
>     "deleted_rows": [
>         {
>             "id": 37,
>             "dtable_uuid": "7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5",
>             "row_id": "ZPFv2pm1SiaQpulvzkHm5Q",
>             "op_user": "244b43hr6fy54bb4afa2c2cb7369d244@auth.local",
>             "op_time": "2020-03-17T10:31:35.000Z",
>             "detail": {
>                 "table_id": "0000",
>                 "table_name": "Table1",
>                 "row_name": "Jasmin Tea",
>                 "row_data": [
>                     {
>                         "column_key": "0000",
>                         "column_name": "Name",
>                         "column_type": "text",
>                         "column_data": {},
>                         "value": "test"
>                     },
>                     {
>                         "column_key": "AKLn",
>                         "column_name": "Details",
>                         "column_type": "file",
>                         "column_data": {},
>                         "value": [
>                             {
>                                 "name": "example.html",
>                                 "size": 514,
>                                 "type": "file",
>                                 "url": "http://cloud.seatable.io/workspace/1/asset/> 46620d70-c8e5-49ab-8874-9d4a2dc4608c/files/2020-03/example.html"
>                             }
>                         ]
>                     }
>                 ]
>             },
>             "op_app": null
>         }
>     ]
> }
> ```
If there's no deleted rows in the last 7 days, an empty list is returned without error message.


**Possible Errors**

403 Forbidden: The access to the base was not accepted (wrong access token or `dtable_uuid`):
> ```
> {
>     "error_msg": "You don't have permission to get deleted rows."
> }
> ```




## Get Row by Row ID in A Table

With the row's ID, get its details with this request.


**URL Structure**

> **\[GET]** /api/v1/dtables/`<dtable_uuid>`/rows/`<row_id>`/



**Request Authentication**

> Base Access Token




**Sample Request**

> ```
> curl \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/rows/J5jgoxDJTE2zUmAQISpk3g/?table_id=9GlO
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**row_id** _\[string, required]_
> The ID of the row to be queried.

**table_id** _\[string, required]_
> The ID of the table.

**convert** _\[enum(`true`, `false`), `true` by default]_
> Whether the column's ID should be converted into column's name. If `true`, column's name is returned.


**Return Values**

JSON-object with the details of the row.

**Sample Response**

> ```
> {
>     "_id": "Qtf7xPmoRaiFyQPO1aNTjA",
>     "_mtime": "2021-01-27T14:59:45.716+00:00",
>     "Name": "Lisa",
>     "Date": "2020-08-19",
>     "collabs": [
>         "244b43hr6fy54bb4afa2c2cb7369d244@auth.local"
>     ],
>     "Content": "Bon",
>     "link": []
> }
> ```

if `convert` = `false`

> ```
> {
>     "_id": "Qtf7xPmoRaiFyQPO1aNTjA",
>     "_participants": [
>         {
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
>             "contact_email": "lisa@example.com",
>             "email": "244b43hr6fy54bb4afa2c2cb7369d244@auth.local",
>             "name": "Ginger Ale"
>         },
>         {
>             "avatar_url": "https://cloud.seatable.io/image-view/avatars/3/7/a0a57575a3ca0c78e8c5b6b0d0dbda/resized/80/cd7f6edd2c75afd3b7299917b3767c0f.png",
>             "contact_email": "jasmin@example.com",
>             "email": "8cb2a6da656876hgf42905bf1647fd3f@auth.local",
>             "name": "Jasmin Tee"
>         }
>     ],
>     "_creator": "8cb2a6da656876hgf42905bf1647fd3f@auth.local",
>     "_ctime": "2020-11-18T12:42:14.779+00:00",
>     "_last_modifier": "8cb2a6da656876hgf42905bf1647fd3f@auth.local",
>     "_mtime": "2021-01-27T14:59:45.716+00:00",
>     "0000": "Lisa",
>     "BydO": "2020-08-19",
>     "LfGJ": [
>         "244b43hr6fy54bb4afa2c2cb7369d244@auth.local"
>     ],
>     "on03": OK,
>     "9SpZ": [
>         "8cb2a6da656876hgf42905bf1647fd3f@auth.local"
>     ],
>     "g200": [
>         {
>             "name": "users.md",
>             "size": 1957,
>             "type": "file",
>             "url": "https://table.seafile.com/workspace/204/asset/650d8a0d-7e27-46a8-8b18-6cc6f3db2057/files/2021-01/users.md"
>         }
>     ],
>     "x1w3": "Bon"
> }
> ```

**Possible Errors**

403 Forbidden: Probably the access token or the ID of the base was wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

404 Not Found: The table's ID was not found:
> ```
> {
>     "error_msg": "table not found"
> }
> ```

404 Not Found: The row's ID was not found in the table:
> ```
> {
>     "error_msg": "row not found"
> }
> ```

