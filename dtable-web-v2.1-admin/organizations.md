# Organizations

## List Organizations

List all the organizations in the current system.

**URL Structure**

> **\[GET]** /api/v2.1/admin/organizations/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

List 2 organizations in the system:

> ```
> curl --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/organizations/?page=1&per_page=2' 
>
> ```

**Input Parameters**

**page** _\[int, optional, 1 by default]_ 

> Page number of the returned organization list.

**per_page** _\[int, optional, 25 by default]_

> Number of organizations displayed on each page.

**Return Values**

JSON-object with the list of organizations.

**Sample Response (200)**

2 organizations with their details are listed in the response to the sample request. The returned `"count"` value indicates there are 152 organizations in total:

> ```
> {
>    "organizations": [
>        {
>            "org_id": 1,
>            "org_name": "Test-Admin",
>            "ctime": "2020-06-01T12:46:26+00:00",
>            "org_url_prefix": "org_8hz6uh",
>            "role": "org_default",
>            "creator_email": "8ca1997823b44dffbaa51e0dd0c35ac0@auth.local",
>            "creator_name": "Christoph Dyllick",
>            "creator_contact_email": "christoph@example.com",
>            "quota": -2,
>            "storage_usage": 0,
>            "storage_quota": 1000000000,
>            "max_user_number": 25,
>            "rows_count": 0,
>            "row_limit": 2000
>        },
>        {
>            "org_id": 2,
>            "org_name": "Testteam",
>            "ctime": "2020-06-01T16:04:06+00:00",
>            "org_url_prefix": "org_yuvlgo",
>            "role": "org_default",
>            "creator_email": "6a339c8f57e34010a63f2c46bb0d7e6c@auth.local",
>            "creator_name": "Ionas RDB (Teamadmin)",
>            "creator_contact_email": "rdb@example.com",
>            "quota": -2,
>            "storage_usage": 20011,
>            "storage_quota": 1000000000,
>            "max_user_number": 25,
>            "rows_count": 3,
>            "row_limit": 2000
>        }
>    ],
>    "count": 152
> }
>
> ```

**Possible Errors**:

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have admin permission:

> ```
> {
>    "detail": "You do not have permission to perform this action."
> }
>
> ```

## List Basic Info of Organizations by Organization ID list

With a list of `org_ids`, list the `org_name` of these organizations.

**URL Structure**

> **\[GET]** api/v2.1/admin/organizations-basic-info/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

List the basic info of the organizations with `org_ids` 1 and 2:

> ```
> curl --request GET \
> -header 'Authorization: Token 9308058de7056a5213d55831e184eb443c1936b4' \
> "https://cloud.seatable.io/api/v2.1/admin/organizations-basic-info/?org_ids=1&org_ids=2" 
>
> ```

**Input Parameters**

**org_ids** _\[multiple, int, required]_

> With each `org_ids`, the basic info of the corresponding organization will be returned. If an `org_ids` is invalid, it'll be ignored and no errors will be returned.

**Return Values**

JSON-object with the list of organizations' basic infos.

**Sample Response (200)**

The basic infos of the two organizations requested in the sample are returned:

> ```
> {
>    "organization_list": [
>        {
>            "org_id": 1,
>            "org_name": "Test-Admin"
>        },
>        {
>            "org_id": 2,
>            "org_name": "Testteam"
>        }
>    ]
> }
>
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have admin permission:

> ```
> {
>    "detail": "You do not have permission to perform this action."
> }
>
> ```

## Add An Organization

Add an organization in the current system.

**URL Structure**

> **\[POST]** /api/v2.1/admin/organizations/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

Add an organization with the name, administrator email and name, as well as admin password:

> ```
> curl --request POST \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/organizations/' \
> --form 'org_name=org-for-add' \
> --form 'admin_email=for-add@seafile.com' \
> --form 'admin_name=for-add' \
> --form 'password=123'
>
> ```

**Input Params**

**org_name** _\[string, required]_ 

> The name of the organization. It'll appear in the base library as "Team \<org_name>". It doesn't have to be unique in the system.

**admin_email** _\[string, email, required]_ 

> Organization administrator's email to log in. It must be a valid email address and is unique in the system.

**admin_name** _\[string, optional]_ 

> The organization administrator's full name.

**password** _\[string, required]_ 

> Organization administrator's password to log in.

**Return Values**

JSON-object with the details of the added organization. The `org_id` is automatically generated.

**Sample Response (201)**

The organization requested in the sample is added in the system, and its details are returned:

> ```
> {
>    "org_id": 3,
>    "org_name": "org-for-add",
>    "ctime": "2020-05-20T03:36:12+00:00",
>    "org_url_prefix": "org_0hht0tv6dmy2ibv6rhop",
>    "role": "org_default",
>    "creator_email": "585dd653ccbf4552ba69c3f04e6be2b6@auth.local",
>    "creator_name": "for-add",
>    "creator_contact_email": "for-add@seafile.com",
>    "quota": -2,
>    "storage_usage": 0,
>    "storage_quota": 1000000000,
>    "max_user_number": 25,
>    "rows_count": 0,
>    "row_limit": 2000
> }
>
> ```

**Possible Errors**

400 Bad Request: The administrator's email was not a valid email address:

> ```
> {
>    "error_msg": "admin_email invalid."
> }
>
> ```

400 Bad Request: The administrator's email is not unique in the system:

> ```
> {
>    "error_msg": "User for-add@seafile.com already exists."
> }
>
> ```

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have admin permission:

> ```
> {
>    "detail": "You do not have permission to perform this action."
> }
>
> ```

## Delete Organization

Delete an organization with its ID.

**URL Structure**

> **\[DELETE]** /api/v2.1/admin/organizations/`<org_id>`/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

Delete the organization with the ID 3:

> ```
> curl --request DELETE \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/organizations/3/' 
>
> ```

**Input Parameters**

**org_id** _\[int, required]_

> The ID of the organization to be deleted.

**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

The organization with the ID 3 was deleted successfully:

> ````
> {
>    "success": true
> }
> >```
>
> ````

**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have admin permission:

> ```
> {
>    "detail": "You do not have permission to perform this action."
> }
>
> ```

404 Not Found: the organization was not found:

> ```
> {
>    "error_msg": "Organization 999 not found."
> }
>
> ```

## Update Organization

Change the attributes of an organization.

**URL Structure**

> **\[PUT]** /api/v2.1/admin/organizations/`<org_id>`/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

Rename, change role and row limit of the organization with the ID 1:

> ```
> curl --request PUT \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/organizations/1/' \
> --form 'org_name=rename-org' \
> --form 'role=guest' \
> --form 'row_limit=100'
>
> ```

**Input Parameters**

**org_name** _\[string, optional]_

> The new name of the organization.

**max_user_number** _\[int, optional]_

> The new user number limit.

**role** _\[string, optional]_

> The role of the organization. SeaTable comes with two built-in roles `default` and `guest`. For more details, refer to the article [Roles and Permissions Support.](https://docs.seatable.io/published/seatable-manual/config/enterprise/roles_permissions.md)

**row_limit** _\[int, optional]_

> The new row number limit.

**asset_quota_mb** _\[int, optional]_

> The new limit of user's asset quota in Mb.

**Return Values**

JSON-object with the updated details of the organization.

**Sample Response (200)**

The returned values show that the organization was updated according to the sample request:

> ```
> {
>    "org_id": 1,
>    "org_name": "rename-org",
>    "ctime": "2020-01-11T07:58:25+00:00",
>    "org_url_prefix": "org_icveztvq1k9gfo9olksp",
>    "role": "guest",
>    "creator_email": "cf7c011380904d1b8beeeaad5234eb0c@auth.local",
>    "creator_name": "System Admin",
>    "creator_contact_email": "admin@example.com",
>    "quota": -2,
>    "storage_usage": 1426,
>    "max_user_number": 5,
>    "rows_count":34,
>    "row_limit":100,
> }
>
> ```

**Possible Errors**

400 Bad Request: the organization role was not defined:

> ```
> {
>    "error_msg": "Role standard invalid."
> }
>
> ```

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have admin permission:

> ```
> {
>    "detail": "You do not have permission to perform this action."
> }
>
> ```

## List Organization Users

List all the users in a certain organization.

**URL Structure**

> **\[GET]** /api/v2.1/admin/organizations/`<org_id>`/users/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

List all the users in the organization with the ID 120:

> ```
> curl --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/organizations/120/users/' 
>
> ```

**Input Parameters**

**org_id** _\[int, required]_

> The ID of the organization whose users are to be listed.

**Return Values**

JSON-object with the list of users.

**Sample Response (200)**

The users in the organization with ID 120 are listed:

> ```
> {
>    "users": [
>        {
>            "org_id": 120,
>            "email": "2436ce64315b4b4abfcff9e5491bb296@auth.local",
>            "name": "Karlheinz Mitarbeiter",
>            "contact_email": "mitarbeiter2@seatable.de",
>            "quota_total": -2,
>            "quota_usage": 0,
>            "create_time": "2020-11-19T11:06:12+00:00",
>            "last_login": "",
>            "active": true
>        },
>        {
>            "org_id": 120,
>            "email": "26815cfaf1154efba122f95559f4e580@auth.local",
>            "name": "Max Teamleiter",
>            "contact_email": "teamleiter@seatable.de",
>            "quota_total": -2,
>            "quota_usage": 0,
>            "create_time": "2020-11-06T09:36:39+00:00",
>            "last_login": "2020-12-04T08:16:31.701045",
>            "active": true
>        },
>        {
>            "org_id": 120,
>            "email": "9f11ca9949b946a3b200555db5ff1d23@auth.local",
>            "name": "Robert Mitarbeiter",
>            "contact_email": "mitarbeiter@seatable.de",
>            "quota_total": -2,
>            "quota_usage": 0,
>            "create_time": "2020-11-06T09:38:10+00:00",
>            "last_login": "2020-12-04T08:16:56.358809",
>            "active": true
>        }
>    ]
> }
>
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have admin permission:

> ```
> {
>    "detail": "You do not have permission to perform this action."
> }
>
> ```

404 Not Found: The organization ID was not found:

> ```
> {
>    "error_msg": "Organization 190 not found."
> }
>
> ```

## List Organization Groups

List all the groups in a certain organization with its ID.

**URL Structure**

> **\[GET]** /api/v2.1/admin/organizations/`<org_id>`/groups/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

List all the groups within the organization 135:

> ```
> curl --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/organizations/135/groups/' 
>
> ```

**Input Parameters**

**org_id** _\[int, required]_

> The ID of the requested organization.

**Return Values**

JSON-object with the list of groups.

**Sample Response (200)**

3 groups in the organization requested in the sample are listed in the response:

> ```
> {
>    "group_list": [
>        {
>            "group_name": "Project 1",
>            "creator_name": "Demo User1",
>            "creator_email": "4cc894da2cd14502bf7dfd922a2ee8e4@auth.local",
>            "created_at": "2020-11-06T23:07:01+00:00",
>            "group_id": 4
>        },
>        {
>            "group_name": "Project 2",
>            "creator_name": "Demo User2",
>            "creator_email": "4cc894da2cd14502bf7dfd944a2ff8e4@auth.local",
>            "created_at": "2020-11-06T23:07:07+00:00",
>            "group_id": 5
>        },
>        {
>            "group_name": "Project 3",
>            "creator_name": "Demo User3",
>            "creator_email": "4cc894da2cd17802bf7dfd944a2ee8e4@auth.local",
>            "created_at": "2020-11-07T00:56:03+00:00",
>            "group_id": 6
>        },
>    ]
> }
>
> ```
>
> If an organization doesn't have any groups in it, an empty list will be returned.

**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have admin permission:

> ```
> {
>    "detail": "You do not have permission to perform this action."
> }
>
> ```

404 Not Found: The given organization ID was not found:

> ```
> {
>    "error_msg": "Organization 113 not found."
> }
>
> ```

## Delete A Group

Delete a group with its `group_id`.

**URL Structure**

> **\[DELETE]** /api/v2.1/admin/groups/`<group_id>`/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

Delete the group with `group_id` 1:

> ```
> curl --request DELETE \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/groups/1/' 
>
> ```

**Input Parameters**

**group_id** _\[int, required]_

> The ID of the group to be deleted.

**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

The returned phrase indicates success:

> ```
> {
>    "success": true
> }
>
> ```
>
> As this API call ensures the group with the given `group_id` doesn't exist any more after the request, even if the given `group_id` is not found, the response will still indicate success.

**Possible Errors**

## List Organization Bases

List all the bases inside of an organization with its ID.

**URL Structure**

> **\[GET]** /api/v2.1/admin/organizations/`<org_id>`/dtables/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

List all the bases inside the organization with `org_id` 1:

> ```
> curl --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/admin/organizations/1/dtables/' 
>
> ```

**Input Parameters**

**org_id** _\[int, required]_

> The ID of the organization to be requested.

**page** _\[int, optional, 1 by default]_ 

> Page number of the returned base list.

**per_page** _\[int, optional, 25 by default]_

> Number of bases displayed on each page.

**Return Values**

JSON-object with the list of bases.

**Sample Response (200)**

The returned sample response indicates there are two bases inside this organization, and the details of the bases are listed:

> ```
> {
>    "dtable_list": [
>        {
>            "id": 216,
>            "workspace_id": 122,
>            "uuid": "d5be63a2-0fc0-4bbf-9731-e706a002ba81",
>            "name": "Project Tracker",
>            "creator": "Jasmin Tee",
>            "modifier": "Jasmin Tee",
>            "created_at": "2020-10-26T14:05:53+00:00",
>            "updated_at": "2020-10-26T14:05:58+00:00",
>            "color": "#656463",
>            "text_color": null,
>            "icon": "icon-company-inventory",
>            "owner": "Jasmin Tee",
>            "rows_count": 0
>        },
>        {
>            "id": 163,
>            "workspace_id": 123,
>            "uuid": "5db730e5-2d33-3h75-b640-b94728ee9984",
>            "name": "CRM & Sales",
>            "creator": "Jasmin Tee",
>            "modifier": "Jasmin Tee",
>            "created_at": "2020-10-26T14:05:58+00:00",
>            "updated_at": "2020-10-26T14:06:05+00:00",
>            "color": "#4CAF50",
>            "text_color": null,
>            "icon": "icon-dollar",
>            "owner": "Jasmin Tee",
>            "rows_count": 65
>        }
>    ],
>    "count": 2
> }
>
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have admin permission:

> ```
> {
>    "detail": "You do not have permission to perform this action."
> }
>
> ```

404 Not Found: The requested organization was not found:

> ```
> {
>    "error_msg": "Organization 1299 not found."
> }
>
> ```



## List organizations by org id list

**URL Structure**

> **\[GET]** api/v2.1/admin/organizations-basic-info/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

> ```
> curl --request GET "https://cloud.seatable.io/api/v2.1/admin/organizations-basic-info/?org_ids=2&org_ids=1" --header 'Authorization: Token 9308058de7056a5213d55831e184eb443c1936b4'
>
> ```

**Input Parameters**

**org_ids**: _\[_multiple_, required]_

> The IDs of the organization to be requested.

**Sample Response (200)**

> ```none
> {
>     "organization_list": [
>         {
>             "org_id": 2,
>             "org_name": "org2"
>         },
>         {
>             "org_id": 1,
>             "org_name": "org1"
>         }
>     ]
> }
>
> ```


