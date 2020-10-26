# Rows

You can find the data format for row in <https://docs.seatable.io/published/dtable-sdk/data-structure.md>

## List rows

### List rows in a view

**GET** [https://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/rows/](https://cloud.seatable.com/api/v1/dtables/:dtable_uuid/rows/)

* dtable_uuid
* table_name, necessary
* view_name, optional, if not given, "Default View"'s rows will be returned

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/rows/?table_name=Table1

```

**Sample response**

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

**GET** [https://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/filtered-rows/](https://cloud.seatable.com/api/v1/dtables/:dtable_uuid/filtered-rows/)

* dtable_uuid
* table_name, necessary
* view_name, optional, if not given, "Default View"'s rows will be returned
* filters, a list of filters.
* filter_conjunction, 'And' or 'Or'

A filter contains four fields `column_name` , `filter_predicate` , `filter_term` , `filter_term_modifier` . For different column types, different `filter_predicate`, `filter_term` , `filter_term_modifier` are supported.

**Text**

* filter_predicate: contains, does_not_contain, is, is_not, is_empty, is_not_empty
* filter_term: a string or an empty string
* filter_term_modifier: an empty string

**Number**

* filter_predicate: equal, not_equal, less, greater, less_or_equal, greater_or_equal, is_empty, is_not_empty
* filter_term: a string containing the number  (like "10") or an empty string
* filter_term_modifier: an empty string



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

**Sample response**

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

**GET** [https://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/rows/](https://cloud.seatable.com/api/v1/dtables/:dtable_uuid/rows/)

* dtable_uuid
* table_name, necessary
* view_name, optional, if not given, "Default View"'s rows will be returned
* grouping, if grouping is true and the view is a grouped view, grouped rows will be returned

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/rows/?table_name=Table1&grouping=true

```

**Sample response**

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

**POST** <https://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/rows/>

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

**Sample response**

```
{
     '0000': 'I am new Row', 
     '_id': 'MeKKGQ5gRSyeuREenGAk4w'
}

```

## Insert a row

**POST** [https://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/rows/](https://cloud.seatable.com/api/v1/dtables/:dtable_uuid/rows/)

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

**Sample response**

```
{
    '0000': 'I am new Row', 
    '_id': 'L_nn31N2TbyNA1Nmm-NTtg'
}

```

## Update a row

**PUT** <https://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/rows/>

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

**Sample response**

```
{
    "success": true
}

```

## Delete a row

**DELETE** <https://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/rows/>

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

**Sample response**

```
{
    "success": true
}

```

## Add a row link

**POST** <https://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/links/>

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

**Sample response**

```
{
    "success": true
}

```

## Delete a row link

**DELETE** <https://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/links/>

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

**Sample response**

```
{
    "success": true
}

```

## List deleted rows

**GET** <https://cloud.seatable.io/dtable-server/api/v1/dtables/:dtable_uuid/deleted-rows/>

**Request Parameters**

* dtable_uuid
* page: page number, default 1, optional
* per_page: number of rows per page, default 25, optional

**Sample Request**

```
curl -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ' "https://cloud.seatable.io/dtable-server/api/v1/dtables/46620d70c8e549ab88749d4a2dc4608c/deleted-rows/"

```

**Sample Response**

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


