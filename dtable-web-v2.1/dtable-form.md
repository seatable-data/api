# Forms

## List A Base's Forms

List all the forms in a base.


**URL Structure**

> **\[GET]** api/v2.1/forms/


**Request Authentication**

> User Authentication (Token)



**Sample Request**

List all the forms of the base `Survey` in the workspace `1`:

> ```
> curl \
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "http://cloud.seatable.io/api/v2.1/forms/?workspace_id=1&name=Survey"
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.


**Return Values**

JSON-object with the list of form(s).




**Sample Response**

The returned response lists off the two forms in the base `Survey`:

> ```
> {
>     "form_list": [
>         {
>             "id": 71,
>             "username": "6534ce64315b4b4abfcff9e5491db296@auth.local",
>             "workspace_id": 377,
>             "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60",
>             "form_id": "3AG1",
>             "form_config": "{\"form_name\":\"Customer Survey\"}",
>             "token": "783af6b3-8c67-4bb8-9529-80063cac6cd9",
>             "form_link": "https://cloud.seatable.io/dtable/forms/783af6b3-8c67-4bb8-9529-80063cac6cd9/",
>             "share_type": "anonymous",
>             "created_at": "2020-11-18T15:35:40+00:00",
>             "submit_count": 0
>         },
>         {
>             "id": 70,
>             "username": "6534ce64315b4b4abfcff9e5491db296@auth.local",
>             "workspace_id": 377,
>             "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60",
>             "form_id": "3BG1",
>             "form_config": "{\"form_name\":\"Employee Survey\"}",
>             "token": "b02c148c-b742-4ded-b9b1-6c8869fe94ba",
>             "form_link": "https://cloud.seatable.io/dtable/forms/b02c148c-b742-4ded-b9b1-6c8869fe94ba/",
>             "share_type": "anonymous",
>             "created_at": "2020-11-18T15:35:03+00:00",
>             "submit_count": 0
>         }
>     ]
> }
> ```
If there's no form in a base, an empty list will be returned without error message.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the workspace or the base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "DTable Survye not found."
> }
> ```

## Create A Form

Use this request to create a form and get its sharing link.


**URL Structure**

> **\[POST]** api/v2.1/forms/



**Request Authentication**

> User Authentication (Token)




**Sample Request**

Create a form `Vendor Survey` in the base `Surveys` from workspace `1` and give it the `form_id` of `1KOJ`:

> ```
> curl -X POST \
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' \
> "https://cloud.seatable.io/api/v2.1/forms/" \
> -d 'workspace_id=1&name=Surveys&form_id=1KOJ&form_config={"form_name":"Vendor Survey"}' 
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**name** _\[string, required]_
> The name of the base.

**form_id** _\[string, 4-digit, required]_
> Give the form a unique ID. It's a 4-digit combination of letters and numbers, like `1kOJ`. When creating a form on the web UI, this ID will be automatically generated.

**form_config** _\[string, required]_
> Use form_config={"form_name":"abc"} to give your form the name "abc". To customize this form, choose which columns to include in it, set required fields, add descriptions, add remarks, send notifications, add a notice on the top of the form, show a notice after submission, and add a redirect link after submission, etc., refer to the following example (detailed instructions will be added on this page shortly):
> ```json
>     {
>         "form_name":"Customer Survey",              // The name of your form
>         "columns":[                                 // Choose the columns to include
>             {
>                 "key":"0000",                       // The column ID
>                 "is_required":false,                // Set obligation
>                 "description":"",                   // Add a description if needed
>                 "filters":[],                       // Conditional question (details follow)
>                 "filter_conjunction":"And"          // Filter behavior (details follow)
>             },
>             {
>                 "key":"zJSb",
>                 "is_required":false,
>                 "description":"",
>                 "filters":[],
>                 "filter_conjunction":"And"
>             },
>             {
>                 "key":"xIy2",
>                 "is_required":false,
>                 "description":"",
>                 "filters":[],
>                 "filter_conjunction":"And"
>             }
>         ],
>         "table_id":"0000",                          // ID of the table
>         "remarkOption":{                            // A notice at the bottom
>             "isRemarkContentShow":false,              
>             "remarkContent":""
>             },
>         "notification_config":{                     // If notification will be sent  
>             "is_send_notification":false,
>             "notification_selected_users":[]
>             },
>         "top_remark_option":{                       // A notice at the top  
>             "is_top_remark_content_show":false,
>             "top_remark_content":""
>             },
>         "success_message_option":{                  // A message after submission
>             "is_success_message_show":true,
>             "success_message":"Thanks!"
>             },
>         "success_redirect_option":{                 // A redirect URL after submission  
>             "is_success_redirect_show":true,
>             "success_redirect":"www.google.com"
>             }
>     }
> ```


**Return Values**

JSON-object with details of the created form including sharing link. The form token is automatically generated.


**Sample Response**

> ```
> {
>     "form": {
>         "id": 72,
>         "username": "6534ce64315b4b4abfcff9e5491db296@auth.local",
>         "workspace_id": "377",
>         "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60",
>         "form_id": "1KOJ",
>         "form_config": "{\"form_name\":\"Vendor Survey\"}",
>         "token": "8ffu31e3-3c74-429f-b047-e8cf2f50bfbb",
>         "form_link": "https://cloud.seatable.io/dtable/forms/8ffu31e3-3c74-429f-b047-e8cf2f50bfbb/",
>         "share_type": "anonymous",
>         "created_at": "2020-11-11T13:34:33+00:00",
>         "submit_count": 0
>     }
> }
> ```

**Possible Errors**

400 Bad Request: The form ID is occupied:
> ```
> {
>     "error_msg": "Table form 1KOJ already exists."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the workspace or the base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found:
> ```
> {
>     "error_msg": "DTable Survey not found."
> }
> ```

## Update A Form

Change the name of a form with its token.


**URL Structure**

> **\[PUT]** api/v2.1/forms/`<token>`/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

> ```
> curl -X PUT \
> -d 'form_config={"form_name":"new name"}' \
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/forms/8ffu31e3-3c74-429f-b047-e8cf2f50bfbb/"
> ```

**Input Parameters**

**token** _\[string, required]_
> The suffix of the form link, like in https\://cloud.seatable.io/dtable/forms/`<token>`/

**form_config** _\[string, required]_
> Use form_config={"form_name":"new name"} to give your form the name "new name".



**Return Values**

JSON-object with the details of the updated form.

**Sample Response**

Seen from the response to the sample request, the name of the table has been changed to `new name`:

> ```
> {
>     "form": {
>         "id": 72,
>         "username": "6534ce64315b4b4abfcff9e5491db296@auth.local",
>         "workspace_id": "377",
>         "dtable_uuid": "5a40dd8e59b749ff84a73c9fb8a0cf60",
>         "form_id": "1KOJ",
>         "form_config": "{\"form_name\":\"new name\"}",
>         "token": "8ffu31e3-3c74-429f-b047-e8cf2f50bfbb",
>         "form_link": "https://cloud.seatable.io/dtable/forms/8ffu31e3-3c74-429f-b047-e8cf2f50bfbb/",
>         "share_type": "anonymous",
>         "created_at": "2020-11-11T13:34:33+00:00",
>         "submit_count": 0
>     }
> }
> ```
If the new name is equal to the old name, i.e. no change was made, the above details will also be returned without error message.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The given form token was not found:
> ```
> {
>     "error_msg": "Form 5f4851e3-3c74-429f-b047-e8cf2f50bfba not found."
> }
> ```



## Delete A Form

Delete a form with its token.


**URL Structure**

> **\[DELETE]** api/v2.1/forms/`<token>`/


**Request Authentication**

> User Authentication (Token)



**Sample Request**

Delete the form with the token of `d76d7428-ba53-4628-8a5b-2e090d693fbf`:

> ```
> curl -X DELETE \
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/forms/d76d7428-ba53-4628-8a5b-2e090d693fbf/"
> ```


**Input Parameters**

**token** _\[string, required]_
> The suffix of the form link, like in https\://cloud.seatable.io/dtable/forms/`<token>`/


**Return Values**

JSON-object with the result of the operation.



**Sample Response**

> ```
> {
>     "success": true
> }
> ```
This API request ensures the given form will not exist any more in the system. Therefore if a form is already deleted or does not exist, the above response will still be returned without error message.

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The given form token is invalid (This doesn't mean the form has been deleted):
> ```
> Sorry, but the requested page could not be found.
> ```


## Get An Upload Link with A Form Token

Get the upload link to a form with its token.


**URL Structure**

> **\[GET]** api/v2.1/forms/`<token>`/upload-link/



**Request Authentication**

None.

**Sample Request**

Get the upload link to the form with the token of `5ac7517a-6315-410f-ac70-a7e02593faf9`

> ```
> curl https://cloud.seatable.io/api/v2.1/forms/5ac7517a-6315-410f-ac70-a7e02593faf9/upload-link/
> ```


**Input Parameters**

**token** _\[string, required]_
> The suffix of the form link, like in https\://cloud.seatable.io/dtable/forms/`<token>`/


**Return Values**

JSON-object with the upload link and the parent path, as well as relative images and files path to the form.



**Sample Response**

> ```
> {
>     "upload_link": "https://cloud.seatable.io/seafhttp/upload-api/d3f91d16-88e9-494d-8402-78260eb82d65",
>     "parent_path": "/asset/a57b56d3-1cc5-4ebd-8a6c-a1b28ac3dbdf"
>     "img_relative_path": "forms",
>     "file_relative_path": "files/2020-12"
> }
> ```

**Possible Errors**

404 Not Found: The form was not found under the given token:
> ```
> {
>     "error_msg": "Form 8e63h5cb-78c9-4c86-abc2-54686e43ce22 not found."
> }
> ```




## List User's Forms


List all the forms created by the current user.


**URL Structure**

> **\[GET]** api/v2.1/forms/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

> ```
> curl \
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/forms/"
> ```

**Input Parameters**

None.


**Return Values**

JSON-object with the list of forms with details.


**Sample Response**

> ```
> {
>     "form_list": [
>         {
>             "id": 86,
>             "username": "1ed53263f17645c78dd3f57314051ea0@auth.local",
>             "workspace_id": 1,
>             "dtable_uuid": "c18e0ffce1ea4157ae5da32bdb36e676",
>             "form_id": "1KOJ",
>             "form_config": "{\"form_name\":\"Vendor Survey\"}",
>             "token": "95fcefb7-7d6c-4e61-a397-6871611e90a0",
>             "form_link": "https://cloud.seatable.io/dtable/forms/95fcefb7-7d6c-4e61-a397-6871611e90a0/",
>             "share_type": "anonymous",
>             "created_at": "2020-11-11T13:33:26+00:00",
>             "submit_count": 30
>         },
>         {
>             "id": 87,
>             "username": "1ed53263f17645c78dd3f57314051ea0@auth.local",
>             "workspace_id": 1,
>             "dtable_uuid": "38fd2617961f496595c9c26e201f5d47",
>             "form_id": "1884",
>             "form_config": "{\"form_name\":\"Employee Survey\"}",
>             "token": "b5c511c7-d011-46b1-9806-7027481e1d0d",
>             "form_link": "https://cloud.seatable.io/dtable/forms/b5c511c7-d011-46b1-9806-7027481e1d0d/",
>             "share_type": "shared_groups",
>             "created_at": "2020-11-18T14:53:15+00:00",
>             "submit_count": 20
>         }
>     ]
> }
> ```
If the user doesn't have any forms, an empty list will be returned without error message.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

## Share a Form to Groups

Share a form to multiple groups.


**URL Structure**

> **\[POST]** api/v2.1/forms/`<token>`/share/


**Request Authentication**

> User Authentication (Token)



**Input Parameters**

* token (suffix of the form link)
* share_type
* group_ids (if you don't know the group ids, contact your organization administrator)

**Sample Request**

Share the form with the token of `d76d7428-ba53-4628-8a5b-2e090d693fbf` to the groups with IDs of `1`, `3`, and `17`:

> ```
> curl --location --request POST \
> 'https://cloud.seatable.io/api/v2.1/forms/d76d7428-ba53-4628-8a5b-2e090d693fbf/share/' \
> --header 'Authorization: Token be531df7bdbb1a146b52c7ea7570bf262c276bb0' \
> --form 'share_type="shared_groups"' \
> --form 'group_ids="[1, 3, 17]"'
> ```


**Input Parameters**

**token** _\[string, required]_
> The suffix of the form link, like in https\://cloud.seatable.io/dtable/forms/`<token>`/

**share_type** _\[string, required]_
> To be able to share a form to a group, its `share_type` has to be `shared_groups`.

**group_ids** _\[int, multiple, required]_
> Enter at least one group ID to share the form.


**Return Values**

JSON-object with the result of the operation.


**Sample Response**
> 
> ```
> {
>    "success": true
> }
> ```

**Possible Errors**

400 Bad Request: The `share_type` was invalid:
> ```
> {
>     "error_msg": "share_type invalid."
> }
> ```

400 Bad Request: The `group_ids` was invalid:
> ```
> {
>     "error_msg": "group_ids invalid."
> }
> ```

401 Unauthorized: The auth token was invalid:
> ```
> {
>     "detail": "Invalid token"
> }
> ```

403 Forbidden: The user doesn't have access to the form:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

403 Forbidden: The user doesn't have permission to share the form to the target group:
> ```
> {
>     "error_msg": "Group 4 permission denied."
> }
> ```

404 Not Found: The form with the given token was not found:
> ```
> {
>     "error_msg": "Form 5a6f6d0a-67ff-4c20-8a85-0bd9a57a5b87 not found."
> }
> ```


## List Shared Forms

List all the shared forms the user has access to.


**URL Structure**

> **\[GET]** api/v2.1/forms/shared/



**Request Authentication**

> User Authentication (Token)


**Sample Request**

> ```
> curl \
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/forms/shared/"
> ```

**Input Parameters**

None.


**Return Values**

JSON-object with the list of shared forms and details.



**Sample Response**

> ```
> {
>     "shared_list": [
>         {
>             "id": 67,
>             "username": "1ed53263f17645c78dd3f57314051ea0@auth.local",
>             "workspace_id": 377,
>             "dtable_uuid": "2909200462364cf790aecbe649959776",
>             "form_id": "1884",
>             "form_config": "{\"form_name\":\"Employee Survey\"}",
>             "token": "8eid766e-baa8-4a75-b4ae-5dc162a62702",
>             "form_link": "https://cloud.seatable.io/dtable/forms/8eid766e-baa8-4a75-b4ae-5dc162a62702/",
>             "share_type": "shared_groups",
>             "created_at": "2020-11-18T14:53:15+00:00",
>             "submit_count": 30,
>             "group_name": "test group",
>             "group_id": 49
>         },
>         {
>             "id": 86,
>             "username": "1ed53263f17645c78dd3f57314051ea0@auth.local",
>             "workspace_id": 377,
>             "dtable_uuid": "03d8b71c84c74a16b31494c886dc170b",
>             "form_id": "1KOJ",
>             "form_config": "{\"form_name\":\"Vendor Survey\"}",
>             "token": "8e63h5cb-78c9-4c86-abc2-54686e43ce21",
>             "form_link": "https://cloud.seatable.io/dtable/forms/8e63h5cb-78c9-4c86-abc2-54686e43ce21/",
>             "share_type": "shared_groups",
>             "created_at": "2020-11-11T13:33:26+00:00",
>             "submit_count": 20,
>             "group_name": "Datamate3",
>             "group_id": 62
>         }
>     ]
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token was invalid:
> ```
> {
>     "detail": "Invalid token"
> }
> ```


