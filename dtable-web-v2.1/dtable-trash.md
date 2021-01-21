# Bases Trash Bin

## List Trashed Bases

List all the bases in the trash bin. 

**URL Structure**

> **\[GET]** /api/v2.1/trash-dtables/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

```
curl \
--header 'Authorization: Token 788fe6cf0776feb46f311f014587105e7a4f7089' \
https://cloud.seatable.io/api/v2.1/trash-dtables/ 
```

**Input Parameters**

None.


**Return Values**

JSON-object with the detailed list of trashed bases. The value of the `id` is the ID of the base.


**Sample Response**

> ```
> {
>     "count": 1,
>     "trash_dtable_list": [
>         {
>             "id": 32,
>             "workspace_id": 20,
>             "uuid": "123aca9c-1cd1-4556-a00c-36546644f9be",
>             "name": "customer_test_2",
>             "creator": "Robert Teamleader",
>             "modifier": "Robert Teamleader",
>             "created_at": "2020-11-27T02:23:04+00:00",
>             "updated_at": "2020-11-27T02:23:04+00:00",
>             "color": null,
>             "text_color": null,
>             "icon": null,
>             "deleted": true,
>             "delete_time": "2020-11-30T05:36:54+00:00"
>         },
>     ]
> }
> ```
If there's no trashed bases, an empty list is returned without error message.


**Possible Errors**

401 Unauthorized: The auth token was not valid:
> ```
> {
>     "detail": "Invalid token"
> }
> ```




## Restore A Trashed Base

Restore a deleted base from the trash bin.


**URL Structure**

> **\[PUT]** /api/v2.1/trash-dtables/`<dtable_id>`/


**Request Authentication**

> User Authentication (Token)





**Sample Request**

> ```
> curl -X PUT \
> --header 'Authorization: Token 788fe6cf0776feb46f311f014587105e7a4f7089' \
> https://cloud.seatable.io/api/v2.1/trash-dtables/32/ 
> ```


**Input Parameters**

**dtable_id** _\[int, required]_
> The ID of the trashed base to be restored. This can be retrieved from the call **List Trashed Bases**.



**Return Values**

JSON-object with the result of the operation.


**Sample Response**

>```
>{
>    "success": true,
>}
>```

**Possible Errors**

401 Unauthorized: The auth token was not valid:
> ```
> {
>     "detail": "Invalid token"
> }
> ```

404 Not Found: The base is not in the trash bin (already restored, or has been permanently deleted):
> ```
> {
>     "error_msg": "Table not found."
> }
> ```

