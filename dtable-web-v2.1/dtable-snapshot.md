# Base Snapshots

Every 24 hours, SeaTable makes a snapshot of an active base. This snapshot is stored for a certain period of time (For more details about how long a snapshot will be stored, refer to [SeaTable Plans](https://seatable.io/en/pricing/)).

## List the Snapshots of A Base

List all the currently stored snapshots of a base.


**URL Structure**

> **\[GET]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/snapshots/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

List max. 2 of the available snapshots of the base `Memoir` in the workspace `1`:

> ```
> curl --location --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://table.seafile.com/api/v2.1/workspace/1/dtable/Memoir/snapshots/?page=1&per_page=2' 
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned user list.

**per_page** _\[int, optional, 25 by default]_
> Number of users displayed on each page.



**Return Values**

JSON-object with the list of snapshots, including the `commit_id` of the snapshots.


**Sample Response**

The returned list offers details of two currently available snapshots, and the returned `has_next_page` value indicates that there are more than 2 snapshots in total:
> ```
> {
>     "snapshot_list": [
>         {
>             "dtable_name": "Memoir.dtable",
>             "commit_id": "031a572cc911bf64b053d3d4f75d5c37c4c932fa",
>             "ctime": "2020-11-19T09:55:20+00:00"
>         },
>         {
>             "dtable_name": "Memoir.dtable",
>             "commit_id": "c9f712dc1d077448fc2932a140d7312ed31a784f",
>             "ctime": "2020-11-17T11:58:36+00:00"
>         }
>     ],
>     "page_info": {
>         "has_next_page": true,
>         "current_page": 1
>     }
> }
> ```
If the queried base doesn't have any snapshots, an empty list will be returned without error message.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the requested base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Memory not found."
> }
> ```


## Restore A Base's Snapshot

Use this request to restore a certain snapshot. The restored snapshot is saved as a separate base besides the existing base, so the original base won't be changed during this operation.


**URL Structure**

> **\[POST]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/snapshots/`<commit_id>`/restore/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

Restore the snapshot with the following `commit_id` and give the restored base the name of `Old Memoir`:

> ```
> curl --request POST \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/Memoir/snapshots/aaeea690cfddb542627d0223426ba0840c03c7de/restore/' \
> --form 'snapshot_name="Old Memoir"'
> ```


**Input Parameters**

**commit_id** _\[string, required]_
> The ID of the snapshot, as acquired from the list of all snapshots.

**snapshot_name** _\[string, optional]_
> Give a name to the restored base. If left empty, SeaTable API will give the new base a default name like "Memoir (Restored)". 



**Return Values**

JSON-object with the details of the restored base.


**Sample Response (200)**

The details of the restored snapshot as a new base are returned:

> ```
> {
>     "dtable": {
>         "id": 403,
>         "workspace_id": 1,
>         "uuid": "3f32d484-6e55-4a9e-b718-3482f0cd0c24",
>         "name": "Old Memoir",
>         "creator": "Robert Teamplayer",
>         "modifier": "Robert Teamplayer",
>         "created_at": "2020-12-15T15:31:39+00:00",
>         "updated_at": "2020-12-15T15:31:39+00:00",
>         "color": null,
>         "text_color": null,
>         "icon": null
>     }
> }
> ```


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the requested base (workspace):
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "dtable Memory not found."
> }
> ```

404 Not Found: The `commit_id` was not found:
> ```
> {
>     "error_msg": "commit_id not found."
> }
> ```
