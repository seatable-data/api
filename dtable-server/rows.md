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
> ```


**Possible Errors**

400 Bad Request: Parameters were not correctly given:
> ```
> {
>     "error_msg": "params invalid"
> }
> ```

403 Forbidden: The permission to the table was denied:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

404 Not Found: The table was not found under the given `table_name`:
> ```
> {
>     "error_msg": "table not found"
> }
> ```

### List Rows by Filters

Apply filtering conditions when listing the rows. A filter contains four fields `column_name` , ``filter_predicate`` , ``filter_term`` , and ``filter_term_modifier`` . For different column types, different ``filter_predicate``, ``filter_term`` , and ``filter_term_modifier`` are supported.


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
> 
>>   if `filter_predicate` is 'is_within', it can be one of the_past_week, the_past_month, the_past_year, this_week, this_month,    this_year, the_next_week, the_next_month, the_next_year, the_next_numbers_of_days, the_past_numbers_of_days.
>>
>>   if `filter_predicate` is 'is_empty' or 'is_not_empty', it is an empty string.
>>
>>   Otherwise,  it can be one of today, tomorrow, yesterday, one_week_ago, one_week_from_now, one_month_ago, one_month_from_now, number_of_days_ago, number_of_days_from_now, exact_date or an empty string.
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


**filter_conjunction** _\[enum(`And`, `Or`), optional]_
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
> ```
When no record can be displayed (also because of wrong filter conditions), an empty list is returned without error message.


**Possible Errors**

400 Bad Request: The filter conjunction was not correctly given:
> ```
> {
>     "error_msg": "filter_conjunction invalid"
> }
> ```

403 Forbidden: The permission to the table was denied:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

404 Not Found: The column was not found:
> ```
> {
>     "error_msg": "column Names not found"
> }
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
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**table_name** _\[string, required]_
> The name of the table.

**view_name** _\[string, optional]_
> The name of the view. If left blank, "Default View" will be applied.

**grouping** _\[enum(`true`, `false`), required]_
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
> ```


**Possible Error**

400 Bad Request: The current view is not grouped, while `grouping=true`:
> ```
> {
>     "error_msg": "table not support group"
> }
> ```

400 Bad Request: Parameter not correct (probably wrong table name?):
> ```
> {
>     "error_msg": "params invalid"
> }
> ```

403 Forbidden: The permission to the table was denied:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

404 Not Found: The view was not found:
> ```
> {
>     "error_msg": "view not found"
> }
> ```

## Append a row

**POST** /dtable-server/api/v1/dtables/:dtable_uuid/rows/

* dtable_uuid
* table_name, necessary
* row, row data of json format

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' -H "Accept: application/json" -H "Content-type: application/json" -X POST -d '{
	"row": {"Name": "I am new Row"},
	"table_name": "Table1"
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/rows/

```

**Sample Response (200)**

```
{
     '0000': 'I am new Row', 
     '_id': 'MeKKGQ5gRSyeuREenGAk4w'
}

```

## Insert a row

**POST** /dtable-server/api/v1/dtables/:dtable_uuid/rows/

* dtable_uuid
* table_name, necessary
* row, row data in json
* anchor_row_id
* above_or_below, insert above anchor row if value is 'above', insert below anchor row if value is 'below', default is below

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' -H "Accept: application/json" -H "Content-type: application/json" -X POST -d '{
	"row": {"Name": "I am new Row"},
	"table_name": "Table1",
    "anchor_row_id": "HT5R_PjVQrOyX3_5O-t6Aw",
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/rows/

```

**Sample Response (200)**

```
{
    '0000': 'I am new Row', 
    '_id': 'L_nn31N2TbyNA1Nmm-NTtg'
}

```

## Batch append rows

**POST** /dtable-server/api/v1/dtables/:dtable_uuid/batch-append-rows/

* **dtable_uuid**
* **table_name**, necessary
* **rows**, necessary

**Sample request**

```
curl --request POST ' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/batch-append-rows/' --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDQxMTUwMTcsImR0YWJsZV91dWlkIjoiNDFjZDA1ZGFiMjlhNDQyOGJjMzFiZDY2ZjQ2MDA4MTciLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.jAIndSyeNivFnAb9f3nF8MENYK2I26JS8BLUyo7aJRw' --header 'Content-Type: application/json' --data-raw '{
    "rows": [{
                "name": "test", 
                "content": "batch append rows"
            }, {
                "name": "test", 
                "content": "batch append rows"
            }, {
                "name": "test", 
                "content": "batch append rows"
            }], 
    "table_name": "Table6"
}'

```

**Sample Response (200)**

```
{
    "inserted_row_count": 3
}

```

## Update a row

**PUT** /dtable-server/api/v1/dtables/:dtable_uuid/rows/

* dtable_uuid
* table_name, necessary
* row, row data in json
* row_id

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' -H "Accept: application/json" -H "Content-type: application/json" -X PUT -d '{
	"row": {"Name": "NewName"},
	"table_name": "Table1",
    "row_id": "HT5R_PjVQrOyX3_5O-t6Aw",
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/rows/

```

**Sample Response (200)**

```
{
    "success": true
}

```

## Delete a row

**DELETE** /dtable-server/api/v1/dtables/:dtable_uuid/rows/

* dtable_uuid
* table_name, necessary
* row_id

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' -H "Accept: application/json" -H "Content-type: application/json" -X DELETE -d '{
	"table_name": "Table1",
    "row_id": "HT5R_PjVQrOyX3_5O-t6Aw",
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/rows/

```

**Sample Response (200)**

```
{
    "success": true
}

```

## Batch delete rows

**DELETE** /dtable-server/api/v1/dtables/:dtable_uuid/batch-delete-rows/ 

* dtable_uuid
* table_name, necessary
* row_ids, necessary

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' -H "Accept: application/json" -H "Content-type: application/json" -X DELETE -d '{
	"table_name": "Table1",
    "row_ids": ["HT5R_PjVQrOyX3_5O-t6Aw", "IjFAMS5jb20iLCJkdGweffe",]
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/batch-delete-rows/

```

**Sample Response (200)**

```
{
    "success": true
}

```

## Add a row link

**POST** /dtable-server/api/v1/dtables/:dtable_uuid/links/

* dtable_uuid
* link_id, necessary
* table_name, necessary
* other_table_name, necessary
* table_row_id, necessary
* other_table_row_id, necessary

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' -H "Accept: application/json" -H "Content-type: application/json" -X POST -d '{
	"table_name": "Table1",
    "other_table_name": "Table2",
    "link_id": '1206'
    "table_row_id": "OkuYk0OWSIyi7zZKJ2NC4g",
    "other_table_row_id": "eyuMiAwaQlSSr983O03oUA"
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/links/

```

**Sample Response (200)**

```
{
    "success": true
}

```

## Delete a row link

**DELETE** /dtable-server/api/v1/dtables/:dtable_uuid/links/

* dtable_uuid
* link_id, necessary
* table_name, necessary
* other_table_name, necessary
* table_row_id, necessary
* other_table_row_id, necessary

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' -H "Accept: application/json" -H "Content-type: application/json" -X DELETE -d '{
	"table_name": "Table1",
    "other_table_name": "Table2",
    "link_id": '1206',
    "table_row_id": "OkuYk0OWSIyi7zZKJ2NC4g",
    "other_table_row_id": "eyuMiAwaQlSSr983O03oUA"
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/links/

```

**Sample Response (200)**

```
{
    "success": true
}

```

## List deleted rows

**GET** /dtable-server/api/v1/dtables/:dtable_uuid/deleted-rows/

**Request Parameters**

* dtable_uuid
* page: page number, default 1, optional
* per_page: number of rows per page, default 25, optional

**Sample Request**

```
curl -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ' "https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/deleted-rows/"

```

**Sample Response (200)**

```
{
    "deleted_rows": [
        {
            "id": 37,
            "dtable_uuid": "7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5",
            "row_id": "ZPFv2pm1SiaQpulvzkHm5Q",
            "op_user": "1@1.com",
            "op_time": "2020-03-17T10:31:35.000Z",
            "detail": {
                "table_id": "0000",
                "table_name": "test",
                "row_name": "test",
                "row_data": [
                    {
                        "column_key": "0000",
                        "column_name": "名称",
                        "column_type": "text",
                        "column_data": {},
                        "value": "test"
                    },
                    {
                        "column_key": "AKLn",
                        "column_name": "files",
                        "column_type": "file",
                        "column_data": {},
                        "value": [
                            {
                                "name": "1.html",
                                "size": 514,
                                "type": "file",
                                "url": "http://127.0.0.1:8001/workspace/1/asset/46620d70-c8e5-49ab-8874-9d4a2dc4608c/files/2020-03/1.html"
                            }
                        ]
                    }
                ]
            },
            "op_app": null
        }
    ]
}

```

## Get row by row id in a table

**GET** /api/v1/dtables/:dtable_uuid/rows/:row_id/

* dtable_uuid
* row_id
* table_id, required
* convert, whether convert column ID to column name, default is true

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/rows/J5jgoxDJTE2zUmAQISpk3g/?table_id=9GlO

```

**Sample response**

```
{
    "_id": "J5jgoxDJTE2zUmAQISpk3g",
    "_mtime": "2020-12-08T04:00:17.330+00:00",
    "Name": "3322",
    "Modifier": "0f3b01785de84940a47665ac72fa57ce@auth.local"
}

```

if convert=false

```
{
    "_id": "J5jgoxDJTE2zUmAQISpk3g",
    "_participants": [],
    "_creator": "foo@foo.com",
    "_ctime": "2020-12-02T04:02:43.582+00:00",
    "_last_modifier": "0f3b01785de84940a47665ac72fa57ce@auth.local",
    "_mtime": "2020-12-08T03:47:48.218+00:00",
    "0000": "32"
}

```


