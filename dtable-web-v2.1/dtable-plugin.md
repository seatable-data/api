# Plugins

## List Plugins in a DTable

**GET** api/v2.1/workspace/:workspace_id/dtable/:name/plugins/

* workspace_id
* name, dtable_name

**Sample request**

```
curl -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' -H 'Accept: application/json; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/2/dtable/gt1/plugins/"

```

**Sample response**

```json
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

**Errors**

* 403 Permission Denied.
* 500 Internal Server Error.

## Add a Plugin to a DTable

**POST** api/v2.1/workspace/:workspace_id/dtable/:name/plugins/

* workspace_id
* name, dtable_name
* plugin, binary zip file

**Sample request**

```
curl -X POST -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' -H "Content-Type: multipart/form-data" -F "plugin=@/home/plugin.zip" "https://cloud.seatable.io/api/v2.1/workspace/2/dtable/gt1/plugins/"

```

**Sample response**

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

**Errors**

* 400 Plugin invalid.
* 403 Permission Denied.
* 500 Internal Server Error.

## Update a Plugin

**PUT **api/v2.1/workspace/:workspace_id/dtable/:name/plugins/:plugin_id/

* workspace_id
* name, dtable_name
* plugin, binary zip file

**Sample request**

```
curl -X PUT -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' -H "Content-Type: multipart/form-data" -F "plugin=@/home/plugin.zip" "https://cloud.seatable.io/api/v2.1/workspace/2/dtable/gt1/plugins/2/"

```

**Sample response**

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

**Errors**

* 400 Plugin invalid.
* 403 Permission Denied.
* 500 Internal Server Error.

## Delete a Plugin

**DELETE** api/v2.1/workspace/:workspace_id/dtable/:name/plugins/:plugin_id/

* workspace_id
* name, dtable_name
* plugin_id

**Sample request**

```
curl -X DELETE -H 'Authorization:Token 0303f89b3607fb86039fdffcf1be6383797b437f' "https://cloud.seatable.io/api/v2.1/workspace/2/dtable/gt1/plugins/1/"

```

**Sample response**

```json
{'success': true}

```

**Errors**

* 403 Permission Denied.
* 500 Internal Server Error.


