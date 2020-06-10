# Activities

## List Row Activities

**GET** /api/v1/dtables/:dtable_uuid/activities/

**Request Parameters**

* **row_id**: row id, required
* **page**: page number, default 1, optional
* **per_page**: number of activities per page, default 10, optional

**Sample Request**

```
curl -X GET \
  https://cloud.seatable.io/dtable-server/api/v1/dtables/a57b56d31cc54ebd8a6ca1b28ac3dbdf/activities/?page=1&row_id=YMIviMeERQCUiQhPPqo6Gw \
  -H 'authorization: Token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1Nzg4MDIxNjUsImR0YWJsZV91dWlkIjoiYTU3YjU2ZDMxY2M1NGViZDhhNmNhMWIyOGFjM2RiZGYiLCJ1c2VybmFtZSI6Inhpb25nY2hhby5jaGVuZ0BzZWFmaWxlLmNvbSIsInBlcm1pc3Npb24iOiJydyJ9.CfhFnZ_zG2oVU3awhbeRMv_ttya5Jb7I4hKrUgoLook'

```

**Sample Response**

```
{
    "activities": [
        {
            "id": 1,
            "dtable_uuid": "a57b56d31cc54ebd8a6ca1b28ac3dbdf",
            "row_id": "YMIviMeERQCUiQhPPqo6Gw",
            "op_user": "xiongchao.cheng@seafile.com",
            "op_type": "insert_row",
            "op_time": "2020-01-09T11:45:29.000Z",
            "detail": {
                "table_id": "0000",
                "table_name": "Table1",
                "row_name": "for-events-2",
                "row_data": [
                    {
                        "column_key": "0000",
                        "column_name": "first-col-in-first-table",
                        "column_type": "text",
                        "column_data": {},
                        "value": "for-events-2"
                    },
                    {
                        "column_key": "b8ee",
                        "column_name": "images",
                        "column_type": "image",
                        "column_data": {},
                        "value": ""
                    },
                    {
                        "column_key": "w21y",
                        "column_name": "files",
                        "column_type": "file",
                        "column_data": {},
                        "value": ""
                    },
                    {
                        "column_key": "u5M3",
                        "column_name": "people",
                        "column_type": "collaborator",
                        "column_data": {},
                        "value": ""
                    }
                ]
            }
        }
    ],
    "total_count": 1
}

```

**Errors**

* **404** Bad Request.
* **403** Permission Denied.
* **500** Internal Server Error.


