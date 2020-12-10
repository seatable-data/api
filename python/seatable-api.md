# SeaTable API Python

This Python package is a wrapper for the SeaTable Restful API.

## Quickstart

### Installation

```
pip3 install seatable-api

```

**Requirements**

* Python >= 3.5
* requests
* socketIO-client-nexus

### Examples

```
from seatable_api import Base


# auth first

server_url = 'https://docs.seatable.io/'
api_token = 'xxxxxx'

base = Base(api_token, server_url)
base.auth()



# list rows

table_name = 'Users'
rows = base.list_rows(table_name)



# update a row

row = rows[0]
row_id = row['_id']                        # Row ID

row_data = {
    "Name": "Update Row",                  # Column key and cell content
    "Email": "seatable@seatable.com",
}
base.update_row(table_name, row_id, row_data)

```

## Data Format

You can find the data format for row, column and table in <https://docs.seatable.io/published/dtable-sdk/data-structure.md>

## API

### Auth

```
from seatable_api import Base

server_url = 'https://docs.seatable.io/'
api_token = 'xxxxxx'

base = Base(api_token, server_url)
base.auth()

```

**Sample params**

* server_url:  `str` , SeaTable server url
* api_token:  `str` , SeaTable API token

**Sample return**

* None

### Connect Websocket

```
from seatable_api import Base
from seatable_api.constants import UPDATE_DTABLE

server_url = 'https://docs.seatable.io/'
api_token = 'xxxxxx'

base = Base(api_token, server_url)
base.auth(with_socket_io=True)


# You can overwrite this event
def on_update_seatable(data, index, *args):
    print(data)


base.socketIO.on(UPDATE_DTABLE, on_update_seatable)
base.socketIO.wait()  # forever
# base.socketIO.wait(seconds=10)  # limit

```

**Sample params**

* server_url:  `str` , SeaTable server url
* api_token:  `str` , SeaTable API token

**Sample return**

* `dict`


```
{
     "op_type":"insert_row",
     "table_id":"0000",
     "row_id":"",
     "row_insert_position":"insert_below",
     "row_data":{"_id":"cdZgLNPdSxSAQC_LnFOeCw","_participants":[],"_creator":"seafile@seafile.com","_ctime":"","_last_modifier":"seafile@seafile.com"},
     "view_index":0
}

```

### List rows of a table

```
# Without view_name

table_name = 'Users'
rows = base.list_rows(table_name)

```

```
# With view_name

table_name = 'Users'
view_name = 'Default'
rows = base.list_rows(table_name, view_name)

```

**Sample params**

* table_name:  `str`  (case sensitive)
* view_name:  `str`  (case sensitive), optional, if not given, "Default View"'s rows will be returned

**Sample return**

* `list` 


```
[
    {
        "_id": "NAu2B3OcRG6UrWagL-9naA",    # Row ID
        "Name": "seatable"                  # Column key and cell content
    },
    {
        "_id": "P3rdZ2ZKR_Cx923ID04ruA",
        "Name": "seafile"
    },
]

```

### List filtered rows of a table

If you want to get rows that meet a certain condition, you can use this API

```
# Without view_name

table_name = 'Table1'
filters = [
    {
        "column_name": "Name",
        "filter_predicate": "contains",
        "filter_term": "a",
    },
    {
        "column_name": "Name",
        "filter_predicate": "contains",
        "filter_term": "b",
    }
]

filtered_rows = base.filter_rows(table_name, filters=filters, filter_conjunction='Or')

```

```
# With view_name

table_name = 'Table1'
view_name = 'Default'
filters = [
    {
        "column_name": "Name",
        "filter_predicate": "contains",
        "filter_term": "a",
    },
    {
        "column_name": "Name",
        "filter_predicate": "contains",
        "filter_term": "b",
    }
]

filtered_rows = base.filter_rows(table_name, view_name, filters=filters, filter_conjunction='Or')

```

**Sample params**

* table_name:  `str`  (case sensitive)
* view_name:  `str`  (case sensitive), optional, if not given, "Default View"'s rows will be returned
* filters: `list`, of which elements are `dicts`
* filter_conjunction: `str`, `"And"`or`"Or"`, default is `"And"`

**Sample return**

* `list` 


```
[
    {
        "_id": "NAu2B3OcRG6UrWagL-9naA",    # Row ID
        "Name": "a"                  		# Column key and cell content
    },
    {
        "_id": "P3rdZ2ZKR_Cx923ID04ruA",
        "Name": "b"
    },
]

```

### Append a row

```
table_name = 'Users'

row_data = {
    "Name": "I am new Row"
}

base.append_row(table_name, row_data)

```

**Sample params**

* table_name:  `str`  (case sensitive)
* row_data:  `dict`  (column key in `dict` case sensitive)

**Sample return**

* `dict` 


```
{'0000': 'I am new Row', '_id': 'L_nn31N2TbyNA1Nmm-NTtg'}

```

### Batch append rows

```
table_name = 'Users'

rows_data = [
    {"Name": "I am new Row"},
    {"Name": "I am an another new Row"}
]

base.batch_append_rows(table_name, rows_data)

```

**Sample params**

* table_name:  `str`  (case sensitive)
* rows_data:  `list` 

**Sample return**

* `list` 


```
[
    {'0000': 'I am new Row', '_id': 'L_nn31N2TbyNA1Nmm-NTtg'},
    {'0000': 'I am an another new Row', '_id': '2ZKR_Cx923ID04ruA-NTtg'}
]

```

### Insert a row

```
table_name = 'Users'

row_data = {
    "Name": "I am another new Row"
}

anchor_row = rows[0]
anchor_row_id = anchor_row['_id']

base.insert_row(table_name, row_data, anchor_row_id)

```

**Sample params**

* table_name:  `str`  (case sensitive)
* row_data:  `dict`  (column key in `dict` case sensitive)
* anchor_row_id:  `str`  (case sensitive), insert below anchor row

**Sample return**

* `dict` 


```
{'0000': 'I am another new Row', '_id': 'MeKKGQ5gRSyeuREenGAk4w'}

```

### Update a row

```
table_name = 'Users'

row_data = {
    "Name": "Update Row"
}

row = rows[1]
row_id = row['_id']

base.update_row(table_name, row_id, row_data)

```

**Sample params**

* table_name:  `str`  (case sensitive)
* row_id:  `str`  (case sensitive)
* row_data:  `dict`  (column key in `dict` case sensitive)

**Sample return**

* `dict` 


```
{"success": True}

```

### Delete a row

```
table_name = 'Users'

row = rows[1]
row_id = row['_id']

base.delete_row(table_name, row_id)

```

**Sample params**

* table_name:  `str`  (case sensitive)
* row_id:  `str`  (case sensitive)

**Sample return**

* `dict` 


```
{"success": True}

```

### Batch delete rows

```
table_name = 'Users'

del_rows = rows[:3]
row_ids = [row['_id'] for row in del_rows]

base.batch_delete_rows(table_name, row_ids)

```

**Sample params**

* table_name:  `str`  (case sensitive)
* row_ids:  `list`  (row_id in `list` case sensitive)

**Sample return**

* `dict` 


```
{"success": True}

```

### Get base metadata

```
base.get_metadata()

```

**Sample params**

* null

**Sample return**

* `dict` 


```
{'tables': [{'_id': '0000',
             'columns': [{'editable': True,
                          'key': '0000',
                          'name': 'Name',
                          'resizable': True,
                          'type': 'text',
                          'width': 200},
                         {'data': {'display_column_key': '0000',
                                   'is_internal_link': True,
                                   'link_id': 'Q4ME',
                                   'other_table_id': 'thI2',
                                   'table_id': '0000'},
                          'draggable': True,
                          'editable': True,
                          'key': '9f8B',
                          'name': 'Foreign Key',
                          'resizable': True,
                          'type': 'link',
                          'width': 200}],
             'name': 'Table1',
             'views': [{'_id': '0000',
                        'filter_conjunction': 'And',
                        'filters': [],
                        'formula_rows': {},
                        'groupbys': [],
                        'groups': [],
                        'hidden_columns': [],
                        'is_locked': False,
                        'name': 'Default',
                        'rows': [],
                        'sorts': [],
                        'summaries': [],
                        'type': 'table'}]},
     ]
}

```

### Convert row

Convert websocket row data to readable row data

```
from seatable_api import Base
from seatable_api.constants import UPDATE_DTABLE
from seatable_api.utils import convert_row

server_url = 'https://docs.seatable.io/'
api_token = 'xxxxxx'

base = Base(api_token, server_url)
base.auth(with_socket_io=True)


# You can overwrite this event
def on_update_seatable(data, index, *args):
    row = convert_row(metadata, data)
    print(row)


global metadata
metadata = base.get_metadata()

base.socketIO.on(UPDATE_DTABLE, on_update_seatable)
base.socketIO.wait()

```

**Sample params**

* server_url:  `str` , seatable server url
* api_token:  `str` , seatable api token

**Sample return**

* `dict`


```
{
    '_id': 'NeWm5ZgDTHmbCY28wU2aew', 'table_name': 'Table1', 'op_type': 'insert_row'
}

```

```
{
    '_id': 'NeWm5ZgDTHmbCY28wU2aew', 'table_name': 'Table1', 'op_type': 'modify_row', 'Name': 'new name'
}

```

### Add a link

```
table_name = 'Table1'
other_table_name = 'Table2'
column_name = 'Foreign Key'

# get column link_id from metadata
# note, the link_id will not change after created, 
# you can get the link_id once and save it in your config file
metadata = base.get_metadata()️
table = None
for item in metadata['tables']:
    if item['name'] == table_name:
        table = item
        break

column = None
for item in table['columns']:
    if item['name'] == column_name:
        column = item
        break

link_id = column['data']['link_id']

# get row
rows = base.list_rows(table_name)
other_rows = base.list_rows(other_table_name)
row_id = rows[0]['_id']
other_row_id = other_rows[0]['_id']

base.add_link(link_id, table_name, other_table_name, row_id, other_row_id)

```

**Sample params**

* link_id: `str` 
* table_name:  `str`  (case sensitive)
* other_table_name:  `str`  (case sensitive)
* row_id:  `str` 
* other_row_id:  `str` 

**Sample return**

* `dict` 


```
{"success": True}

```

### Remove a link

```
table_name = 'Table1'
other_table_name = 'Table2'
column_name = 'Foreign Key'

# get column link_id from metadata
metadata = base.get_metadata()️
table = None
for item in metadata['tables']:
    if item['name'] == table_name:
        table = item
        break

column = None
for item in table['columns']:
    if item['name'] == column_name:
        column = item
        break

link_id = column['data']['link_id']

# get row
rows = base.list_rows(table_name)
other_rows = base.list_rows(other_table_name)
row_id = rows[0]['_id']
other_row_id = other_rows[0]['_id']

base.remove_link(link_id, table_name, other_table_name, row_id, other_row_id)

```

**Sample params**

* link_id: `str` 
* table_name:  `str`  (case sensitive)
* other_table_name:  `str`  (case sensitive)
* row_id:  `str` 
* other_row_id:  `str` 

**Sample return**

* `dict` 


```
{"success": True}

```

### Get file download link by path

```
path = '/files/2020-02/test_pic.jpg'
download_link = base.get_file_download_link(path)

```

**Sample params**

* path:  `str`  (case sensitive)

**Sample return**

* `str`  


```
https://cloud.seatable.io/seafhttp/files/498fe8b6-68f4-4878-8ce7-91517b9c6e1c/test_pic.jpg

```

### Get file upload link

```
upload_link = base.get_file_upload_link()

```

**Sample return**

* `dict`  


```
{
    'upload_link': 'https://cloud.seatable.io/seafhttp/upload-api/19f3a6a8-354d-4bc4-9554-282a3e835fc1', 
    'parent_path': '/asset/e5e26c89-6afb-47be-a3e9-af78b71c0f5a'
}

```


