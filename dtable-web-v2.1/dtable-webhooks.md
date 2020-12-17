# Webhooks

## List A Base's Webhooks

With webhooks, the changes doen to a base can be posted to the desired URL. This request lists all the webhooks created in a base.


**URL Structure**

> **\[GET]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/webhooks/



**Sample Request**

List all the webhooks created in the base `Tweets` in the workspace `1`:

> ```
> curl --request GET \
> --header 'Authorization: Token 3120688f207383ba90e6160190ff70036d2e185d' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Tweets/webhooks/' 
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.


**Return Values**

JSON-object with the details of the webhooks, including the ID of the webhooks.




**Sample Response (200)**

The response lists off the two webhooks with IDs of `2` and `12` in the base:

> ```
> {
>     "webhook_list": [
>         {
>             "id": 2,
>             "dtable_uuid": "626e40fa76304a4fb7641b71efab4795",
>             "url": "http://cloud.example.com",
>             "creator": "5758ecdce3e741ad81293a304b6d3388@auth.local",
>             "created_at": "2020-09-23T06:28:06.412738",
>             "settings": {
>                 "secret": "example"
>             }
>         },
>         {
>             "id": 12,
>             "dtable_uuid": "626e40fa76304a4fb7641b71efab4795",
>             "url": "http://cloud.seatable.io",
>             "creator": "5758ecdce3e741ad81293a304b6d3388@auth.local",
>             "created_at": "2020-09-24T09:54:09.264397"
>         }
>     ]
> }
> ```


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the requested base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Twitts not found."
> }
> ```



## Create A Webhook for A Base

Create a new webhook for a base with desired URL and secret (optional).


**URL Structure**

> **\[POST]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/webhooks/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

Create a webhook in the base `Tweets` from workspace `1`, with the post URL of `http://www.example.com` and a `secret` of `123456`:

> ```
> curl --request POST \
> --header 'Authorization: Token 3120688f207383ba90e6160190ff70036d2e185d' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Tweets/webhooks/' \
> --form 'url=http://www.example.com' \
> --form 'secret=123456'
> ```


**Input Parameters**

**url** _\[URL, required]
> The new webhook's URL.

**secret** _\[string, optional]_
> When you set a secret, you'll receive the X-SeaTable-Signature header in the webhook POST request. Its value is the result of hashing the secret key with SHA1 algorithm.



**Return Values**

JSON-object with the details of the created webhook. The webhook's ID is automatically generated.


**Sample Response (200)**

The webhook with the ID of `15` has now been created:

> ```
> {
>     "webhook": {
>         "id": 15,
>         "dtable_uuid": "626e40fa76304a4fb7641b71efab4795",
>         "url": "http://www.example.com",
>         "creator": "5758ecdce3e741ad81293a304b6d3388@auth.local",
>         "created_at": "2020-09-24T10:10:59.473003",
>         "settings": {
>             "secret": "123456"
>         }
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

403 Forbidden: The user doesn't have access to the requested base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Twitts not found."
> }
> ```

409 Conflict: A webhook with the same URL already exists:
> ```
> {
>     "error_msg": "Webhook exists."
> }
> ```


## Update A Webhook

With this request, update the URL and/or the secret of a webhook.


**URL Structure**

> **\[PUT]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/webhooks/`<webhook_id>`/


**Request Authentication**

> User Authentication (Token)



**Sample Request**

Change the webhook `15`'s URL and secret as follows:

> ```
> curl --request PUT \
> --header 'Authorization: Token 3120688f207383ba90e6160190ff70036d2e185d' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Tweets/webhooks/15/' \
> --form 'url=https://cloud.example.com' \
> --form 'secret=654321'
> ```


**Input Parameters**

**url** _\[URL, required]
> The webhook's new URL.

**secret** _\[string, optional]_
> The new secret. When you set a secret, you'll receive the X-SeaTable-Signature header in the webhook POST request. Its value is the result of hashing the secret key with SHA1 algorithm.



**Return Values**

JSON-object with the details of the updated webhook.



**Sample Response (200)**

The updated details of the webhook are returned:

> ```
> {
>     "webhook": {
>         "id": 15,
>         "dtable_uuid": "626e40fa76304a4fb7641b71efab4795",
>         "url": "https://cloud.example.com",
>         "creator": "5758ecdce3e741ad81293a304b6d3388@auth.local",
>         "created_at": "2020-09-24T10:10:59.473003",
>         "settings": {
>             "secret": "654321"
>         }
>     }
> }
> ```
If you repeat this operation, you'll always get the same response without error message.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the requested base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Twitts not found."
> }
> ```

404 Not Found: The webhook was not found with the given ID:
> ```
> {
>     "error_msg": "Webhook not found."
> }
> ```

## Delete A Webhook

Use this request to remove a webhook.


**URL Structure**

> **\[DELETE]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/webhooks/`<webhook_id>`/


**Request Authentication**

> User Authentication (Token)

**Sample Request**

Remove the webhook with the ID of `15` from the base `Tweets` in the workspace `1`:

>```
>curl --request DELETE \
>--header 'Authorization: Token 3120688f207383ba90e6160190ff70036d2e185d' \
>'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Tweets/webhooks/15/' 
>```

**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.

**webhook_id** _\[int, required]_
> The ID of the webhook. It is automatically generated and returned when creating a new webhook.


**Return Values**

JSON-object with the result of the operation.


**Sample Response (200)**

> ```
> 200 OK
> ```


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the requested base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Twitts not found."
> }
> ```

404 Not Found: The webhook was not found with the given ID:
> ```
> {
>     "error_msg": "Webhook not found."
> }
> ```
