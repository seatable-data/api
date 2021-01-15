# Comments

## Get Row Comments Count

Get the number of comments in a certain row.


**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/comments-count/


**Request Authentication**

> Base Access Token


**Sample Request**

> ```
> curl -X GET \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/comments-count/?row_id=NAu2B3OcRG6UrWagL-9naA' 
> ```


**Input Parameter**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**row_id** _\[string, required]_
> The ID of the row to be queried.



**Return Value**

JSON-object with the number of comments.


**Sample Response (200)**

> ```
> {
>     "count": 2
> }
> ```

**Possible Errors**

403 Forbidden: You cannot access the current base or table (probably because of wrong `dtable_uuid` or access token):
> ```
> {
>     "error_msg": "You don't have permission to access the table's comments."
> }
> ```





## List Row Comments

List all the comments in a certain row.


**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/comments/


**Request Authentication**

> Base Access Token



**Sample Request**

> ```
> curl -X GET \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/comments/?row_id=NAu2B3OcRG6UrWagL-9naA' 
> ```



**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**row_id** _\[string, required]_
> The ID of the row.

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned list.

**per_page** _\[int, optional, 10 by default]_
> Number of comments to be displayed per page.




**Return Values**

JSON-object with the list of comments. The returned `id` value is the ID of each comment.




**Sample Response (200)**

> ```
> [
>     {
>         "id": 140,
>         "author": "28dhr6e7d1754bb4afa2c2cb7369d244@auth.local",
>         "comment": "This is good!",
>         "dtable_uuid": "650d8a0d-7e27-46a8-8b18-6cc6374yf557",
>         "row_id": "NAu2B3OcRG6UrWagL-9naA",
>         "created_at": "2021-01-15T13:35:26.000Z",
>         "updated_at": "2021-01-15T13:35:26.000Z",
>         "resolved": 0
>     },
>     {
>         "id": 141,
>         "author": "28dhr6e7d1754bb4afa2c2cb7369d244@auth.local",
>         "comment": "Go online tomorrow?",
>         "dtable_uuid": "650d8a0d-7e27-46a8-8b18-6cc6374yf557",
>         "row_id": "NAu2B3OcRG6UrWagL-9naA",
>         "created_at": "2021-01-15T13:52:48.000Z",
>         "updated_at": "2021-01-15T13:52:48.000Z",
>         "resolved": 0
>     },
>     {
>         "id": 142,
>         "author": "8cb2a6da1928374ba42905bf1647fd3f@auth.local",
>         "comment": "Agreed!",
>         "dtable_uuid": "650d8a0d-7e27-46a8-8b18-6cc6374yf557",
>         "row_id": "NAu2B3OcRG6UrWagL-9naA",
>         "created_at": "2021-01-15T13:53:13.000Z",
>         "updated_at": "2021-01-15T13:53:13.000Z",
>         "resolved": 0
>     }
> ]
> ```
If the `row_id` is wrong, SeaTable returns an empty list (200) instead of an error message.

**Possible Errors**

400 Bad Request: The `row_id` parameter is missing:
> ```
> {
>     "error_msg": "row_id invalid"
> }
> ```

403 Forbidden: You do not have the permission to the base or table (probably because of wrong `dtable_uuid` or access token):
> ```
> {
>     "error_msg": "You don't have permission to read comments."
> }
> ```


## Create A Row Comment

Use this request to create a comment to a certain row.


**URL Structure**

> **\[POST]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/comments/



**Request Authentication**

> Base Access Token





**Sample Request**

Post a comment to the following base>table>row:
> ```
> curl -X POST \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' \
> -H 'content-type: application/json' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/comments/?table_id=0000&row_id=NAu2B3OcRG6UrWagL-9naA' 
> -d '{
> 	"comment": "Finally, this project is finished!"
> }'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**table_id** _\[string, required]_
> The ID of the table.

**row_id** _\[string, required]_
> The ID of the row.

**comment** _\[string, required]_
> The content of the comment, given in a JSON-object (see **Sample Request**).



**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```

**Possible Errors**

400 Bad Request: One or more of the required parameters are missing:
> ```
> {
>     "error_msg": "table_id or row_id invalid"
> }
> ```

403 Forbidden: Your access token is read-only, or the table or row doesn't exist:
> ```
> {
>     "error_msg": "You don't have permission to comment the row"
> }
> ```

## Update A Comment

Use this request to change the content of a comment, or mark it as resolved.


**URL Structure**

> **\[PUT]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/comments/`<comment_id>`/


**Request Authentication**

> Base Access Token





**Sample Request**

> ```
> curl -X PUT \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' \
> H 'content-type: application/json' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/comments/9/' \
> -d '{
> 	"options": {
> 		"comment": "Great!",
> 		"resolved": 1
> 	}
> }'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**comment_id** _\[int, required]_
> The ID of the comment when it's created. Can be retrieved from the call **List Row Comments**.

**comment** _\[string, optional]_
> The new content of the comment if you want to change it, given in a JSON-object (see **Sample Request**).

**resolved** _\[enum(0, 1), optional]_
> Set the value to 1 to mark the comment as resolved. However, setting it to 0 cannot mark a comment that's already marked as resolved to unresolved. Same as **comment**, this parameter is given in a JSON-object (see **Sample Request**).



**Return Values**

JSON-object with the result of the operation.


**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```
A resolved comment cannot be marked as unresolved, however. In this case, the above success response will be returned without error message.

**Possible Errors**

400 Bad Request: The `options` parameter is not correctly parsed or is missing:
> ```
> {
>     "error_msg": "options invalid"
> }
> ```

403 Forbidden: Your permission was denied (the access token or the base's ID was not correct):
> ```
> {
>     "error_msg": "You don't have permission to update the comment"
> }
> ```




## Delete A Comment

Use this request to delete an existing comment. You can only delete your own comments.


**URL Structure**

> **\[DELETE]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/comments/`<comment_id>`/



**Request Authentication**

> Base Access Token



**Sample Request**

> ```
> curl -X DELETE \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs' 
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/comments/7/'
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.

**comment_id** _\[int, required]_
> The ID of the comment when it's created. Can be retrieved from the call **List Row Comments**.



**Return Values**

JSON-object with the result of the operation.




**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```

**Possible Errors**

403 Forbidden: Probably is the access token or `dtable_uuid` wrong, or it's not your comment:
> ```
> {
>     "error_msg": "You don't have permission to delete comment"
> }
> ```

404 Not Found: The comment doesn't exist:
> ```
> {
>     "error_msg": "comment 188 not found"
> }
> ```

## Get Comment by ID

Get the details of a certain comment by its ID.


**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/comments/`<comment_id>`/


**Request Authentication**

> Base Access Token



**Sample Request**


> ```
> curl -X GET \
> -H 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NzYyMTg4MzAsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.DDp5q4hg98cvHUqBhJdFxbENm7ukrwDvlnNdY0OFCXs'  \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/comments/8/' 
> ```



**Input Parameters**


**dtable_uuid** _\[string, required]_
> The ID of the base.

**comment_id** _\[int, required]_
> The ID of the comment when it's created. Can be retrieved from the call **List Row Comments**.




**Return Values**

JSON-object with the details of the comment.



**Sample Response (200)**

> ```
> {
>     "id": 141,
>     "author": "244b4667d1757ey46fg3c2cb7369d244@auth.local",
>     "comment": "Here is my email address",
>     "dtable_uuid": "650d8a0d-7e27-46a8-8b18-6cc6374yf557",
>     "row_id": "NAu2B3OcRG6UrWagL-9naA",
>     "created_at": "2021-01-15T13:52:48.000Z",
>     "updated_at": "2021-01-15T13:52:48.000Z",
>     "resolved": 0
> }
> ```

**Possible Errors**

403 Forbidden: The comment is not in your base:
> ```
> {
>     "error_msg": "You don't have permission to get the comment"
> }
> ```

403 Forbidden: Permission to the base is denied:
> ```
> {
>     "error_msg": "You don't have permission to read comment"
> }
> ```



## List Comments within Days

List all the comments in the base within a given number of days.


**URL Structure**

> **\[GET]** /dtable-server/api/v1/dtables/`<dtable_uuid>`/comments-within-days/



**Request Authentication**

> Base Access Token




**Sample Request**

> ```
> curl --request GET \
> --header 'Authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1ODczNDk0NzQsImR0YWJsZV91dWlkIjoiMDAzOTA0MTViNmRjNDE2YThmMmE3MGEzYTEzNTZhMTgiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.BG55vZP0WMkM8cx_12aI-dNQiNp0l8kHlTqmErclX8Y' \
> 'https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/comments-within-days/?days=3' 
> ```


**Input Parameters**


**dtable_uuid** _\[string, required]_
> The ID of the base.

**days** _\[int, required, 3 by default]_
> Number of days from today.



**Return Values**

JSON-object with the list of comments.



**Sample Response (200)**

> ```
> {
>     "comments": [
>         {
>             "id": 44,
>             "author": "244b4667d1757ey46fg3c2cb7369d244@auth.local",
>             "comment": "4",
>             "dtable_uuid": "7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5",
>             "row_id": "U_eTV7mDSmSd-K2P535Wzw",
>             "created_at": "2020-04-17T02:23:17.000Z",
>             "updated_at": "2020-04-17T02:23:17.000Z",
>             "resolved": 0
>         },
>         {
>             "id": 43,
>             "author": "244b4667d1757ey46fg3c2cb7369d244@auth.local",
>             "comment": "3",
>             "dtable_uuid": "7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5",
>             "row_id": "U_eTV7mDSmSd-K2P535Wzw",
>             "created_at": "2020-04-17T02:23:16.000Z",
>             "updated_at": "2020-04-17T02:23:16.000Z",
>             "resolved": 0
>         }
>     ]
> }
> ```

**Possible Errors**

400 Bad Request: The parameter `days` was not correctly given:
> ```
> {
>     "error_msg": "days is invalid."
> }
> ```

403 Forbidden: Permission to the base is denied:
> ```
> {
>     "error_msg": "You don't have permission to read comments."
> }
> ```


