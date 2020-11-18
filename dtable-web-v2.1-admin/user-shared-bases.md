# User shared bases

## List bases shared with user

**GET** /api/v2.1/admin/users/:email/shared-dtables/

**Request params**

* **page**: the number of page to list, default 1, optional
* **per_page**: the number of tables per page, default 25, optional

**Sample request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/admin/users/xiongchao.cheng@seafile.com/shared-dtables/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Sample response**

```
{
    "dtable_list": [
        {
            "id": 270,
            "workspace_id": 111,
            "uuid": "7acce6ca-2f03-4c3f-8f3a-33b905af8d57",
            "name": "for-del",
            "creator": "test",
            "modifier": "test",
            "created_at": "2020-04-13T03:58:52+00:00",
            "updated_at": "2020-06-23T09:27:31+00:00",
            "rows_count": 1,
            "from_user": "68@seafile_group"
        }
    ],
    "count": 2
}

```


