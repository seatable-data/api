# System Notifications

System notifications are highlighted messages displayed on the top of the base library. System administrators can use this feature to inform users about their subscription status, or pass through any necessary message. 

To mark a system notification as seen, users can click on the "x" to close them, or use the API request in this article.

## Mark A User-Specific System Notification as Seen

When a system notification is marked as seen, it'll disappear from the user's base library.

**URL Structure**

> **\[PUT]** /api/v2.1/sys-user-notifications/`<notification_id>`/seen/

**Request Authentication**

> User Authentication (Token)

**Sample Request**

> ```
> curl -X PUT \
> -H 'Authorization: Token 42468cbb413c2a628d2ee6249dc8b2935364aaaa' \
> https://cloud.seatable.io/api/v2.1/sys-user-notifications/11/seen/ 
> ```

**Input Parameters**

**notification_id** _\[int, required]_
> The ID of the notification.

**Return Values**

JSON-object of the updated notification' details.

**Sample Response (200)**

> ```
> {
>     "notification": {
>         "id": 17,
>         "msg": "Test customer seen notice",
>         "username": "87d485c2281a42adbddb137a1070f395@auth.local",
>         "name": "Robert Teamleader",
>         "seen": true,
>         "created_at": "2020-12-25T03:31:03+00:00"
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

403 Forbidden: The current user doesn't have access to this system notification:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```

404 Not Found: The notification was not found:
> ```
> {
>     "error_msg": "notification 5 not found."
> }
> ```

## List All Unseen System Notifications

Use this request to list a user's unseen system notifications.

**URL Structure**

> **\[GET]** /api/v2.1/sys-user-notifications/unseen/

**Request Authentication**

> User Authentication (Token)

**Sample Request**

> ```
> curl -X GET \
> -H 'Authorization: Token 5c5446465b445ae5bd16b3464e8fff69127d4496' \
> https://cloud.seatable.io/api/v2.1/sys-user-notifications/unseen/ 
> ```

**Input Parameters**

None.

**Return Values**

JSON-object with the list of unseen notifications' details.

**Sample Response (200)**

> ```
> {
>     "notifications": [
>         {
>             "id": 41,
>             "msg": "Sample message",
>             "username": "0febcccbb7d744b581911d3fa628e631@auth.local",
>             "name": "Tom",
>             "contact_email": "tom@example.com",
>             "seen": false,
>             "org_name": "Team Yufeng",
>             "created_at": "2021-01-19T09:12:42+00:00",
>             "msg_format": ""
>         },
>         {
>             "id": 40,
>             "msg": "Sample message",
>             "username": "0febcccbb7d744b581911d3fa628e631@auth.local",
>             "name": "Jack",
>             "contact_email": "jack@example.com",
>             "seen": false,
>             "org_name": "Team Yufeng",
>             "created_at": "2021-01-19T09:12:33+00:00",
>             "msg_format": ""
>         }
> ```


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

