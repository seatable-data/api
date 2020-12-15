# Plugins Management

## List Plugins in a Base

List all the plugins added in a base.


**URL Structure**

> **\[GET]** api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/plugins/


**Request Authentication**

> User Authentication (Token)

**Sample Request**

List all the plugins added in the base `Stores` in the workspace `1`:

> ```
> curl 
> -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' \
> -H 'Accept: application/json; indent=4' \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Stores/plugins/"
> ```

**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.


**Return Values**

JSON-object with the list of plugins' details.


**Sample Response (200)**

```
{
    "plugin_list": [
        {
            "id": 2,
            "plugin_name": "dedede",
            "info": {
                "name": "dedede",
                "desc": "my desc",
                "last_modified": "2020-01-01"
            },
            "added_by": "foo",
            "added_time": "2020-01-13T07:55:50+00:00"
        }
    ]
}
```

**Possible Errors**

* 403 Permission Denied.
* 500 Internal Server Error.

## Add a Plugin to a DTable

**POST** api/v2.1/workspace/:workspace_id/dtable/:name/plugins/

* workspace_id
* name, dtable_name
* plugin, binary zip file

**Sample Request**

```
curl -X POST -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' -H "Content-Type: multipart/form-data" -F "plugin=@/home/plugin.zip" "https://cloud.seatable.io/api/v2.1/workspace/2/dtable/gt1/plugins/"

```

**Sample Response (200)**

```json
{
    "id": 2,
    "plugin_name": "dedede",
    "info": {
        "name": "dedede",
        "desc": "my desc",
        "last_modified": "2020-01-01"
    },
    "added_by": "foo",
    "added_time": "2020-01-13T07:55:50+00:00"
}

```

**Possible Errors**

* 400 Plugin invalid.
* 403 Permission Denied.
* 500 Internal Server Error.

## Update a Plugin

**PUT **api/v2.1/workspace/:workspace_id/dtable/:name/plugins/:plugin_id/

* workspace_id
* name, dtable_name
* plugin, binary zip file

**Sample Request**

```
curl -X PUT -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' -H "Content-Type: multipart/form-data" -F "plugin=@/home/plugin.zip" "https://cloud.seatable.io/api/v2.1/workspace/2/dtable/gt1/plugins/2/"

```

**Sample Response (200)**

```json
{
    "id": 2,
    "plugin_name": "new plugin",
    "info": {
        "name": "new plugin",
        "desc": "my desc",
        "last_modified": "2020-01-01"
    },
    "added_by": "foo",
    "added_time": "2020-01-13T07:55:50+00:00"
}

```

**Possible Errors**

* 400 Plugin invalid.
* 403 Permission Denied.
* 500 Internal Server Error.

## Delete a Plugin

**DELETE** api/v2.1/workspace/:workspace_id/dtable/:name/plugins/:plugin_id/

* workspace_id
* name, dtable_name
* plugin_id

**Sample Request**

```
curl -X DELETE -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' "https://cloud.seatable.io/api/v2.1/workspace/2/dtable/gt1/plugins/1/"

```

**Sample Response (200)**

```json
{'success': true}

```

**Possible Errors**

* 403 Permission Denied.
* 500 Internal Server Error.


