# Account

## Get Account Info

Get the account details with the user's auth token.

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

**Sample Response**

> ```
> {
>     "is_org_staff": 0,
>     "space_usage": "0.295870636%",
>     "total": 100000000000,
>     "usage": 295870636,
>     "row_usage_rate": "0%",
>     "row_total": -1,
>     "row_usage": 55,
>     "avatar_url": "https://cloud.seatable.io/media/avatars/default.png",
>     "email": "6534ce64315b4b4abfcff9e5491db296@auth.local",
>     "name": "Karlheinz Mitarbeiter",
>     "login_id": "",
>     "contact_email": "karlheinz@example.com",
>     "institution": "",
>     "is_staff": false,
>     "enable_chargebee": true,
>     "enable_subscription": false,
>     "email_notification_interval": 0
> }
>
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

## Update email address

**PUT** /api/v2.1/user/contact-email/

**URL Structure**

> **\[PUT]** /api/v2.1/user/contact-email/

**Request Authentication**

> User Authentication (Token)

**Sample Request**

> ```
> curl --request PUT 'https://cloud.seatable.io/api/v2.1/user/contact-email/' \
> --header 'Authorization: Token 57dbe76c579d7a926539c04c3e8bcbb1e6a65301' \
> --form 'new_contact_email=1223408988@qq.com'
>
> ```

**Input Parameters**

**new_contact_email **_\[str, required]_

> your new contact email address

**Sample Response (200)**

> ```
> {
>     "msg": "email has been sent, please check it in your current email."
> }
>
> ```


