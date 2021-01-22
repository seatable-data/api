# Collaborators

## List Collaborators of A Base

Use this request to list all the users collaborating on a certain base.


**URL Structure**

> **\[GET]** /api/v1/dtables/`<dtable_uuid>`/related-users/


**Request Authentication**

> Base Access Token

**Sample Request**

> ```
> curl -X GET \
> -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg1NjUzMzUsImR0YWJsZV91dWlkIjoiZmY5NzdkYzhmMDY1NDY3MjlkNDg5ZGVmZDY0Y2ZlOGYiLCJ1c2VybmFtZSI6ImFkbWluQHNlYWZpbGV0ZXN0LmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.7j3nTzViP9LxINGIxf9YR8KyWs633DHRW7SyfXvOF7Y' \
> https://cloud.seatable.io/dtable-server/api/v1/dtables/7f7dc9c7-187a-4d9f-b6cf-ff5e5019a6d5/related-users/ 
> ```


**Input Parameters**

**dtable_uuid** _\[string, required]_
> The ID of the base.


**Return Values**

JSON-object with the list of collaborative users.


**Sample Response (200)**

> ```
> {
>     "user_list": [
>         {
>             "email": "244b43hr6fy54bb4afa2c2cb7369d244@auth.local",
>             "name": "Ginger Ale",
>             "contact_email": "gingerale@example.com",
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png"
>         },
>         {
>             "email": "8cb2a6da656876hgf42905bf1647fd3f@auth.local",
>             "name": "Jasmin Tee",
>             "contact_email": "jasmintee@example.com",
>             "avatar_url": "https://cloud.seatable.io/media/avatars/default.png"
>         }
>     ]
> }
> ```

**Possible Errors**:

403 Forbidden: Access to the base was denied (probably wrong `dtable_uuid` or access token):
> ```
> {
>     "error_msg": "You don't have permission to get users."
> }
> ```


