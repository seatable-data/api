# Notifications

## List All Notifications

List all the current notifications in the base.


**URL Structure**

> **\[GET]** /api/v1/dtables/`<dtable_uuid>`/notifications/


**Request Authentication**

> Base Access Token




**Sample Request**

> ```
> curl \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aae-dbc1-4325-a890-1c2e79ea5319/notifications/'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned list.

**per_page** _\[int, optional, 25 by default]_
> Number of notifications to be displayed per page.


**Return Values**

JSON-object with the list of notifications, including the `id` of each notification, and the value of `seen` indicates the status (`0`-unread, `1`-read).


**Sample Response (200)**

> ```
> {
>     "notification_list": [
>         {
>             "id": 131,
>             "username": "8bh4yf7565694918dy4gf6cb1647fd3f@auth.local",
>             "msg_type": "row_comment",
>             "created_at": "2021-01-15T13:21:28.000Z",
>             "detail": {
>                 "author": "jf36vbf7d1754bb4afa2c2cb7369d244@auth.local",
>                 "table_id": "0000",
>                 "row_id": "fS8qtN6FQ1uPOaNAC0Locw",
>                 "comment": "This looks promising"
>             },
>             "seen": 1
>         },
>         {
>             "id": 130,
>             "username": "8bh4yf7565694918dy4gf6cb1647fd3f@auth.local",
>             "msg_type": "row_comment",
>             "created_at": "2021-01-15T13:21:21.000Z",
>             "detail": {
>                 "author": "jf36vbf7d1754bb4afa2c2cb7369d244@auth.local",
>                 "table_id": "0000",
>                 "row_id": "V_jBEGOXQ3mC3rJkQi-DOQ",
>                 "comment": "I want more details"
>             },
>             "seen": 0
>         },
>         {
>             "id": 142,
>             "username": "8bh4yf7565694918dy4gf6cb1647fd3f@auth.local",
>             "msg_type": "selected_collaborator",
>             "created_at": "2021-01-18T14:56:04.000Z",
>             "detail": {
>                 "author": "7fyr8ey7d1754bb4f7fu4ucb7369d244@auth.local",
>                 "row_id": "Qtf7xPmoRaiFyQPO1aNTjA",
>                 "table_id": "0000"
>             },
>             "seen": 0
>         }
>     ]
> }
> ```
If there's no notification in the current base, an empty list will be returned without error message.

**Possible Errors**

400 Bad Request: The optional parameters have been wrongly given:
> ```
> {
>     "error_msg": "page or per_page invalid."
> }
> ```

403 Forbidden: Access was denied:
> ```
> {
>     "error_msg": "You don't have permission to access the table's notifications."
> }
> ```

## Send A Notification

In a row comment, when you mention someone with an '@' before their username, they'll get a notification that they are mentioned in a comment. Use this API request to send such a mentioning comment.

**URL Structure**

> **\[POST]** /api/v1/dtables/`<dtable_uuid>`/notifications/




**Request Authentication**

> Base Access Token

**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' \
> -H 'Content-type: application/json' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aae-dbc1-4325-a890-1c2e79ea5319/notifications/' \
> -d '{
> 	"to_user": "8bh4yf7565694918dy4gf6cb1647fd3f@auth.local",
> 	"msg_type": "row_comment",
> 	"detail": {
> 		"author": "7fyr8ey7d1754bb4f7fu4ucb7369d244@auth.local", 
> 		"row_id": "NqXZP3YyTyCBOlPf5RNvWQ", 
> 		"comment": "Take a look at this!"}
> }' 
> ```


**Input Parameters**


**dtable_uuid** _\[string, required]_
> The ID of the base.


**to_user** _\[string, required]_
> The ID of the user who should receive this notification.

**msg_type** _\[string, required]_
> Use the value of `row_comment` to define the type of this notification.

**detail** _\[object, required]_
> Define the author, row ID and the content of the comment in this object:

**Author** _\[string, required]_
> The ID of the sender of the comment.
 
**row_id** _\[string, required]_
> The ID of the row.

**comment** _\[string, optional]_
> The content of the comment text.



**Return Value**

JSON-object with the result of the operation.



**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```

**Possible Errors**

400 Bad Request: There has been mistake(s) in the parameters:
> ```
> {
>     "error_msg": "parameters invalid."
> }
> ```

403 Forbidden: Access to the base's notifications was denied:
> ```
> {
>     "error_msg": "You don't have permission to access the table's notifications."
> }
> ```

## Batch Add Notifications

Add multiple notifications at once.


**URL Structure**

> **\[POST]** /api/v1/dtables/`<dtable_uuid>`/notifications-batch/


**Request Authentication**

> Base Access Token

**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' \
> -H 'Content-type: application/json' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aae-dbc1-4325-a890-1c2e79ea5319/notifications-batch/' \
> -d '{
>	"user_messages":[		
>        {
>			"to_user": "7fyr8ey7d1754bb4afa2c2cb7369d244@auth.local",
>	        "msg_type": "row_comment",
>	        "detail": {
>                "author": "8bh4yf756569491ba42905bf1647fd3f@auth.local", 
>                "row_id": "Qtf7xPmoRaiFyQPO1aNTjA", 
>                "comment": "Take a look at this!"}
>		},
>		{
>			"to_user": "7fyr8ey7d1754bb4afa2c2cb7369d244@auth.local",
>	        "msg_type": "row_comment",
>	        "detail": {
>                "author": "8bh4yf756569491ba42905bf1647fd3f@auth.local", 
>                "row_id": "Qtf7xPmoRaiFyQPO1aNTjA",
>                "comment": "And this!"}
>		}
>	]
>}'
> ```

**Request Parameters**


**dtable_uuid** _\[string, required]_
> The ID of the base.

**to_user** _\[string, required]_
> The ID of the user who should receive this notification.

**msg_type** _\[string, required]_
> Use the value of `row_comment` to define the type of this notification.

**user_messages** _\[object, required]_
> Define the author, row ID and the content of the comment in this object:

**Author** _\[string, required]_
> The ID of the sender of the comment.
 
**row_id** _\[string, required]_
> The ID of the row.

**comment** _\[string, optional]_
> The content of the comment text.




**Return Values**

JSON-object with the count of message sent.



**Sample Response (200)**

> ```
> {
>     "message_send_count": 2
> }
> ```

**Possible Errors**

* **400**: Bad Request
* **403**: Forbidden
* **404**: Not Found
* **500**: Internal Server Error




## Mark A Notification Read/Unread

Use this request to mark a specific notification as read or unread.


**URL Structure**

> **\[PUT]** /api/v1/dtables/`<dtable_uuid>`/notifications/`<notification_id>`/


**Request Authentication**

> Base Access Token




**Sample Request**

> ```
> curl -X PUT \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aae-dbc1-4325-a890-1c2e79ea5319/notifications/2/' \
> -d 'seen=true' 
> ```



**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**notification_id** _\[int, required]_
> The ID of the notification. This can be retrived from the call **List All Notifications**.

**seen** _\[enum(`true`, `false`), required]_
> Use `true` to mark the notification as read or `false` as unread. All other values are invalid.


**Return Values**

JSON-object with the result of the operation.



**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```
If a notification is already read/unread and the status wasn't changed, the above response is also returned without error message.


**Possible Errors**

400 Bad Request: The parameter `seen` was not correct (`true` or `false`):
> ```
> {
>     "error_msg": "seen invalid."
> }
> ```

403 Forbidden: Probably is the `dtable_uuid` or the `access_token` wrong:
> ```
> {
>     "error_msg": "You don't have permission to access the table's notifications."
> }
> ```

404 Not Found: Probably the notification's ID is not correct:
> ```
> {
>     "error_msg": "notification 68 not found."
> }
> ```


## Mark All Notifications Read/Unread

Use this request to mark all notifications read or unread.


**URL Structure**

> **\[PUT]** /api/v1/dtables/`<dtable_uuid>/notifications/



**Request Authentication**

> Base Access Token




**Sample Request**

> ```
> curl -X PUT \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aae-dbc1-4325-a890-1c2e79ea5319/notifications/' \
> -d 'seen=true' 
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**seen** _\[enum(`true`, `false`), required]_
> Use `true` to mark the notification as read. All other values than `true` or `false` are invalid.



**Return Values**

JSON-object with the result of the operation.



**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```

**Possible Errors**

400 Bad Request: The parameter `seen` was not correct (`true` or `false`):
> ```
> {
>     "error_msg": "seen invalid."
> }
> ```

403 Forbidden: Probably is the `dtable_uuid` or the `access_token` wrong:
> ```
> {
>     "error_msg": "You don't have permission to access the table's notifications."
> }
> ```





## Delete All Notifications

Use this request to delete all the notifications irrevocably. 


**URL Structure**

> **\[DELETE]** /api/v1/dtables/`<dtable_uuid>`/notifications/


**Request Authentication**

> Base Access Token


**Sample Request**

> ```
> curl -X DELETE \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg3MzczNjMsImR0YWJsZV91dWlkIjoiZDQ4YzNhYWVkYmMxNDMyNWE4OTAxYzJlNzllYTUzMTkiLCJ1c2VybmFtZSI6IjFAMS5jb20iLCJwZXJtaXNzaW9uIjoicncifQ.JAVTMTLiW1exHumjnVQ0Ebkc9xO0JEy5vftlBrHDiyw' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/d48c3aae-dbc1-4325-a890-1c2e79ea5319/notifications/'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.



**Return Values**

JSON-object with the result of the operation.



**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```

**Possible Errors**

403 Forbidden: Probably is the `dtable_uuid` or the `access_token` wrong:
> ```
> {
>     "error_msg": "You don't have permission to access the table's notifications."
> }
> ```

