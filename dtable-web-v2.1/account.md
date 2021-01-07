# Account

## Get Account Info

Get the account details with the user's auth token. This is especially helpful, when a user is looking for their organization's ID (the `org_id`).

**URL Structure**

> **\[GET]** /api2/account/info/

**Request Authentication**

> User Authentication (Token)

**Sample Request**

> ```
> curl \
> -H "Authorization: Token asd410d592f59efc64410bbf4ee7602eb6854dd7" \
> -H 'Accept: application/json; indent=4' \
> https://cloud.seatable.io/api2/account/info/
>
> ```

**Input Parameters**

None.

**Return Values**

JSON-object with account details.

**Sample Response (200)**

> ```
> {
>     "org_id": 4,
>     "is_org_staff": 0,
>     "space_usage": "0.121974751%",
>     "total": 100000000000,
>     "usage": 121974751,
>     "row_usage_rate": "0%",
>     "row_total": -1,
>     "row_usage": 88,
>     "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
>     "email": "7fhe63g949b946a3b200555db5de1d23@auth.local",
>     "name": "Robert Teamplayer",
>     "login_id": "",
>     "contact_email": "teamplayer@example.com",
>     "institution": "",
>     "is_staff": false,
>     "enable_chargebee": true,
>     "enable_subscription": false,
>     "dtable_updates_email_interval": 0,
>     "dtable_collaborate_email_interval": 0
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```






## Update Email Address

Update the user's contact email address. Currently, this feature is disabled on cloud.seatable.io.

**URL Structure**

> **\[PUT]** /api/v2.1/user/contact-email/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

> ```
> curl --request PUT 
> --header 'Authorization: Token 57dbe76c579d7a926539c04c3e8bcbb1e6a65301' \
> 'https://cloud.seatable.io/api/v2.1/user/contact-email/' \
> --form 'new_contact_email=newemail@example.com'
> ```


**Input Parameters**

**new_contact_email** _\[string, required]_
> The new contact email address.


**Return Values**

JSON-object with the feedback of the operation.


**Sample Response**

> ```
> {
>     "msg": "email has been sent, please check it in your current email."
> }
> ```


**Possible Errors**

400 Bad Request: The new contact email was invalid, probably because the parameter `new_contact_email` was not typed in correctly:
> ```
> {
>     "error_msg": "new_contact_email invalid."
> }
> ```

401 Unauthorized: The auth token is invalid:
> ```
> {
>     "detail": "Invalid token"
> }
> ```

403 Forbidden: This feature is disabled by the system admin (e.g. on cloud.seatable.io):
> ```
> {
>     "error_msg": "Feature disabled."
> }
> ```

409 Conflict: The new email address is already used:
> ```
> {
>     "error_msg": "email already exists!"
> }
> ```