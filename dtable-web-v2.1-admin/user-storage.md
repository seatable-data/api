# User storage

## List A User's Storage Objects

List objects stored by a certain user by the user's ID (`<email>`).


**URL Structure**

> **\[GET]** /api/v2.1/admin/users/`<email>`/storage/



**Request Authentication**

> Admin Authentication (Token)



**Sample Request**

Inspect the storage of the user with ID `31452cfaf1154efba122f92359f4e580@auth.local` and list the objects in the root (`\`) folder:

>```
>curl --request GET \
>--header 'Authorization: Token 3120688f207383ba90e6160190ff70036d2e185d' \
>'https://cloud.seatable.io/api/v2.1/admin/users/31452cfaf1154efba122f92359f4e580@auth.local/storage/?parent_dir=/' 
>```



**Input Parameters**

**email** _\[string, required]_
> The user's ID that ends with `@auth.local` (not the user's email address).

**parent_dir** _\[string, optional]_
> In which list dirs/files are in.



**Return Values**

JSON-object with the list of storage objects.



**Sample Response**

The following response shows three items with their details in the parent directory:

* A folder named "asset",
* a base "Test" labeled as deleted,
* and a normal base "Told":

>```
>{
>    "dirent_list": [
>        {
>            "obj_id": "965bfc4817b429e7629e765a42ac117b27483cfd",
>            "is_file": false,
>            "obj_name": "asset",
>            "file_size": "",
>            "last_update": "2020-08-13T02:05:15+00:00"
>        },
>        {
>            "obj_id": "48965bfc4817b429e765a42ac117b401e7800727",
>            "is_file": true,
>            "obj_name": "_(deleted_296) Test.dtable",
>            "file_size": 1356,
>            "last_update": "2020-06-17T07:12:01+00:00"
>        },
>        {
>            "obj_id": "5a42ac117b401e780072748965bfc4817b429e76",
>            "is_file": true,
>            "obj_name": "Told.dtable",
>            "file_size": 447,
>            "last_update": "2020-11-06T09:58:01+00:00"
>        }
>    ],
>    "email": "31452cfaf1154efba122f92359f4e580@auth.local"
>}
>```

If the ID (`email` that ends with `@auth.local`) was mistaken by the user's `contact_email` (the real email address), an empty list will be returned (**200**) without error message (A "Not found" error will only be returned when neither the `email` nor the `contact_email` were found):

>```
>{
>    "dirent_list": [],
>    "email": "someone-using-SeaTable@example.com"
>}
>```



**Possible Errors**

400 Not Found: The given user's not found:
>```
>{
>    "error_msg": "Workspace not found."
>}
>```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```