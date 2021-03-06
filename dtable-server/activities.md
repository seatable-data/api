# Activities


## Get Activity Log

List all the activities logged in the base.


**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/operations/


**Request Authentication**

> Base Access Token


**Sample Request**
> ```
> curl --request GET \
> --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg4MDIxNjUsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.CfhFnZ_zG2oVU3awhbeRMv_ttya5Jb7I4hKrUgoLook' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf/operations/?page=1' 
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned list. Maximum 25 items are displayed on each page.



**Return Values**

JSON-object with the list of activities.


**Sample Response**

> ```
> {
>     "operations": [
>         {
>             "author": "12345678d1754bb4afa2c2cb7369d244@auth.local",
>             "app": null,
>             "op_time": 1610981745927,
>             "operation": "{\"op_type\":\"delete_column\",\"table_id\":\"0000\",\"column_key\":\"iJB4\",\"old_column\":{\"rowType\":\"header\",\"key\":\"iJB4\",\"type\":null,\"name\":null,\"editable\":true,\"width\":200,\"resizable\":true,\"draggable\":true,\"data\":null,\"permission_type\":\"\",\"permitted_users\":[],\"editor\":{\"key\":null,\"ref\":null,\"props\":{},\"_owner\":null},\"formatter\":null,\"left\":1058,\"idx\":5},\"upper_column_key\":\"LfGJ\"}",
>             "op_id": 118
>         },
>         {
>             "author": "12345678d1754bb4afa2c2cb7369d244@auth.local",
>             "app": null,
>             "op_time": 1610981742518,
>             "operation": "{\"op_type\":\"delete_column\",\"table_id\":\"0000\",\"column_key\":\"J2mq\",\"old_column\":{\"rowType\":\"header\",\"key\":\"J2mq\",\"type\":null,\"name\":null,\"editable\":true,\"width\":200,\"resizable\":true,\"draggable\":true,\"data\":null,\"permission_type\":\"\",\"permitted_users\":[],\"editor\":{\"key\":null,\"ref\":null,\"props\":{},\"_owner\":null},\"formatter\":null,\"left\":280,\"idx\":2},\"upper_column_key\":\"0000\"}",
>             "op_id": 117
>         },
>         {
>             "author": "12345678d1754bb4afa2c2cb7369d244@auth.local",
>             "app": null,
>             "op_time": 1610981739830,
>             "operation": "{\"op_type\":\"delete_column\",\"table_id\":\"0000\",\"column_key\":\"jQyv\",\"old_column\":{\"rowType\":\"header\",\"key\":\"jQyv\",\"type\":null,\"name\":null,\"editable\":true,\"width\":200,\"resizable\":true,\"draggable\":true,\"data\":null,\"permission_type\":\"\",\"permitted_users\":[],\"editor\":{\"key\":null,\"ref\":null,\"props\":{},\"_owner\":null},\"formatter\":null,\"left\":480,\"idx\":3},\"upper_column_key\":\"J2mq\"}",
>             "op_id": 116
>         }
>     ]
> }
> ```


**Possible Errors**

403 Forbidden: Probably the base's ID or the access token was wrong:
> ```
> {
>     "error_msg": "You don't have permission to get data from the current table."
> }
> ```

## List Row Activities

This API request lists off all the recent activities done to a certain row.


**URL Structure**

> **\[GET]** /api/v1/dtables/`<dtable_uuid>`/activities/


**Request Authentication**

> Base Access Token

**Sample Request**

Display the last 10 activities in the row with the following `row_id` in the base with the following `dtable_uuid`:
> ```
> curl -X GET \
> -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg4MDIxNjUsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.CfhFnZ_zG2oVU3awhbeRMv_ttya5Jb7I4hKrUgoLook' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf/activities/?page=1&row_id=YMIviMeERQCUiQhPPqo6Gw'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**row_id** _\[string, required]_
> The ID of the row.

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned list.

**per_page** _\[int, optional, 10 by default]_
> Number of activities to be displayed per page.


**Return Values**

JSON-object with the list of activities (grouped by activity ID) details, sorted by descending date.


**Sample Response (200)**

Three activities `6782`, `6778`, and `5960` with their details are returned, with the first one being the latest activity:
> ```
> {
>     "activities": [
>         {
>             "id": 6782,
>             "dtable_uuid": "a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf",
>             "row_id": "YMIviMeERQCUiQhPPqo6Gw",
>             "op_user": "0ef256cb715841dd81b147b2530c2904@auth.local",
>             "op_type": "modify_row",
>             "op_time": "2021-01-14T09:01:57.000Z",
>             "detail": {
>                 "table_id": "0000",
>                 "table_name": "Table1",
>                 "row_name": "Meng",
>                 "row_data": [
>                     {
>                         "column_key": "BydO",
>                         "column_name": "Date",
>                         "column_type": "date",
>                         "column_data": {
>                             "format": "YYYY-MM-DD"
>                         },
>                         "value": "2020-08-19",
>                         "old_value": "2020-08-16"
>                     }
>                 ]
>             }
>         },
>         {
>             "id": 6778,
>             "dtable_uuid": "a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf",
>             "row_id": "YMIviMeERQCUiQhPPqo6Gw",
>             "op_user": "0ef256cb715841dd81b147b2530c2904@auth.local",
>             "op_type": "modify_row",
>             "op_time": "2021-01-14T08:56:53.000Z",
>             "detail": {
>                 "table_id": "0000",
>                 "table_name": "Table1",
>                 "row_name": "Meng",
>                 "row_data": [
>                     {
>                         "column_key": "0000",
>                         "column_name": "Name",
>                         "column_type": "text",
>                         "column_data": {},
>                         "value": "Meng",
>                         "old_value": ""
>                     },
>                     {
>                         "column_key": "BydO",
>                         "column_name": "Date",
>                         "column_type": "date",
>                         "column_data": {
>                             "format": "YYYY-MM-DD"
>                         },
>                         "value": "2020-08-16",
>                         "old_value": ""
>                     }
>                 ]
>             }
>         },
>         {
>             "id": 5960,
>             "dtable_uuid": "a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf",
>             "row_id": "YMIviMeERQCUiQhPPqo6Gw",
>             "op_user": "0ef256cb715841dd81b147b2530c2904@auth.local",
>             "op_type": "insert_row",
>             "op_time": "2020-11-18T12:42:14.000Z",
>             "detail": {
>                 "table_id": "0000",
>                 "table_name": "Table1",
>                 "row_name": "",
>                 "row_data": [
>                     {
>                         "column_key": "0000",
>                         "column_name": "Name",
>                         "column_type": "text",
>                         "column_data": {},
>                         "value": ""
>                     }
>                 ]
>             }
>         }
>     ],
>     "total_count": 3
> }
> ```
If a `row_id` is wrong or doesn't exist, SeaTable considers this row as not existing yet, and will return an empty list of activities without error message.
> ```
> {
>     "activities": [],
>     "total_count": 0
> }
> ```

**Possible Errors**

403 Forbidden: Probably is the `dtable_uuid` or the `access_token` wrong:
> ```
> {
>     "error_msg": "You don't have permission to get activities."
> }
> ```



