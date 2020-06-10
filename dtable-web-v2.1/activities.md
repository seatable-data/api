# Activities

## Get Activities

**GET** api/v2.1/dtable-activities/

**Request parameters**

* page (default=1)
* per_page (default=25)
* avatar_size (default=72)

**Sample request**

```
curl -H 'Authorization: Token a407800e307ee8eb545fab94e2d22bb37944661f' -H 'Accept: application/json; charset=utf-8; indent=4' "http://127.0.0.1:8001/api/v2.1/dtable-activities/"

```

**Sample response**

```json
{
    "activities": [
        {
            "dtable_uuid": "d48c3aaedbc14325a8901c2e79ea5319",
            "row_id": "NqXZP3YyTyCBOlPf5RNvWQ",
            "op_type": "modify_row",
            "author_email": "1@1.com",
            "author_name": "Alex",
            "author_contact_email": "1@1.com",
            "op_time": "2019-12-13T17:38:15",
            "table_id": "0000",
            "table_name": "Table",
            "row_data": [
                {
                    "column_key": "0000",
                    "column_name": "Name",
                    "column_type": "text",
                    "value": "Bob"
                },
                {
                    "column_key": "YL33",
                    "column_name": "Character",
                    "column_type": "text",
                    "value": "well",
                    "old_value": "good"
                }
            ],
            "avatar_url": "http://127.0.0.1:8000/media/avatars/d/2/19af79b45e5891507fda4c4c2139a0/resized/72/03e77af8819c66f25260297dd5e97dc7.png"
        },
        {
            "dtable_uuid": "d48c3aaedbc14325a8901c2e79ea5319",
            "row_id": "e95bd622-4081-4169-823d-4462e00cbf06",
            "op_type": "modify_row",
            "author_email": "1@1.com",
            "author_name": "Alex",
            "author_contact_email": "1@1.com",
            "op_time": "2019-12-13T16:45:17",
            "table_id": "0000",
            "table_name": "Table",
            "row_data": [
                {
                    "column_key": "0000",
                    "column_name": "Name",
                    "column_type": "text",
                    "value": "Alex"
                },
                {
                    "column_key": "YL33",
                    "column_name": "Gender",
                    "column_type": "text",
                    "value": "nice",
                    "old_value": "male"
                }
            ],
            "avatar_url": "http://127.0.0.1:8000/media/avatars/d/2/19af79b45e5891507fda4c4c2139a0/resized/72/03e77af8819c66f25260297dd5e97dc7.png"
        },
    ]
}

```

**Errors**

* 400 Bad Request.
* 500 Internal Server Error.


