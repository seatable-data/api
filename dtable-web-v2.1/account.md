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

**Sample Response (200)**

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




