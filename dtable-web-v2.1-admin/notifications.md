# Notifications

## Sys-admin list user notifications

**URL Structure**

> **\[GET]** api/v2.1/admin/sys-user-notifications/

**Request Authentication**

> Admin Authentication (Token)

**Sample request **

> ```
> curl 
> -H 'Authorization: Token 42468cbb413c2a628d2ee6249dc8b2935364aaaa'  \
> https://cloud.seatable.io/api/v2.1/admin/sys-user-notifications/?page=1&per_page=3 
>
> ```

**Input Parameters**

**page** _\[int, _optional_]_

> Default 1.

**per_page** _\[int, optional_]

> Default 25.

**Return Values**

JSON-object with the list of notifications' details.

**Sample Response (200)**

```
{
    "notifications": [
        {
            "id": 24,
            "msg": "您好，欢迎参加本周末的线上研讨会，我们将为表格中公式的使用情况进行详细说明， 研讨会链接为: https://bbs.seatable.cn/top/all",
            "username": "7adb8d4b7b464141bf426ae169e8eeea@auth.local",
            "name": "XXXX",
            "contact_email": "248812350@qq.com",
            "seen": false,
            "org_name": "光驰合作发展有限公司",
            "created_at": "2020-12-30T02:54:56+00:00"
        },
        {
            "id": 23,
            "msg": "您好，您的服务将于5日后到期， 如果希望我们的继续服务，请您于cloud.seatable.cn完成续费",
            "username": "7adb8d4b7b464141bf426ae169e8eeea@auth.local",
            "name": "XXXX",
            "contact_email": "248812350@qq.com",
            "seen": true,
            "org_name": "光驰合作发展有限公司",
            "created_at": "2020-12-30T02:53:15+00:00"
        },
        {
            "id": 22,
            "msg": "您好，您的VIP的服务版本将于3日后到期，请您尽快续费， 续费链接为: clound.seafile.cn",
            "username": "admin@seafiletest.com",
            "name": "admin",
            "contact_email": "",
            "seen": false,
            "org_name": "",
            "created_at": "2020-12-30T02:49:40+00:00"
        }
    ],
   "total_count":100
}

```

## Sys-admin add a system notification to user

**URL Structure**

> **\[POST]** api/v2.1/admin/sys-user-notifications/

**Request Authentication**

> Admin Authentication (Token)

**Sample request **

```
curl 
-X POST https://cloud.seatable.io/api/v2.1/admin/sys-user-notifications/ 
-H 'Authorization: Token 42468cbb413c2a628d2ee6249dc8b2935364aaaa' 
-H 'Content-Type: application/json' 
-d '{"msg":"Hello world!","username":"7d1bf25bba6243418f376464c80045d1@auth.local"}'

```

**Input Parameters**

**msg** _\[str, required]_

> message detail which to be ready to add.

**username** _\[str, required_]

> Assigned user.

**Return Values**

JSON-object of the notification' details.

**Sample Response (200)**

```
{
    "notification": {
        "id": 12,
        "msg": "The current note to you all!",
        "username": "7d1bf25bba6243418f376464c80045d1@auth.local",
        "name": "uu",
        "seen": false,
        "created_at": "2020-12-23T06:04:23+00:00"
    }
}

```

## Sys-admin delete a user notification

**URL Structure**

> **\[DELETE]** api/v2.1/admin/sys-user-notifications/`<notification_id>`/

**Request Authentication**

> Admin Authentication (Token)

**Sample request **

> ```
> curl 
> -X DELETE https://cloud.seatable.io/api/v2.1/admin/sys-user-notifications/15/ 
> -H 'Authorization: Token 42468cbb413c2a628d2ee6249dc8b2935364aaaa' 
>
> ```

**Input Parameters**

**notification_id** _\[int, required]_

> The ID of the notification.

**Sample Response (200)**

```
{
    "success": true
}

```

## Mark a user-specific notification as seen

**URL Structure**

> **\[PUT]** api/v2.1/sys-user-notifications/\<notification_id>/seen/

**Request Authentication**

> Admin Authentication (Token)

**Sample request **

```
curl 
-X PUT https://cloud.seatable.io/api/v2.1/sys-user-notifications/11/seen/ 
-H 'Authorization: Token 42468cbb413c2a628d2ee6249dc8b2935364aaaa' 

```

**Input Parameters**

**notification_id** _\[int, required]_

> The ID of the notification.

**Return Values**

JSON-object of the notification' details.

**Sample Response (200)**

```
{
    "notification": {
        "id": 17,
        "msg": "Test customer seen notice",
        "username": "87d485c2281a42adbddb137a1070f395@auth.local",
        "name": "冉继伟",
        "seen": true,
        "created_at": "2020-12-25T03:31:03+00:00"
    }
}

```

## List the user's unseen notifications

**URL Structure**

> **\[GET]** api/v2.1/sys-user-notifications/unseen/

**Request Authentication**

> Admin Authentication (Token)

**Sample request **

```
curl 
-X GET https://cloud.seatable.io/api/v2.1/sys-user-notifications/unseen/ 
-H 'Authorization: Token 5c5446465b445ae5bd16b3464e8fff69127d4496' 

```

**Return Values**

JSON-object with the list of unseen notifications' details.

**Sample Response (200)**

```
{
    "notifications": [
        {
            "id": 41,
            "msg": "xxx",
            "username": "0febcccbb7d744b581911d3fa628e631@auth.local",
            "name": "tom",
            "contact_email": "r350178982@126.com",
            "seen": false,
            "org_name": "宇枫国际有限公司",
            "created_at": "2021-01-19T09:12:42+00:00",
            "msg_format": "xxx"
        },
        {
            "id": 40,
            "msg": "xxx",
            "username": "0febcccbb7d744b581911d3fa628e631@auth.local",
            "name": "jack",
            "contact_email": "r350178982@126.com",
            "seen": false,
            "org_name": "宇枫国际有限公司",
            "created_at": "2021-01-19T09:12:33+00:00",
            "msg_format": "xxx"
        },

```

### 


