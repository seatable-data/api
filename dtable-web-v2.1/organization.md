# Organization

## Get an Organization

**GET** /api/v2.1/organizations/:org_id/

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/organizations/23/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Sample Response**

```
{
    "org_id": 23,
    "org_name": "org~4-put-3"
}

```

## Migrate User Self to An Organization

**POST** /api/v2.1/user/migrate-org/

**Request Params**

* **org_id**: the ID of the organization which user want to migrate self to

**Sample Request**

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/user/migrate-org/' --header 'Authorization: Token c20d7a808581d3a0c267dc745e5edce6b9d44d89' --form 'org_id=23'

```

**Sample Response**

```
{
    "success": true
}

```


