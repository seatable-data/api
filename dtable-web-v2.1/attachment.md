# Attachment

## Get Base Attachment Upload Link

Get the attachment upload link to a base.


**URL Structure**

> **\[GET]** /api/v2.1/workspace/`<workspace_id>`/dtable-asset-upload-link/?name=`<name>`



**Request Authentication**

> User Authentication (Token)



**Sample Request**

Get the attachment upload link to the base named Merchandise in the workspace 1:

> ```
> curl \
> -H 'Authorization: Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; indent=4' \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable-asset-upload-link/?name=Merchandise"
> ```


**Input Parameters**

**workspace_id** _\[numeric, required]_
> The ID of the workspace where the target base is stored.

**name** _\[string, required]_
> The name of the target base.


**Return Values**

JSON-object with upload link, parent path, images / files relative path.


**Sample Response**

>```
>{
>    "upload_link": "https://cloud.seatable.io/seafhttp/upload-api/5d2b06ba-ec8d-4efb-a62e-3ae6ac84a67c",
>    "parent_path": "/asset/o09eab5d-a796-4ef5-909d-b491c9a056a0",
>    "img_relative_path": "images/2020-11",
>    "file_relative_path": "files/2020-11"
>}
>```

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


404 Not Found: The base was not found (probably because of a wrong name):
> ```
> {
>     "error_msg": "dtable Merchan not found."
> }
> ```




## List Base Asset Directories And Files

List all the assets (directories, files and images) of a base.


**URL Structure**

> **\[GET]** /api/v2.1/dtable-asset/`<dtable_uuid>`/



**Request Authentication**

> User Authentication (Token)



**Sample Request**

List the asset directories and files in the /files/2020-03 folder of the base with the `dtable_uuid` of `e76bc522-a82d-4b74-9bf1-bfb01416d090`:

> ```
> curl \
> -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; indent=4' \
> 'https://cloud.seatable.io/api/v2.1/dtable-asset/e76bc522-a82d-4b74-9bf1-bfb01416d090/?parent_dir=/files/2020-03'
> ```

**Input Parameters**

**parent_dir** _\[string, optional]_
> The path to list, `'/'` by default. Typical directory structures are:
> * For files: `/files/2020-11` where the `2020-11` stands for the time of upload.
> * For images: `/images/2020-11` where the `2020-11` stands for the time of upload.
> * If the base doesn't have file/image attachment, defining a `/files` or `/images` parameter will cause an error. Details refer to **Possible Errors**.


**Return Values**

JSON-object with the list of details of the attachments. The returned `"is_file"` indicates if the object is a file (`true`) or a directory (`false`).


**Sample Response**

The two files in the `files/2020-03` folder are listed in the response to the sample request:

> ```
> {
>     "dirent_list": [
>         {
>             "is_file": true,
>             "obj_name": "fb_2018-03-01.csv",
>             "file_size": 1201,
>             "last_update": "2020-03-02T03:06:16+00:00"
>         },
>         {
>             "is_file": true,
>             "obj_name": "2018-05-15.csv",
>             "file_size": 133,
>             "last_update": "2020-03-02T03:05:08+00:00"
>         }
>     ]
> }
> ```

**Possible Errors**

400 Bad Request: The directory defined in the request doesn't exist (probably because the base doesn't have file or image attachment in this directory):
> ```
> {
>     "error_msg": "parent_dir is invalid."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the given base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ``` 

404 Not Found: The base was not found with the given `dtable_uuid`:
> ```
> {
>     "error_msg": "Table 1234ab5d-a796-4ef5-909d-b491c9a056a1 not found."
> }
> ```


## Delete Asset of A Base

Delete certain asset (a directory, a file or an image) of a base.


**URL Structure**

> **\[DELETE]** /api/v2.1/dtable-asset/`<dtable_uuid>`/



**Request Authentication**

> User Authentication (Token)


**Sample Request**

Delete the directory `files/2020-03` in the base with `dtable_uuid` of `2e1fb433-836c-4a14-9d94-80d3ce7cfeac`:

> ```
> curl -X DELETE \
> -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; indent=4' \
> 'https://cloud.seatable.io/api/v2.1/dtable-asset/2e1fb433-836c-4a14-9d94-80d3ce7cfeac/?parent_path=/&name=files/2020-03'
> ```



**Input Parameters**

**name** _\[string, required]_
> Name of the directory, the file or the image.

**parent_path** _\[string, required]_
> The path to the directory, the file or the image.



**Return Values**

JSON-object with the result of the operation.

**Sample Response**

The response to the sample request indicates that the named asset has been deleted.

> ```
> {
>     "success": true
> }
> ```
This API request ensures the given asset won't exist after the request. Hence, if the named asset doesn't exist, the above response will still be sent without error message.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the given base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ``` 

404 Not Found: The base was not found with the given `dtable_uuid`:
> ```
> {
>     "error_msg": "Table 1234ab5d-a796-4ef5-909d-b491c9a056a1 not found."
> }
> ```

## Rotate Image

Use this API request to rotate an image attached to a base.


**URL Structure**

> **\[POST]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<dtable_name>`/rotate-image/



**Request Authentication**

> User Authentication (Token)



**Sample Request**

In the base `merchandise` in workspace "`1`, rotate the image `sample.png` under the path `images/2020-03` for 90 degrees counterclockwise:

> ```
> curl -X POST \
> -H 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> -H 'Accept: application/json; indent=4' \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/dtable/merchandise/rotate-image/' \
> -F 'angle=90' \
> -F 'path=images/2020-03/sample.png'
> ```

**Input Parameters**

**path** _\[string, required]_
> The image path, normally in the format like `images/2020-03` where `2020-03` is the upload time.

**angle** _\[numeric(`90`, `180`, or `270`), required]_ 
> The rotating angle, choose between `90`, `180` and `270` to rotate the image counterclockwise. Any other value would trigger an error. See **Possible Errors**.


**Return Values**

JSON-object with the result of the operation.


**Sample Response**

> ```
> {
>     "success": true
> }
> ```


**Possible Errors**

400 Bad Request: The value of angel was not one of 90, 180 and 270:
> ```
> {
>     "error_msg": "angle is invalid."
> }
> ```

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the given base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ``` 

404 Not Found: The given path or file name is wrong:
> ```
> {
>     "error_msg": "Picture images/2020-11/ample.jpg not found."
> }
> ```



