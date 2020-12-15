# Rows

You can find the data format for row in <https://docs.seatable.io/published/dtable-sdk/data-structure.md>

## List rows

### List rows in a view

**GET** /dtable-server/api/v1/dtables/:dtable_uuid/rows/

* dtable_uuid
* table_name, necessary
* view_name, optional, if not given, "Default View"'s rows will be returned

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/rows/?table_name=Table1

```

**Sample Response (200)**

```
{
    "rows": [
        {
            "_id": "NAu2B3OcRG6UrWagL-9naA",
            "Name": "212ws1"
        },
        {
            "_id": "P3rdZ2ZKR_Cx923ID04ruA",
            "Name": "212ws1"
        },
    ]
}

```

### List rows by filters

**GET** /dtable-server/api/v1/dtables/:dtable_uuid/filtered-rows/

* dtable_uuid
* table_name, necessary
* view_name, optional, if not given, "Default View"'s rows will be returned
* filters, a list of filters.
* filter_conjunction, 'And' or 'Or'

A filter contains four fields `column_name` , `filter_predicate` , `filter_term` , `filter_term_modifier` . For different column types, different `filter_predicate`, `filter_term` , `filter_term_modifier` are supported.

**Text、Geolocation**

* filter_predicate: contains, does_not_contain, is, is_not, is_empty, is_not_empty
* filter_term: a string or an empty string
* filter_term_modifier: an empty string

**Number**

* filter_predicate: equal, not_equal, less, greater, less_or_equal, greater_or_equal, is_empty, is_not_empty
* filter_term: a string containing the number  (like "10") or an empty string
* filter_term_modifier: an empty string

**Checkbox**

* filter_predicate: is
* filter_term: true or false
* filter_term_modifier: an empty string

**Single-select**

* filter_predicate: is, is_not, is_empty, is_not_empty
* filter_term: a string containing the name of option (like "seaTable") or an empty string
* filter_term_modifier: an empty string

**Multiple-select**

* filter_predicate: has_any_of, has_all_of, has_none_of, is_exactly, is_empty, is_not_empty
* filter_term: an array that some items are the names of options or an empty array or an empty string
* filter_term_modifier: an empty string

**Date、Ctime、Mtime**

* filter_predicate: is, is_within, is_before, is_after, is_on_or_before, is_on_or_after, is_not, is_empty, is_not_empty
* filter_term: a date string (like "2020-10-27 12:00") or an empty string
* filter_term_modifier: changes with the change of filter_predicate

   if filter_predicate is 'is_within', it can be one of the_past_week, the_past_month, the_past_year, this_week, this_month,    this_year, the_next_week, the_next_month, the_next_year, the_next_numbers_of_days, the_past_numbers_of_days.

  if filter_predicate is 'is_empty' or 'is_not_empty', it is an empty string.

  Otherwise,  it can be one of today, tomorrow, yesterday, one_week_ago, one_week_from_now, one_month_ago, one_month_from_now, number_of_days_ago, number_of_days_from_now, exact_date or an empty string.

**Collaborator**

* filter_predicate:  has_any_of, has_all_of, has_none_of, is_exactly, is_empty, is_not_empty, include_me
* filter_term: an array or an empty array or an empty string
* filter_term_modifier: an empty string

**Creator、Last_modifier**

* filter_predicate: contains, dost_not_contain, include_me, is, is_not
* filter_term: an array or an empty array or an empty string
* filter_term_modifier: an empty string

**Formula**

* If the result type is 'string' or 'bool', process according to the text column type.
* If the result type is 'date', process according to the date column type.
* If the result type is 'number', process according to the number column type.

**Link**

* filter_predicate: contains, dost_not_contain, is_empty, is_not_empty
* filter_term: a string or an empty string
* filter_term_modifier: an empty string

**Auto-number**

* filter_predicate: contains, dost_not_contain, is, is_not
* filter_term: a string or an empty string
* filter_term_modifier: an empty string

**File、Image、Long_text、URL**

* not support 

**Sample request**

```
curl -H "Content-Type: application/json" -d 
`{
	"filters":[
		{
			"column_name": "Name",
			"filter_predicate": "contains",
			"filter_term": "a",
			"filter_term_modifier": ""	
		},
		{
			"column_name": "Name",
			"filter_predicate": "contains",
			"filter_term": "b",
			"filter_term_modifier": ""	
		}
	],
	"filter_conjunction": "Or"
}`
 -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/filtered-rows/?table_name=Table1

```

**Sample Response (200)**

```
{
    "rows": [
        {
            "_id": "ELtcMWQOQm2qbJEn56QW9A",
            "Name": "b"
        },
        {
            "_id": "NwI3PS_KTY-DtTqxo6n9_g",
            "Name": "a"
        },
        {
            "_id": "C6GXtPi7RJS80bQQcrLkmw",
            "Name": "a"
        }
    ]
}

```

### List grouped rows in a view

**GET** /dtable-server/api/v1/dtables/:dtable_uuid/rows/

* dtable_uuid
* table_name, necessary
* view_name, optional, if not given, "Default View"'s rows will be returned
* grouping, if grouping is true and the view is a grouped view, grouped rows will be returned

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/rows/?table_name=Table1&grouping=true

```

**Sample Response (200)**

```
{
    "groups": [
        {
            "column_name": "Name",
            "column_key": "0000",
            "cell_value": "a",
            "rows": [
                {
                    "_id": "NwI3PS_KTY-DtTqxo6n9_g",
                    "Name": "a"
                },
                {
                    "_id": "C6GXtPi7RJS80bQQcrLkmw",
                    "Name": "a"
                }
            ]
        },
        {
            "column_name": "Name",
            "column_key": "0000",
            "cell_value": "b",
            "rows": [
                {
                    "_id": "ELtcMWQOQm2qbJEn56QW9A",
                    "Name": "b"
                }
            ]
        }
    ]
}

```

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
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/rows/

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
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/rows/

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
curl --request POST ' https://cloud.seatable.io/dtable-server/api/v1/dtables/41cd05dab29a4428bc31bd66f4600817/batch-append-rows/' --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MDQxMTUwMTcsImR0YWJsZV91dWlkIjoiNDFjZDA1ZGFiMjlhNDQyOGJjMzFiZDY2ZjQ2MDA4MTciLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.jAIndSyeNivFnAb9f3nF8MENYK2I26JS8BLUyo7aJRw' --header 'Content-Type: application/json' --data-raw '{
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
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/rows/

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
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/rows/

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
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/batch-delete-rows/

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
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/links/

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
}' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/links/

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
curl -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ' "https://cloud.seatable.io/dtable-server/api/v1/dtables/46620d70c8e549ab88749d4a2dc4608c/deleted-rows/"

```

**Sample Response (200)**

```
{
    "deleted_rows": [
        {
            "id": 37,
            "dtable_uuid": "46620d70c8e549ab88749d4a2dc4608c",
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


