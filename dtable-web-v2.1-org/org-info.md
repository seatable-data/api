# Org Info

## Update Org Info

**PUT** https\://cloud.seatable.io/api/v2.1/org/admin/info/

**Request parameters**

* new_org_name: optional

**Request Sample**

```
curl -X PUT -H 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' -H 'Content-Type: multipart/form-data' 'https://cloud.seatable.io/api/v2.1/org/admin/info/' -F 'org_name=org~4-put-2'

```

**Response Sample**

```
{
    "success": true
}

```

**Errors**

* **403** Permission Denied.
* **500** Internal Server Error.


