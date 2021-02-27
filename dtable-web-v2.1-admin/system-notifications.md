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

## Delete A System Notification to A User

Delete a system notification with its ID.

**URL Structure**

> **\[DELETE]** /api/v2.1/admin/sys-user-notifications/`<notification_id>`/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl -X DELETE \
> -H 'Authorization: Token 42468cbb413c2a628d2ee6249dc8b2935364aaaa' \
> 'https://cloud.seatable.io/api/v2.1/admin/sys-user-notifications/15/'
> ```

**Input Parameters**

**notification_id** _\[int, required]_
> The ID of the system notification.

**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

> ```
> {
>     "success": true
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

404 Not Found: The notification with the given ID was not found, probably already deleted:
> ```
> {
>     "error_msg": "notification 15 not found."
> }
> ```




