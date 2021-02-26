# System Notifications

System notifications are highlighted messages displayed on the top of the base library. System administrators can use this feature to inform users about their subscription status, or pass through any necessary message. When the user has clicked on the 'x' to close that message, this notification will be marked as 'seen'.

## List User's System Notifications

List all the system notifications sent to users.

**URL Structure**

> **\[GET]** /api/v2.1/admin/sys-user-notifications/

**Request Authentication**

> Admin Authentication (Token)

**Sample request **

> ```
> curl 
> -H 'Authorization: Token 42468cbb413c2a628d2ee6249dc8b2935364aaaa'  \
> "https://cloud.seatable.io/api/v2.1/admin/sys-user-notifications/?page=1&per_page=3"
>
> ```

**Input Parameters**

**page** _\[int, optional, 1 by default]_
> The page number of the returned list.

**per_page** _\[int, optional, 25 by default]_
> Items to display on each page.

**Return Values**

JSON-object with the list of notifications' details. The returned `id` is the ID of the notification, and the `username` is the ID of the user.

**Sample Response (200)**

> ```
> {
>     "notifications": [
>         {
>             "id": 24,
>             "msg": "Hello, your subscription is expiring in 2 weeks!",
>             "username": "7adb8d4b7b464141bf426ae169e8eeea@auth.local",
>             "name": "John Doe",
>             "contact_email": "johndoe@example.com",
>             "seen": false,
>             "org_name": "Team John Doe",
>             "created_at": "2020-12-30T02:54:56+00:00"
>         },
>         {
>             "id": 23,
>             "msg": "Hello, your subscription is expiring in 4 weeks!",
>             "username": "7adb8d4b7b464141bf426ae169e8eeea@auth.local",
>             "name": "John Doe",
>             "contact_email": "johndoe@example.com",
>             "seen": true,
>             "org_name": "Team John Doe",
>             "created_at": "2020-12-30T02:53:15+00:00"
>         },
>         {
>             "id": 22,
>             "msg": "Hello, this is a test notification.",
>             "username": "123abc456def789ghi123jkl456mno789@auth.local",
>             "name": "admin",
>             "contact_email": "admin@example.com",
>             "seen": false,
>             "org_name": "",
>             "created_at": "2020-12-30T02:49:40+00:00"
>         }
>     ],
>    "total_count":100
> }
> ```
If there's no system notifications, an empty list is returned without error message.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The current user doesn't have admin clearance:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```

## Add A System Notification to A User

Add a system notification to a specific user with their ID.

**URL Structure**

> **\[POST]** /api/v2.1/admin/sys-user-notifications/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token 42468cbb413c2a628d2ee6249dc8b2935364aaaa' \
> -H 'Content-Type: application/json' \
> https://cloud.seatable.io/api/v2.1/admin/sys-user-notifications/ \
> -d '{"msg":"Hello user!","username":"7d1bf25bba6243418f376464c80045d1@auth.local"}'
> ```

**Input Parameters**

**msg** _\[str, required]_
> The content of the message in text format.

**username** _\[str, required]_
> The user's ID.

**Return Values**

JSON-object of the notification's details.

**Sample Response (200)**

> ```
> {
>     "notification": {
>         "id": 12,
>         "msg": "The current note to you all!",
>         "username": "7d1bf25bba6243418f376464c80045d1@auth.local",
>         "name": "uu",
>         "seen": false,
>         "created_at": "2020-12-23T06:04:23+00:00"
>     }
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The current user doesn't have admin clearance:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```

404 Not Found: The user's ID was not accepted (probably not the ID but the contact email address was given):
> ```
> {
>     "error_msg": "User admin@example.com not found."
> }
> ```

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


