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
> Type in the format like 2020-06-19+00:00:00

**avatar_size** _\[numeric, optional, 72 by default]_ 
> The size of the user's avatar returned.

**page** _\[numeric, optional, 1 by default]_ 
> Page number of the returned user list.

**per_page** _\[numeric, optional, 25 by default]_
> Number of users displayed on each page.


**Sample response (200)**

Response from the sample request shows 2 active users and their avatar URL, ID (<email>), contact email address, name and registration time:

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