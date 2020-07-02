# Forms

## List All Forms

**GET** /api/v2.1/admin/forms/

**Request Params:**

* **page**: the number of page to list, default 1, optional
* **per_page**: the number of tables per page, default 25, optional

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/admin/forms/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Sample Response**

```
{
    "form_list": [
        {
            "id": 1,
            "form_id": "JCVu",
            "form_name": "wow-form",
            "username": "admin",
            "dtable_uuid": "a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf",
            "dtable_name": "first"
        }
    ],
    "count": 6
}

```


