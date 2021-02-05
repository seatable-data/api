# Views

## List Views by Table Name or Table ID


List all the views in a table by its name or its ID. The table's ID can be retrieved from the request **Get A Base's Metadata**.


**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/views/



**Request Authentication**

> Base Access Token


**Sample Request**

> ```
> curl \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/views/?table_name=Table1
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**table_id** OR **table_name** _\[string, required]_
> The ID or the name of the table.


**Return Values**

JSON-object with the list of views.


**Sample Response (200)**

> ```
> {
>     "views": [
>         {
>             "_id": "0000",
>             "name": "Default View",
>             "type": "table",
>             "is_locked": false,
>             "rows": [],
>             "formula_rows": {},
>             "summaries": [],
>             "filter_conjunction": "And",
>             "sorts": [],
>             "filters": [],
>             "hidden_columns": [],
>             "groupbys": [],
>             "group_rows": [],
>             "groups": []
>         }
>     ]
> }
> ```



**Possible Errors**


403 Forbidden: Probably the access token or the ID of the base was wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

404 Not Found: The table's name or ID was not found:
> ```
> {
>     "error_msg": "table not found"
> }
> ```

## Create A View

Create a new view in the current table.


**URL Structure**

> **\[POST]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/views/



**Request Authentication**

> Base Access Token


**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/views/?table_name=Table1' \
> -d '{ \
>   "name": "A New View" \
> }'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**table_id** OR **table_name** _\[string, required]_
> The ID or the name of the table.

**viewData** _\[JSON object, required]_
> In this JSON object, define the new view with the following params:
> 
> **name** _\[string, required]_
> > The name of this view.
> 
> **is_locked** _\[enum(`true`, `false`), optional, `false` by default]_
> > If this view will be locked.
> 
> **filters** and **filter_conjunction** _\[list, optional]_
> > Refer to the list of filters and filter conjunctions in the API request **List Rows by Filters**.
> 
> **hidden_columns** _\[list, optional]_
> > The IDs of the columns that should be hidden in this view.
> 
> **sorts** _\[array, optional]_
>> In this array, define two params if needed: `column_key` (the ID of the column to be sorted), and `sort_type` (if the sorting should be ascending with `up` or descending with `down`).
> 
> **groupbys** _\[array, optional]_
>> In this array, define the column used to group the records with two params if needed: `column_key` (the ID of the column to group by), and `sort_type` (if the sorting should be ascending with `up` or descending with `down`).



**Return Values**

JSON-object with the details of the new view. The `_id` is the automatically generated ID of the view.


**Sample Response (200)**

> ```
> {
>     "_id": "obW4",
>     "name": "testView",
>     "type": "table",
>     "is_locked": false,
>     "rows": [],
>     "formula_rows": {},
>     "summaries": [],
>     "filter_conjunction": "And",
>     "sorts": [],
>     "filters": [],
>     "hidden_columns": [],
>     "groupbys": [],
>     "group_rows": [],
>     "groups": []
> }
> ```


**Possible Errors**

400 Bad Request: A view with the same name already exists:
> ```
> {
>     "error_msg": "view already exists"
> }
> ```

403 Forbidden: Probably the access token or the ID of the base was wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

404 Not Found: The table was not found by its name or ID:
> ```
> {
>     "error_msg": "table not found"
> }
> ```

## Get A View by View Name

Get the details of a view by its name.


**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/views/`<view_name>`/


**Request Authentication**

> Base Access Token



**Sample Request**

> ```
> curl \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/views/Default View/?table_name=Table1
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**table_id** OR **table_name** _\[string, required]_
> The ID or the name of the table.

**view_name** _\[string, required]_
> The name of this view.


**Sample Response (200)**

> ```
> {
>     "_id": "0000",
>     "name": "Default View",
>     "type": "table",
>     "is_locked": false,
>     "rows": [],
>     "formula_rows": {},
>     "summaries": [],
>     "filter_conjunction": "And",
>     "sorts": [],
>     "filters": [],
>     "hidden_columns": [],
>     "groupbys": [],
>     "group_rows": [],
>     "groups": []
> }
> ```


**Possible Errors**

403 Forbidden: Probably the access token or the ID of the base was wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

404 Not Found: The table was not found by its name or ID:
> ```
> {
>     "error_msg": "table not found"
> }
> ```

404 Not Found: The view was not found under the given name:
> ```
> {
>     "error_msg": "view not found"
> }
> ```



## Update A View

Change the details of a view: the name, permission, filters, hidden columns, sorts and groupbys.


**URL Structure**

> **\[PUT]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/views/`<view_name>`/



**Request Authentication**

> Base Access Token


**Sample Request**

> ```
> curl -X PUT \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/views/testView/?table_name=Table1'
> -d '{ \ 
>     "name": "testView", \
>     "is_locked": true, \
>     "filters": [], \
>     "filter_conjunction": "Or", \
>     "sorts": [ \
>         { \
>             "column_key": "0000", \
>             "sort_type": "up" \
>         } \
>     ], \
>     "hidden_columns": [ \
>         "uSYH" \
>     ], \
>     "groupbys": [ \
>         { \
>             "column_key": "0000", \
>             "sort_type": "up" \
>         } \
>     ] \
> }'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**table_id** OR **table_name** _\[string, required]_
> The ID or the name of the table.

**view_name** _\[string, required]_
> The name of this view.

**viewData** _\[JSON object, required]_
> In this JSON object, choose one or more following params to update:
> 
> **name** _\[string, required]_
> > The name of this view.
> 
> **is_locked** _\[enum(`true`, `false`), optional, `false` by default]_
> > If this view will be locked.
> 
> **filters** and **filter_conjunction** _\[list, optional]_
> > Refer to the list of filters and filter conjunctions in the API request **List Rows by Filters**.
> 
> **hidden_columns** _\[list, optional]_
> > The IDs of the columns that should be hidden in this view.
> 
> **sorts** _\[array, optional]_
>> In this array, define two params if needed: `column_key` (the ID of the column to be sorted), and `sort_type` (if the sorting should be ascending with `up` or descending with `down`).
> 
> **groupbys** _\[array, optional]_
>> In this array, define the column used to group the records with two params if needed: `column_key` (the ID of the column to group by), and `sort_type` (if the sorting should be ascending with `up` or descending with `down`).



**Return Values**

JSON-object with the details of the updated view.



**Sample Response (200)**

> ```
> {
>     "_id": "O3OV",
>     "name": "testView",
>     "type": "table",
>     "is_locked": true,
>     "rows": [],
>     "formula_rows": {},
>     "summaries": [],
>     "filter_conjunction": "Or",
>     "sorts": [
>         {
>             "column_key": "0000",
>             "sort_type": "up"
>         }
>     ],
>     "filters": [],
>     "hidden_columns": [
>         "uSYH"
>     ],
>     "groupbys": [
>         {
>             "column_key": "0000",
>             "sort_type": "up"
>         }
>     ],
>     "group_rows": [],
>     "groups": []
> }
> ```


**Possible Errors**

403 Forbidden: Probably the access token or the ID of the base was wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

404 Not Found: The table was not found by its name or ID:
> ```
> {
>     "error_msg": "table not found"
> }
> ```

## Delete A View

Delete an existing view.


**URL Structure**

> **\[DELETE]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/views/`<view_name>`/




**Request Authentication**

> Base Access Token


**Sample Request**

> ```
> curl -X DELETE \
> -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/views/testView/?table_name=Table1'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**table_id** OR **table_name** _\[string, required]_
> The ID or the name of the table.

**view_name** _\[string, required]_
> The name of this view.



**Return Values**

JSON-object with the result of the operation.


**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```
If a view doesn't exist or is already deleted, the same response is returned without error message.



**Possible Errors**

403 Forbidden: Probably the access token or the ID of the base was wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

404 Not Found: The table was not found by its name or ID:
> ```
> {
>     "error_msg": "table not found"
> }
> ```