# Daily Active Users

## List Daily Active Users

**GET **api/v2.1/admin/daily-active-users/

**Request parameters**

* date
* avatar_size (default 72)
* page (default, 1)
* per_page (default, 25)

**Sample request**

```
curl -H 'Authorization:Token a407800e307ee8eb545fab94e2d22bb37944661f' -H 'Accept: application/json; indent=4' "https://cloud.seatable.io/api/v2.1/admin/daily-active-users/?date=2020-06-19+00:00:00"

```

**Sample response**

```
{
    "active_user_list": [
        {
            "avatar_url": "https://cloud.seatable.io/media/avatars/d/2/19af79b45e5891507fda4c4c2139a0/resized/72/03e77af8819c66f25260297dd5e97dc7.png",
            "email": "1@1.com",
            "contact_email": "1@1.com",
            "name": "Alex",
            "reg_date": "2019-08-08T12:16:11.359002"
        },
        {
            "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
            "email": "3@3.com",
            "contact_email": "3@3.com",
            "name": "Cata",
            "reg_date": "2020-03-11T13:35:55.632356",
            "org_id": 13,
            "org_name": "League"
        }
    ],
    "page": 1,
    "total_count": 2
}

```

**Errors**

* 400 Bad Request.
* 403 Permission Denied.
* 500 Internal Server Error.


