# Base notification rules

## List Base notification rules in a Base

**URL Structure**

> **\[GET] **api/v2.1/workspace/\<workspace_id>/dtable/\<name>/notification-rules/

**Request Authentication**

> User Authentication (Token)

**Sample request**

> ```
> curl 
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' 
> -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/notification-rules/"
>
> ```

**Input Parameters**

**workspace_id** _\[int, required]_

> The ID of the workspace where the base is stored.

**name** _\[string, required]_

> The name of the base.

**Return Values**

JSON-object with the list of dtable notification_ _rules' details.

**Sample Response (200)**

```
{
    "dtable_notification_rule_list": [
        {
            "id": 2,
            "dtable": "t1",
            "run_condition": "per_day",
            "trigger": {
                "rule_name": 'xxx',
                "condition": "rows_modified",
                "table_id": 0,
                "view_id": 0
            },
            "action": {
                "type": "notify",
                "users": [
                    "foo@foo.com"
                ]
            },
            "creator": "admin",
            "ctime": "2020-04-29T03:00:42+00:00",
            "last_scan_time": ""
        }
    ]
}

```

## Add a Base notification rule

**URL Structure**

> **\[POST] **api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/notification-rules/

**Request Authentication**

> User Authentication (Token)

**Sample request**

> ```
> curl 
> -X POST 
> -d 
> '{
> 	"run_condition": "per_day",
> 	"trigger": {
> 		"rule_name": 'xxx'
> 		"condition": "rows_modified",
> 		"table_id":0,
> 		"view_id":0
> 	},
> 	"action": {
> 		"type":"notify",
> 		"users":["foo@foo.com"]
> 	}
> }'
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/notification-rules/"
>
> ```

**Input Parameters**

**workspace_id** _\[int, required]_

> The ID of the workspace where the base is stored.

**name** _\[string, required]_

> The name of the base.

**Return Values**

JSON-object of the Base notification rule' details.

**Sample Response (200)**

```
{
        "id": 2,
        "dtable": "t1",
        "run_condition": "per_day",
        "trigger": {
            "rule_name": 'xxx'
            "condition": "rows_modified",
            "table_id": 0,
            "view_id": 0
        },
        "action": {
            "type": "notify",
            "users": [
                "foo@foo.com"
            ]
        },
        "creator": "admin",
        "ctime": "2020-04-29T03:00:42+00:00",
        "last_trigger_time": ""
}

```

## Update a Base notification rule

**URL Structure**

> **\[PUT] **api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/notification-rules/\<dtable_notification_rule_id>/

**Request Authentication**

> User Authentication (Token)

**Sample request**

> ```
> curl -X PUT -d 
> '{
> 	"run_condition": "per_day",
> 	"trigger": {
> 		"rule_name": 'xxx'
> 		"condition": "rows_modified",
> 		"table_id":"0000",
> 		"view_id":"0000"
> 	},
> 	"action": {
> 		"type":"notify",
> 		"users":["foo@foo.com"]
> 	}
> }'
>  -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/notification-rules/2/"
>
> ```

**Input Parameters**

**workspace_id** _\[int, required]_

> The ID of the workspace where the base is stored.

**name** _\[string, required]_

> The name of the base.

**Return Values**

JSON-object of the Base notification rule' details.

**Sample Response (200)**

```
{
        "id": 2,
        "dtable": "t1",
        "run_condition": "per_day",
        "trigger": {
            "rule_name": 'xxx'
            "condition": "rows_modified",
            "table_id": "0000",
            "view_id": "0000"
        },
        "action": {
            "type": "notify",
            "users": [
                "foo@foo.com"
            ]
        },
        "creator": "admin",
        "ctime": "2020-04-29T03:00:42+00:00",
        "last_trigger_time": ""
}

```

## Delete a Base notification rule

**URL Structure**

> **\[DELETE] **api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/notification-rules/\<dtable_notification_rule_id>/

**Request Authentication**

> User Authentication (Token)

**Sample request**

> ```
> curl 
> -X DELETE -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' 
> -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/notification-rules/1/"
>
> ```

**Input Parameters**

**workspace_id** _\[int, required]_

> The ID of the workspace where the base is stored.

**name** _\[string, required]_

> The name of the base.

**Return Values**

JSON-object of the Base notification rule' details.

**Sample Response (200)**

```
{
    "success": true
}

```


