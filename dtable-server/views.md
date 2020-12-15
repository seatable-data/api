# Views

## List views by table name or table id

**GET** /dtable-server/api/v1/dtables/:dtable_uuid/views/

* dtable_uuid
* table_name or table_id

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs' https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/views/?table_name=Table1

```

**Sample Response (200)**

```json
{
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
            "sorts": [],
            "filters": [],
            "hidden_columns": [],
            "groupbys": [],
            "group_rows": [],
            "groups": []
        }
    ]
}

```

## Create a new view

**POST** /dtable-server/api/v1/dtables/:dtable_uuid/views/

* dtable_uuid
* table_name or table_id
* viewData, json

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs'
-X POST -d 
'
{
  "name": "testView"
}
'
https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/views/?table_name=Table1

```

**Sample Response (200)**

```json
{
    "_id": "obW4",
    "name": "testView",
    "type": "table",
    "is_locked": false,
    "rows": [],
    "formula_rows": {},
    "summaries": [],
    "filter_conjunction": "And",
    "sorts": [],
    "filters": [],
    "hidden_columns": [],
    "groupbys": [],
    "group_rows": [],
    "groups": []
}

```

## Get a view by view name

**GET** /dtable-server/api/v1/dtables/:dtable_uuid/views/:view_name/

* dtable_uuid
* table_name or table_id

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs'
https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/views/Default View/?table_name=Table1

```

**Sample Response (200)**

```json
{
    "_id": "0000",
    "name": "Default View",
    "type": "table",
    "is_locked": false,
    "rows": [],
    "formula_rows": {},
    "summaries": [],
    "filter_conjunction": "And",
    "sorts": [],
    "filters": [],
    "hidden_columns": [],
    "groupbys": [],
    "group_rows": [],
    "groups": []
}

```

## Update a view

**PUT** /dtable-server/api/v1/dtables/:dtable_uuid/views/:view_name/

* dtable_uuid
* table_name or table_id

chose one or more options to update:

* name
* is_locked
* filters and filter_conjunction
* hidden_columns
* sorts
* groupbys

**Sample request**

```
curl -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs'
-X PUT -d 
'
{
    "name": "testView",
    "is_locked": true,
    "filters": [
        ],
    "filter_conjunction": "Or",
    "sorts": [
        {
            "column_key": "0000",
            "sort_type": "up"
        }
    ],
    "hidden_columns": [
        "uSYH"
    ],
    "groupbys": [
        {
            "column_key": "0000",
            "sort_type": "up"
        }
    ]
}
'
https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/views/testView/?table_name=Table1

```

**Sample Response (200)**

```json
{
    "_id": "O3OV",
    "name": "testView",
    "type": "table",
    "is_locked": true,
    "rows": [],
    "formula_rows": {},
    "summaries": [],
    "filter_conjunction": "Or",
    "sorts": [
        {
            "column_key": "0000",
            "sort_type": "up"
        }
    ],
    "filters": [],
    "hidden_columns": [
        "uSYH"
    ],
    "groupbys": [
        {
            "column_key": "0000",
            "sort_type": "up"
        }
    ],
    "group_rows": [],
    "groups": []
}

```

## Delete a view

**DELETE** /dtable-server/api/v1/dtables/:dtable_uuid/views/:view_name/

* dtable_uuid
* table_name or table_id

**Sample request**

```
curl -X DELETE -H 'Authorization: Token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IjFAMS5jb20iLCJkdGFibGVfdXVpZCI6IjYyMmYxZTZkMzM3NDQ5ZTQ5YjQyOWYyMjUzMDM3YTc2In0.3ytwzZsfZwzifAQtsLzn0AFMnEDSeHxkKlIgD6XKuIs'
https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7187a4d9fb6cfff5e5019a6d5/views/testView/?table_name=Table1

```

**Sample Response (200)**

```json
{
    "success": true
}

```


