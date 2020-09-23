# User storage

## List user's storage

**GET** /api/v2.1/admin/users/:email/storage/

**Request Params**

* **parent_dir**: in which list dirs/files are in

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/admin/users/xiongchao.cheng%40seafile.com/storage/' \
--header 'Authorization: Token 3120688f207383ba90e6160190ff70036d2e185d'

```

**Sample Response**

```
{
    "dirent_list": [
        {
            "is_file": false,
            "obj_name": "asset",
            "file_size": "",
            "last_update": "2020-08-13T02:05:15+00:00"
        },
        {
            "is_file": true,
            "obj_name": "_(deleted_296) for-copy-2.dtable",
            "file_size": 1356,
            "last_update": "2020-06-17T07:12:01+00:00"
        }
    ],
    "email": "xiongchao.cheng@seafile.com"
}

```


