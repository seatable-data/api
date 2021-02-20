# Statistics

## Statistics of active users

**URL Structure**

> **\[GET]** api/v2.1/admin/statistics/active-users/

**Request Authentication**

> Admin Authentication (Token)

**Sample request**

> ```
> curl 
> -H 'Authorization: Token a407800e307ee8eb545fab94e2d22bb37944661f' 
> -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/admin/statistics/active-users/?start=2020-01-01+00:00:00&end=2020-01-08+00:00:00"
>
> ```

**Input Parameters**

**start** _\[datetime, required]_

> The start time.

**end** _\[datetime, required_]

> The end time.

**Return Values**

JSON-object with the list of active users' details.

**Sample Response (200)**

```
{
    "active_users": [
        {
            "datetime": "2020-01-01T00:00:00+00:00",
            "count": 0
        },
        {
            "datetime": "2020-01-02T00:00:00+00:00",
            "count": 1
        },
        {
            "datetime": "2020-01-03T00:00:00+00:00",
            "count": 3
        },
        {
            "datetime": "2020-01-04T00:00:00+00:00",
            "count": 0
        },
        {
            "datetime": "2020-01-05T00:00:00+00:00",
            "count": 0
        },
        {
            "datetime": "2020-01-06T00:00:00+00:00",
            "count": 2
        },
        {
            "datetime": "2020-01-07T00:00:00+00:00",
            "count": 2
        },
        {
            "datetime": "2020-01-08T00:00:00+00:00",
            "count": 3
        }
    ]
}

```

## Statistics of run scripts

**URL Structure**

> **\[GET]** api/v2.1/admin/statistics/scripts-running/

**Request Authentication**

> Admin Authentication (Token)

**Sample request**

> ```
> curl 
> -H 'Authorization: Token 60ba962845e8380d25948b95c3c439165fafbff1'
> 'https://cloud.seatable.io/api/v2.1/admin/statistics/scripts-running/?is_user=false&month=202012' 
>
> ```

**Input Parameters**

**month** _\[int, optional]_

> The month of the statistics you want to view, for example, 202012

**is_user** _\[boolean, optional_]

> Users or organizations

**page** _\[int, _optional_]_

> Default 1.

**per_page** _\[int, optional_]

> Default 25.

**order_by** _\[str, optional_]

> Which field sort by, total_run_time/total_run_count, if you want sort desc, just add '-' at the start, for example, -total_run_count

**Return Values**

JSON-object with the list of statistics of run scripts' details.

**Sample Response (200)**

```
{
    "results": [
        {
            "org_id": 1,
            "total_run_count": 5,
            "total_run_time": 2.9095635414123535,
            "org_name": "org-1"
        },
        {
            "org_id": 2,
            "total_run_count": 3,
            "total_run_time": 9.999990463256836,
            "org_name": "org-2"
        }
    ],
    "count": 2
}

```


