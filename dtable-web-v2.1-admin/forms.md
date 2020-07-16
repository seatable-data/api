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
            "id": 14,
            "form_name": "for-add-form-1",
            "username": "admin",
            "dtable_name": "for-add",
            "token": "b1d5d00b-2da2-4b8d-9164-a0afa32ed5ee"
        },
        {
            "id": 16,
            "form_name": "for-add-form-2",
            "username": "admin",
            "dtable_name": "for-add",
            "token": "3f9ee7c8-7338-4ca5-b877-4df454c6ad8b"
        }
    ],
    "count": 2
}

```

## Delete a Form

DELETE /api/v2.1/admin/forms/:token/

**Sample Request**

```
curl --request DELETE 'https://cloud.seatable.io/api/v2.1/admin/forms/3f9ee7c8-7338-4ca5-b877-4df454c6ad8b/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Sample Response**

```
{
    "success": true
}

```

****


