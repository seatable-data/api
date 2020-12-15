# Activities

## Get Activities

List the base operations done by the user in the past week.


**URL Structure**

> **\[GET]** /api/v2.1/dtable-activities/



**Request Authentication**

> User Authentication (Token)



**Sample Request**

List three activities done by the user:
> ```
> curl \
> -H 'Authorization: Token a407800e307ee8eb545fab94e2d22bb37944661f' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "http://cloud.seatable.io/api/v2.1/dtable-activities/page=1&per_page=3"
> ```


**Input Parameters**

**avatar_size** _\[int, optional, 72 by default]_ 
> The size of the user's avatar returned.

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned base list.

**per_page** _\[int, optional, 25 by default]_
> Number of bases displayed on each page.



**Return Values**

JSON-object with the list of base activities.



**Sample Response (200)**

The response to the sample request lists off three activities done by the user:

> ```
> {
>     "table_activities": [
>         {
>             "dtable_uuid": "d48c3aaedbc14325a8901c2e79ea5319",
>             "workspace_id": 125,
>             "dtable_name": "SeaTable API Docs",
>             "dtable_icon": "icon-research",
>             "dtable_color": "#1688FC",
>             "op_date": "2020-11-09T09:59:13+00:00",
>             "insert_row": 0,
>             "modify_row": 13,
>             "delete_row": 0
>         },
>         {
>             "dtable_uuid": "d48c3aaedbc14325a8901c2e79ea5319",
>             "workspace_id": 131,
>             "dtable_name": "Release Date management",
>             "dtable_icon": "",
>             "dtable_color": "",
>             "op_date": "2020-11-09T08:16:13+00:00",
>             "insert_row": 0,
>             "modify_row": 1,
>             "delete_row": 0
>         },
>         {
>             "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60",
>             "workspace_id": 130,
>             "dtable_name": "SeaTable API Docs",
>             "dtable_icon": "icon-research",
>             "dtable_color": "#1688FC",
>             "op_date": "2020-11-08T08:50:54+00:00",
>             "insert_row": 0,
>             "modify_row": 13,
>             "delete_row": 0
>         }
>     ]
> }
> ```
If there's no activities in the past week, an empty list will be returned without error message.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```


