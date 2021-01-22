# User common info

## Get User's Common Info

Get the user's common info in a organization.

**URL Structure**

> **\[GET]** /api/v2.1/user-common-info/`<email>`/


**Request Authentication**

> User Authentication (Token)

**Request Params**

* **email**: the user ID ending with @auth.local, required
* **avatar_size**: the size of info's avatar url, optional

**Sample Request**

> ```
> curl --request GET \
> --header 'Authorization: Token 74cb105bbc17f678748a90821045a29e7ae0bf9f' \
> 'https://cloud.seatable.io/api/v2.1/user-common-info/244b43hr6fy54bb4afa2c2cb7369d244@auth.local/?avatar_size=12' 
> ```


**Input Parameters**

**email** _\[string, required]_
> The user's ID ending with `@auth.local`. Not to be confused with the user's `contact_email`.

**avatar_size** _\[int, optional, 80 by default]_
> The size of the avatar.


**Return Values**

JSON-object with the user's common info.


**Sample Response (200)**

> ```
> {
>        "email": "8cb2a6da656876hgf42905bf1647fd3f@auth.local",
>        "name": "Jasmin Tee",
>        "contact_email": "jasmintee@example.com",
>        "avatar_url": "https://cloud.seatable.io/media/avatars/default.png"
> }
> ```

**Possible Errors**:

401 Unauthorized: The token was not accepted:
> ```
> {
>     "detail": "Invalid token"
> }
> ```

404 Not Found: The user was not found (probably was the ID wrong):
> ```
> {
>     "error_msg": "User not found."
> }
> ```


