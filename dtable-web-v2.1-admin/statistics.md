# statistics

## Statistics of Active Users

**GET **api/v2.1/admin/statistics/active-users/

**Request parameters**

* start
* end

**Sample request**

```
curl -H 'Authorization: Token a407800e307ee8eb545fab94e2d22bb37944661f' -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/admin/statistics/active-users/?start=2020-01-01+00:00:00&end=2020-01-08+00:00:00"

```

**Sample response**

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

**Errors**

* 400 Bad Request.
* 403 Permission Denied.
* 500 Internal Server Error.


