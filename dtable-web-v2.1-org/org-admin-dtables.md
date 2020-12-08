# Organization Administrator: Bases Operations

## List Bases

An org-admin (organization administrator) can use this API call to list all the bases in their own organization.


**URL Structure**

> **\[GET]** /api/v2.1/org/`<org_id>`/admin/dtables/


**Request Authentication**

> Org-admin Authentication (Token)


**Sample Request**

List two bases in the organization with `org_id` of 23:

> ```
> curl --request GET \
> --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
> 'https://cloud.seatable.io/api/v2.1/org/23/admin/dtables/?page=1&per_page=2' 
> ```


**Input Parameters**

**org_id** _\[numeric, required]_
> The organization ID for the request.

**page** _\[numeric, optional, 1 by default]_ 
> Page number of the returned base list.

**per_page** _\[numeric, optional, 25 by default]_
> Number of bases displayed on each page.



**Return Values**

JSON-object with the list of bases with their detailed infos.



**Sample Response (200)**

Two bases are listed in the response to the sample request. The returned `"count"` value indicates there are 8 bases in this organization in total. Among others, the returned `id` value is the ID of the base:

> ```
> {
>     "dtable_list": [
>         {
>             "id": 321,
>             "workspace_id": 826,
>             "uuid": "fa282c65-9d94-4f97-b6fe-8b5538xn4a87",
>             "name": "Told",
>             "creator": "Max Teamleiter",
>             "modifier": "Max Teamleiter",
>             "created_at": "2020-11-06T09:54:01+00:00",
>             "updated_at": "2020-11-06T09:54:01+00:00",
>             "color": null,
>             "text_color": null,
>             "icon": null,
>             "owner": "Max Teamleiter",
>             "rows_count": 0
>         },
>         {
>             "id": 724,
>             "workspace_id": 827,
>             "uuid": "f492ab5d-a796-4ef5-909d-b491c83nf8a0",
>             "name": "Test Phase",
>             "creator": "Robert Mitarbeiter",
>             "modifier": "Robert Mitarbeiter",
>             "created_at": "2020-11-06T14:56:02+00:00",
>             "updated_at": "2020-11-17T12:58:21+00:00",
>             "color": null,
>             "text_color": null,
>             "icon": null,
>             "owner": "Robert Mitarbeiter",
>             "rows_count": 47
>         }
>     ],
>     "count": 8
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have org-admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```


## Delete A Base

Delete a base from the organization and move it into the trash bin.


**URL Structure**

> **\[DELETE]** /api/v2.1/org/`<org_id>`/admin/dtables/`<dtable_id>`/


**Request Authentication**

> Org-admin Authentication (Token)



**Sample Request**

Delete the base with `dtable_id` 277 from the organization with `org_id` 23:

> ```
> curl --request DELETE \
> --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
> 'https://cloud.seatable.io/api/v2.1/org/23/admin/dtables/277/' 
> ```

**Input Parameters**

**org_id** _\[numeric, required]_
> ID of the organization from which the base is to be deleted.

**dtable_id** _\[numeric, required]_
> ID of the base to be deleted. 



**Return Values**

JSON-object with the result of the operation.



**Sample Response (200)**

The returned result indicates the base has been deleted.

> ```
> {
>     "success": true
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have org-admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```

404 Not Found: The given base was not found in the organization, or already deleted:
> ```
> {
>     "error_msg": "table not found."
> }
> ```

## List Trash Bases

List all the trashed bases in the organization.


**URL Structure**

> **\[GET]** /api/v2.1/org/`<org_id>`/admin/trash-dtables/



**Request Authentication**

> Org-admin Authentication (Token)



**Sample Request**

List one trashed base in the organization with `org_id` 23:

> ```
> curl --request GET \
> --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
> 'https://cloud.seatable.io/api/v2.1/org/23/admin/trash-dtables/?page=1&per_page=1' 
> ```

**Input Parameters**

**page** _\[numeric, optional, 1 by default]_ 
> Page number of the returned trash base list.

**per_page** _\[numeric, optional, 25 by default]_
> Number of trashed bases displayed on each page.



**Return Values**

JSON-object with trashed base list and the base details.



**Sample Response (200)**

The returned list shows one trashed base with its detailed information, and the `"count"` value indicates there are 26 trashed bases in the organization:

> ```
> {
>     "dtable_list": [
>         {
>             "id": 277,
>             "workspace_id": 796,
>             "uuid": "fa282c65-9d94-4f97-b6fe-8b55lkdk2a87",
>             "name": "Told",
>             "creator": "Max Teamleiter",
>             "modifier": "Max Teamleiter",
>             "created_at": "2020-11-06T09:54:01+00:00",
>             "updated_at": "2020-11-06T09:54:01+00:00",
>             "color": null,
>             "text_color": null,
>             "icon": null,
>             "deleted": true,
>             "delete_time": "2020-11-08T11:03:54+00:00",
>             "owner": "Max Teamleiter"
>         }
>     ],
>     "count": 26
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have org-admin permission for the given organization:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```



## Restore a Base

Restore a base from the trash bin.


**URL Structure**

> **\[PUT]** /api/v2.1/org/`<org_id>`/admin/trash-dtables/`<dtable_id>`/


**Request Authentication**

> Org-admin Authentication (Token)


**Sample Request**

Restore the base with `dtable_id` of 277 from the trash bin in the organization with `org_id` 23:

> ```
> curl --request PUT \
> --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
> 'https://cloud.seatable.io/api/v2.1/org/23/admin/trash-dtables/277/' 
> ```


**Input Parameters**

**org_id** _\[numeric, required]_
> ID of the organization in which the base is to be restored.

**dtable_id** _\[numeric, required]_
> ID of the base to be restored.


**Return Values**

JSON-object with the result of the operation.




**Sample Response (200)**

The response indicates the restoring was successful:

> ```
> {
>     "success": true
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have org-admin permission for the given organization:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```

404 Not Found: the base was not found in the trash bin:
> ```
> {
>     "error_msg": "Table not found."
> }
> ```


