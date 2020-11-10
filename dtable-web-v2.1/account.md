# Account

## Get account info

**GET** /api2/account/info/﻿

**Sample request**

```
curl -H "Authorization: Token asd410d592f59efc64410bbf4ee7602eb6854dd7" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api2/account/info/

```

**Sample response**

```json
{
    "space_usage": "0%",
    "total": -2,
    "usage": 3198516,
    "row_usage_rate": "1.15%",
    "row_total": 2000,
    "row_usage": 23,
    "avatar_url": "https://cloud.seatable.io/image-view/avatars/5/2/731e5a1304b90d990dce20afb2cf33/resized/72/03e77af8819c66f25260297dd5e97dc7_5kJmrG6.png",
    "email": "user@email.com",
    "name": "username",
    "login_id": "",
    "contact_email": "user@email.com",
    "institution": "",
    "is_staff": false,
    "enable_chargebee": false,
    "enable_subscription": false,
    "email_notification_interval": 0
}

```

**Errors**

* 403 Invalid token


