# Org admin work Weixin

## Get work Weixin info

**GET** /api/v2.1/org/:org_id/admin/work-weixin/info/

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/org/23/admin/work-weixin/info/' --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6'

```

**Sample Response**

```
{
    "corp": {
        "org_id": 3,
        "corp_id": "cropid",
        "corp_name": "SeaTable",
        "department_count": 2
    }
}

```


