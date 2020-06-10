# Org admin settings

## Get Org Settings

**GET** api/v2.1/org/admin/settings/

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/org/admin/settings/' \
--header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6'

```

**Sample Response**

```
{
    "enable_force_2fa": false
}

```

## Update Org Settings

**PUT** api/v2.1/org/admin/settings/

**Request Params**

* **enable_force_2fa**: enable force org users two factor Authorization, optional, 0/1
* ...**other settings**

**Sample Request**

```
curl --location --request PUT 'https://cloud.seatable.io/api/v2.1/org/admin/settings/' \
--header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
--form 'enable_force_2fa=0'

```

**Sample Response**

```
{
    "enable_force_2fa": false
}

```


