# Daily Active Users

## List Daily Active Users


List the daily active users on a given day.

**URL Structure**

> **\[GET]** /api/v2.1/admin/daily-active-users/

**Request Authentication**

> Admin Authentication (Token)



**Sample Request**

Request the daily active users list on 19 June, 2020:

>```
> curl \
> -H 'Authorization:Token a407800e307ee8eb545fab94e2d22bb37944661f' \
> -H 'Accept: application/json; indent=4' \
> "https://cloud.seatable.io/api/v2.1/admin/daily-active-users/?date=2020-06-19+00:00:00"
>```


**Input Parameters**

**date** _\[date, required]_
> This is the date on which you want the number of active user to be shown. \
> Type in the ISO format like 2020-06-19+00:00:00

**avatar_size** _\[numeric, optional, 72 by default]_ 
> The size of the user's avatar returned.

**page** _\[numeric, optional, 1 by default]_ 
> Page number of the returned user list.

**per_page** _\[numeric, optional, 25 by default]_
> Number of users displayed on each page.


**Return Values**

JSON-object with the active user list.


**Sample response (200)**

Response from the sample request shows 2 active users and their avatar URL, ID (`<email>`), contact email address, name and registration time:

> ```
> {
>    "active_user_list": [
>        {
>            "avatar_url":"https://cloud.seatable.io/media/avatars/d/2/19af79b45e5891507fda4c4c2139a0/resized/72/03e77af8819c66f25260297dd5e97dc7.png",
>            "email":"0ef256cb715841dd81b147b2530c2904@auth.local",
>            "contact_email":"alexander@example.com",
>            "name":"Alex",
>            "reg_date":"2019-08-08T12:16:11.359002"
>        },
>        {
>            "avatar_url":"https://cloud.seatable.io/media/avatars/default.png",
>            "email":"0ef256cb71584188b1b147b2530c2904@auth.local",
>            "contact_email":"cata@example.com",
>            "name":"Cata",
>            "reg_date":"2020-03-11T13:35:55.632356",
>            "org_id":13,
>            "org_name":"League"
>        }
>    ],
>    "page": 1,
>    "total_count": 2
>}
>```





**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```


## Statistics of Active Users

List daily active users in a given period of time.

**URL Structure**

> **\[GET]** /api/v2.1/admin/statistics/active-users/



**Sample Request**

Request the daily active users between the 1st and the 3rd of November, 2020:

>```
>curl 
>-H 'Authorization: Token a407800e307ee8eb545fab94e2d22bb37944661f' \
>-H 'Accept: application/json; charset=utf-8; indent=4' \
>"https://cloud.seatable.io/api/v2.1/admin/statistics/active-users/?start=2020-11-01+00:00:00&end=2020-11-03+00:00:00"
>```


**Input Parameters**

**start** _\[date, required]_
> The first day in your request. Type in the ISO format like 2020-11-01+00:00:00.

**end** _\[date, required]_
> The last day in your request. Type in the ISO format like 2020-11-03+00:00:00.


**Return Values**

JSON-object with daily statistics of active users.


**Sample Response (200)**

The response from the sample request lists off the number of daily active users from the starting date to the ending date:

>```
>{
>    "active_users": [
>        {
>            "datetime": "2020-11-01T00:00:00+00:00",
>            "count": 1234
>        },
>        {
>            "datetime": "2020-11-02T00:00:00+00:00",
>            "count": 2345
>        },
>        {
>            "datetime": "2020-11-03T00:00:00+00:00",
>            "count": 3456
>        }
>    ]
>}
>```
If start time was given later than end time, an empty list will be returned without error message.

**Possible Errors**

400 Bad Request: Time format is wrong:
>```
>{
>    "error_msg": "End time 2020-11-08 00:00:99 invalid"
>}
>```

400 Bad Request: Start time missing (same for end time):
>```
>{
>    "error_msg": "Start time can not be empty"
>}
>```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```
