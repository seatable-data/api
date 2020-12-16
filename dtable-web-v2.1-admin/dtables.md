# DTables (Bases)

## List All Bases

List all the bases of all organizations and users.

**URL Structure**

>**\[GET]** /api/v2.1/admin/dtables/

**Request Authentication**

> Admin Authentication (Token)


**Sample Request**

List 3 bases:
>```
> curl \
> -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; indent=4' \
> "https://cloud.seatable.io/api/v2.1/admin/dtables/?page=1&per_page=3"
>```

**Input Parameters**

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned base list.

**per_page** _\[int, optional, 100 by default]_
> Number of bases displayed on each page.

**Return Values**

JSON-object with the list of bases.

**Sample Response (200)**

Response from the sample request shows Page 1 with 3 bases and their detailed infos. The returned `"has_next_page"` value indicates there are more pages:

>```
>{
>    "page_info": {
>        "has_next_page": true,
>        "current_page": 1
>    },
>    "dtables": [
>        {
>            "id": 1,
>            "workspace_id": 1,
>            "uuid": "42a120a7-f6c8-4005-b527-b4971234a7c7",
>            "name": "test",
>            "creator": "Meng Wu",
>            "modifier": "Meng Wu",
>            "created_at": "2019-11-13T11:15:58+00:00",
>            "updated_at": "2019-11-13T11:15:58+00:00",
>            "color": null,
>            "text_color": null,
>            "icon": null,
>            "owner": "Meng Wu",
>            "org_id": -1,
>            "rows_count": 6
>        },
>        {
>            "id": 2,
>            "workspace_id": 3,
>            "uuid": "0f0564f8-350b-4222-a4b4-7f74d0b12342",
>            "name": "Seafile Issues Report",
>            "creator": "Daniel Pan",
>            "modifier": "Christoph Dyllick-Brenzinger",
>            "created_at": "2019-11-14T02:28:02+00:00",
>            "updated_at": "2020-07-17T08:17:19+00:00",
>            "color": null,
>            "text_color": null,
>            "icon": null,
>            "owner": "Seafile-Datamate (group)",
>            "org_id": -1,
>            "rows_count": 80
>        },
>        {
>            "id": 5,
>            "workspace_id": 4,
>            "uuid": "1cf7aa4a-e02e-44fe-a03e-1332b5742392",
>            "name": "Online Testing",
>            "creator": "Meng Wu",
>            "modifier": "Meng Wu",
>            "created_at": "2019-11-14T07:53:17+00:00",
>            "updated_at": "2019-11-14T07:54:30+00:00",
>            "color": null,
>            "text_color": null,
>            "icon": null,
>            "owner": "Meng Wu",
>            "org_id": -1,
>            "rows_count": 0
>        }
>    ]
>}
>```

**Possible Errors**

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




## List A User's Bases

List all the bases of a certain user by user's ID.

**URL Structure**

> **\[GET]** /api/v2.1/admin/users/`<email>`/dtables/


**Request Authentication**

> Admin Authentication (Token)


**Sample Request**

List 3 bases of the user with ID 0ef256cb71584188b1b147b2530c2904@auth.local:
>```
> curl --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/users/0ef256cb71584188b1b147b2530c2904@auth.local/dtables/?page=1&per_page=3' 
>```


**Input Parameters**

**email** _\[string, required]_
> The user ID ending with @auth.local, e.g. '0ef256cb71584188b1b147b2530c2904@auth.local'.

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned base list.

**per_page** _\[int, optional, 25 by default]_
> Number of bases displayed on each page.



**Return Values**

JSON-object with the list of bases.


**Sample Response (200)**

Response from the sample request shows Page 1 with 3 bases and their detailed infos. The returned `"count"` value shows that this user has 5 bases in total:

>```
>{
>    "dtable_list": [
>        {
>            "id": 258,
>            "workspace_id": 135,
>            "uuid": "4b572a04-39b7-4ce7-aa08-7fe1f4dad0b6",
>            "name": "DtableTestBase",
>            "creator": "Robert Mitarbeiter",
>            "modifier": "Robert Mitarbeiter",
>            "created_at": "2020-11-19T14:43:24+00:00",
>            "updated_at": "2020-11-19T14:43:24+00:00",
>            "color": "#7626FD",
>            "text_color": "#7626FD",
>            "icon": "icon-software-test-management",
>            "rows_count": 0
>        },
>        {
>            "id": 124,
>            "workspace_id": 136,
>            "uuid": "29000004-6236-4cf7-90ae-cbe649959776",
>            "name": "external",
>            "creator": "Robert Mitarbeiter",
>            "modifier": "Robert Mitarbeiter",
>            "created_at": "2020-11-17T15:29:48+00:00",
>            "updated_at": "2020-11-17T15:29:48+00:00",
>            "color": null,
>            "text_color": null,
>            "icon": null,
>            "rows_count": 0
>        },
>        {
>            "id": 305,
>            "workspace_id": 137,
>            "uuid": "03d8a71c-84c7-4a16-b314-94c886dc170b",
>            "name": "formtest",
>            "creator": "Robert Mitarbeiter",
>            "modifier": "Robert Mitarbeiter",
>            "created_at": "2020-11-17T15:39:26+00:00",
>            "updated_at": "2020-11-17T15:39:26+00:00",
>            "color": null,
>            "text_color": null,
>            "icon": null,
>            "rows_count": 8
>        },
>    ],
>    "count": 5
>}
>
>```
If the user's ID was not found, no errors will be raised. Instead, an empty list is returned.

**Possible Errors**

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



## List An Organization's Bases

List all the bases of a certain organization by ID.

**URL Structure**

> **\[GET]** /api/v2.1/admin/organizations/`<org_id>`/dtables/


**Request Authentication**

> Admin Authentication (Token)


**Sample Request**

List 1 base of the organization with ID 23:

>```
> curl --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/organizations/23/dtables/?page=1&per_page=1'
>```

**Input Parameters**

**org_id** _[int, required]_
> The organization ID. 

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned base list.

**per_page** _\[int, optional, 25 by default]_
> Number of bases displayed on each page.



**Return Values**

JSON-object with the list of bases.



**Sample Response (200)**

Response from the sample request shows Page 1 with 1 base and its detailed infos. The returned `"count"` value indicates this organization has 6 bases in total: 

>```
>{
>    "dtable_list": [
>        {
>            "id": 999,
>            "workspace_id": 909,
>            "uuid": "24fdb4a5-282e-41f2-9724-5d9b42345694",
>            "name": "for-delete-restore",
>            "creator": "org~4-admin-1",
>            "modifier": "org~4-admin-1",
>            "created_at": "2020-04-14T07:15:13+00:00",
>            "updated_at": "2020-04-14T07:15:13+00:00",
>            "rows_count": 0
>        }
>    ],
>    "count": 6
>}
>
>```

**Possible Errors**

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

404 Not Found: The organization ID was not found:
>```
>{
>    "error_msg": "Organization 177 not found."
>}
>```



## List Trash Bases

List all the bases that are in the trash bin.

**URL Structure**

> **\[GET]** /api/v2.1/admin/trash-dtables/


**Request Authentication**

> Admin Authentication (Token)


**Sample Request**

List 3 trashed bases in the current system:

>```
> curl -X GET \
> -H 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/trash-dtables/?page=1&per_page=3' 
>```

**Input Parameters**

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned base list.

**per_page** _\[int, optional, 25 by default]_
> Number of bases displayed on each page.


**Return Values**

JSON-object with the list of trashed bases.


**Sample Response (200)**

Response from the sample request shows Page 1 with 3 bases and their infos. The returned `"count"` indicates there're 41 bases in the trash bin:

>```
>{
>    "count": 41,
>    "trash_dtable_list": [
>        {
>            "id": 382,
>            "workspace_id": 177,
>            "uuid": "9ba13c04-7154-4b51-a0c7-3ce500d96b5e",
>            "name": "pt",
>            "creator": "Robert Mitarbeiter",
>            "modifier": "Robert Mitarbeiter",
>            "created_at": "2020-11-27T11:00:07+00:00",
>            "updated_at": "2020-11-27T11:00:07+00:00",
>            "color": null,
>            "text_color": null,
>            "icon": null,
>            "deleted": true,
>            "delete_time": "2020-11-27T11:12:12+00:00",
>            "owner": "Robert Mitarbeiter",
>            "org_id": 120,
>            "org_name": "API Test"
>        },
>        {
>            "id": 381,
>            "workspace_id": 177,
>            "uuid": "f76d153f-8104-4775-8e13-ea0f1b9ef2bc",
>            "name": "pt",
>            "creator": "Robert Mitarbeiter",
>            "modifier": "Robert Mitarbeiter",
>            "created_at": "2020-11-27T10:43:44+00:00",
>            "updated_at": "2020-11-27T10:43:44+00:00",
>            "color": null,
>            "text_color": null,
>            "icon": null,
>            "deleted": true,
>            "delete_time": "2020-11-27T10:59:56+00:00",
>            "owner": "Robert Mitarbeiter",
>            "org_id": 120,
>            "org_name": "API Test"
>        },
>        {
>            "id": 309,
>            "workspace_id": 5,
>            "uuid": "f1b991ee-9964-489c-9172-87c83358a5df",
>            "name": "fafds",
>            "creator": "Robert Mitarbeiter",
>            "modifier": "Robert Mitarbeiter",
>            "created_at": "2020-11-02T16:50:12+00:00",
>            "updated_at": "2020-11-02T16:57:52+00:00",
>            "color": "#1DDD1D",
>            "text_color": null,
>            "icon": "icon-customer-inquiry",
>            "deleted": true,
>            "delete_time": "2020-11-26T12:35:52+00:00",
>            "owner": "Robert Mitarbeiter",
>            "org_id": -1
>        }
>    ]
>}
>```

**Possible Errors**

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


## Restore A Base from Trash

Restore a deleted base from the trash bin and put it back where it was.

**URL Structure**

> **\[PUT]** /api/v2.1/admin/trash-dtables/`<dtable_id>`/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

Restore the base with token 64b9ee55dc4ab902ff36763ef5c604a76d52875e from the trash bin:

>```
>curl -X PUT \
>-H 'authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
>'https://cloud.seatable.io/api/v2.1/admin/trash-dtables/30/' 
>```

**Input Parameters**

**dtable_id** _\[int, required]_
> The ID of the base that needs to be restored.


**Return Values**

JSON-object with the result of operation.


**Response Sample**

Response from the sample request shows the base has been restored successfully:

>```
>{
>    "success": true
>}
>
>```

**Possible Errors**

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

404 Not Found: The base is not in the trash:
>```
>{
>    "error_msg": "Table not found"
>}
>```

