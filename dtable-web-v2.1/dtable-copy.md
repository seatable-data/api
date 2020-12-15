# Copying Bases

## Copy A Base from A Workspace

Normally, a user can have access to multiple workspaces, e.g. the "My bases" is their own workspace, and a shared group is another workspace, etc. Use this API request to copy a base from another workspace to your own workspace, or to a workspace you have permission to write.


**URL Structure**

> **\[POST]** /api/v2.1/dtable-copy/


**Request Authentication**

> User Authentication (Token)




**Sample Request**

In this sample request, the user copies `Projects` from workspace `1` to `80`:
> ```
> curl -X POST \
> -H 'authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> https://cloud.seatable.io/api/v2.1/dtable-copy/ \
> -F src_workspace_id=1 \
> -F name=Projects \
> -F dst_workspace_id=80 
> ```


**Input Parameters**

**src_workspace_id** _\[int, required]_
> The ID of the source workspace. The user has to have access to this workspace and the source base in order to carry out this request.

**dst_workspace_id** _\[int, required]_
> The ID of the destination workspace. The user has to have write permission in the destination workspace in order to carry out this request.

**name** _\[string, required]_
> The name of the source base. The user has to have access to this base in order to carry out the copying request.



**Return Values**

JSON-object with the details of the copied base.

**Sample Response (200)**

> ```
> {
>     "dtable":{
>         "id":978,
>         "workspace_id":80,
>         "uuid":"9e214427-cddd-425a-bc11-1dcbba93ebcd",
>         "name":"Projects",
>         "creator":"Teamplayer",
>         "modifier":"Teamplayer",
>         "created_at":"2020-10-27T16:08:46+08:00",
>         "updated_at":"2020-10-27T16:08:46+08:00",
>         "color":null,
>         "text_color":null,
>         "icon":null
>     }
> }
> ```

**Possible Errors**

400 Bad Request: The given parameters are not correct:
> ```
> {
>     "error_msg": "src_workspace_id or dst_workspace_id is invalid"
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the source workspace/base, or cannot write to the destination workspace:
> ```
> {
>     "error_msg": "Permission denied"
> }
> ```

404 Not Found: The source base was not found:
> ```
> {
>     "error_msg": "dtable: Projekts not found"
> }
> ```



## Copy A Base with An External Link

When an external link is available, you can copy this base to your own workspace or to a workspace you have write permission in.


**URL Structure**

> **\[POST]** /api/v2.1/dtable-external-link/dtable-copy/


**Request Authentication**

> User Authentication (Token)



**Sample Request**

With the external link as below, copy the base to the workspace `80`:

> ```
> curl -X POST \
> -H 'authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> https://cloud.seatable.io/api/v2.1/dtable-external-link/dtable-copy/ \
> -F link='https://cloud.seatable.io/dtable/external-links/6be92845836f41febafe/' \
> -F dst_workspace_id=80
> ```


**Input Parameters**

**link** _\[string, required]_
> The external link of the source base.

**dst_workspace_id** _\[int, required]_
> The ID of the destination workspace. The user has to have write permission in this workspace.



**Return Values**

JSON-object with the details of the copied base.


**Sample Response (200)**

The details of the copied base are returned:
> ```
> {
>     "dtable":{
>         "id":978,
>         "workspace_id":80,
>         "uuid":"9e214427-cddd-425a-bc11-1dcbba93ebcd",
>         "name":"Projects",
>         "creator":"Teamleader",
>         "modifier":"Teamleader",
>         "created_at":"2020-10-27T16:08:46+08:00",
>         "updated_at":"2020-10-27T16:08:46+08:00",
>         "color":null,
>         "text_color":null,
>         "icon":null
>     }
> }
> ```

**Possible Errors**

400 Bad Request: The external link is invalid:
> ```
> {
>     "error_msg": "link is invalid."
> }
> ```

400 Bad Request: A base with the same name already exists in the destination workspace:
> ```
> {
>     "error_msg": "Table Projects already exists in this workspace."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user cannot write to the destination workspace:
> ```
> {
>     "error_msg": "Permission denied"
> }
> ```


