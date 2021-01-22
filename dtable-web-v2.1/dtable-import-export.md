# The Import and Export of Bases

## Import A Base From \*.dtable File

Bases in SeaTable can by easily exported as \*.dtable file and imported in the same library or in another library.

**URL Structure**

> **\[POST]** /api/v2.1/workspace/`<workspace_id>`/import-dtable/

**Request Authentication**

> User Authentication (Token)

**Sample Request**

Import the `test.dtable` file from local path `@/home/karlheinz/Downloads` to workspace `1`:

> ```
> curl --location --request POST \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/import-dtable/' \
> --header 'Authorization: Token 0303f89b3607fb86039fdffcf1be6383797b437f' \
> --header 'Content-Type: multipart/form-data' \
> --form 'dtable=@"/home/karlheinz/Downloads/test.dtable"'
>
> ```

**Input Parameters**

**workspace_id** _\[int, required]_

> The ID of the workspace where your base is stored.

**dtable** _\[file, required]_

> \*.dtable is a zip file containing the data in your base. 

**Return Values**

JSON-object with the import task's ID and the details of the imported base. The ID and the UUID are automatically generated.

**Sample Response (200)**

The response returned the import task's ID and the details of the imported base:

> ```
> {
>     "task_id": "1607961118337",
>     "table": {
>         "id": 394,
>         "workspace_id": 1,
>         "uuid": "8enb662d-5ce7-4668-a4ab-9f97f40c11c2",
>         "name": "test",
>         "creator": "Robert Teamplayer",
>         "modifier": "Robert Teamplayer",
>         "created_at": "2020-11-14T15:51:58+00:00",
>         "updated_at": "2020-11-14T15:51:58+00:00",
>         "color": null,
>         "text_color": null,
>         "icon": null
>     }
> }
>
> ```

**Possible Errors**

400 Bad Request: The file path is not correct, or the file is not valid:

> ```
> {
>     "error_msg": "dtable invalid."
> }
>
> ```

400 Bad Request: The base name is not unique in the library:

> ```
> {
>     "error_msg": "Table test already exists."
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

403 Forbidden: The user doesn't have access to the workspace or the base:

> ```
> {
>     "error_msg": "Permission denied."
> }
>
> ```

## Import A Base From \*.csv File

When creating a new base, you have the option to import it from a \*.csv file.

**URL Structure**

> **\[POST]** /api/v2.1/workspace/`<workspace_id>`/import-dtable/

**Request Authentication**

> User Authentication (Token)

**Sample Request**

Import the `testcsv.csv` file from local path `@/home/karlheinz/Downloads` to workspace `1`:

> ```
> curl --location --request POST \
> 'https://cloud.seatable.io/api/v2.1/workspace/1/import-dtable/' \
> --header 'Authorization: Token 0303f89b3607fb86039fdffcf1be6383797b437f' \
> --header 'Content-Type: multipart/form-data' \
> --form 'dtable=@"/home/karlheinz/Downloads/testcsv.csv"'
>
> ```

**Input Parameters**

**workspace_id** _\[int, required]_

> The ID of the workspace where your base is stored.

**dtable** _\[file, required]_

> The path to the .csv file in your local drive. 

**Return Values**

JSON-object with the import task's ID and the details of the imported base. The ID and the UUID are automatically generated.

**Sample Response (200)**

The response returned the import task's ID and the details of the imported base:

> ```
> {
>     "task_id": "1607961118338",
>     "table": {
>         "id": 395,
>         "workspace_id": 1,
>         "uuid": "e6e22f5b-8d44-41d2-8c64-455296a6f7f8",
>         "name": "testcsv",
>         "creator": "Robert Teamplayer",
>         "modifier": "Robert Teamplayer",
>         "created_at": "2020-11-14T15:51:58+00:00",
>         "updated_at": "2020-11-14T15:51:58+00:00",
>         "color": null,
>         "text_color": null,
>         "icon": null
>     }
> }
>
> ```

**Possible Errors**

400 Bad Request: The file path is not correct, or the file is not valid:

> ```
> {
>     "error_msg": "dtable invalid."
> }
>
> ```

400 Bad Request: The base name is not unique in the library:

> ```
> {
>     "error_msg": "Table test already exists."
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

403 Forbidden: The user doesn't have access to the workspace or the base:

> ```
> {
>     "error_msg": "Permission denied."
> }
>
> ```

## Export A Base as \*.dtable File

A base in SeaTable can be exported as a .dtable file, which is a zip file of the content of the base. This request wraps the base in a zipped .datable file and returns a task ID. To download the zipped file, refer to [Download the Exported File](https://docs.seatable.io/published/seatable-api/dtable-web-v2.1/dtable-import-export.md#user-content-Get%20Export%20Content).

**URL Structure**

> **\[GET]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/export-dtable/

**Request Authentication**

> User Authentication (Token)

**Sample Request**

Export and download the base `test` from the workspace `1` as .dtable file:

> ```
> curl \
> -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" \
> https://cloud.seatable.io/api/v2.1/workspace/1/dtable/test/export-dtable/
>
> ```

**Input Parameters**

**workspace_id** _\[int, required]_

> The ID of the workspace where the base is stored.

**name** _\[string, required]_

> The name of the base to be exported.

**Return Value**

JSON-object with the zipping task ID and the details of the exported base.

**Sample Response (200)**

A `task_id` and the details of the exported base are returned. Download the file with the `task_id` with the URL provided in [Download the Exported File](https://docs.seatable.io/published/seatable-api/dtable-web-v2.1/dtable-import-export.md#user-content-Get%20Export%20Content).

> ```
> {
>     "task_id": "16079624690666",
>     "table": {
>         "id": 396,
>         "workspace_id": 1,
>         "uuid": "e6e22f5b-8d44-41d2-8c64-455296a6f7f8",
>         "name": "test",
>         "creator": "Robert Teamplayer",
>         "modifier": "Robert Teamplayer",
>         "created_at": "2020-11-14T16:00:24+00:00",
>         "updated_at": "2020-11-14T16:00:24+00:00",
>         "color": null,
>         "text_color": null,
>         "icon": null
>     }
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

403 Forbidden: The user doesn't have access to the workspace or the base:

> ```
> {
>     "error_msg": "Permission denied."
> }
>
> ```

404 Not Found: The base was not found:

> ```
> {
>     "error_msg": "DTable test not found."
> }
>
> ```

## Query Import/Export Status

Sometimes a base is so large, that importing/exporting takes some time. Use the returned `task_id` to query if this task has been finished.

**URL Structure**

> **\[GET]** /api/v2.1/dtable-io-status/

**Request Authentication**

> User Authentication (Token)

**Sample Request**

Query if the task with ID `1582970303923` has been finished or not:

> ```
> curl \
> -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" \
> https://cloud.seatable.io/api/v2.1/dtable-io-status/?task_id=1582970303923
>
> ```

**Input Parameters**

**task_id** _\[int, required]_

> Automatically generated and returned ID of the importing/exporting task.

**Return Value**

JSON-object with the result of the query.

**Sample Response (200)**

The response indicates that the task has been finished:

> ```
> {
>     "is_finished": true
> }
>
> ```

**Possible Errors**

400 Bad Request: The `task_id` was invalid:

> ```
> {
>     "error_msg": "task_id invalid."
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

## Download the Exported File

With the automatically generated task ID when exporting a file, use this API request to download the zipped .dtable base file.

**URL Structure**

> **\[GET]** /dtable-export-content/

**Request Authentication**

> User Authentication (Token)

**Sample Request**

Download the exported base file with the task ID and base UUID as follows:

> ```
> curl \
> -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" \
> https://cloud.seatable.io/dtable-export-content/?task_id=1582970912441&dtable_uuid=d09b6bcc-b6e5-4b8c-b9e2-c4329a8af482
>
> ```

**Input Parameters**

**task_id** _\[int, required]_

> Automatically generated and returned ID of the importing/exporting task.

**dtable_uuid** _\[int, required]_

> Automatically generated base identification code when creating or importing a new base.

**Return Values**

Zip file with .dtable suffix.

**Sample Response (200)**

A .dtable file with the same name as the base is downloaded.

## Cancel Task

With the automatically generated task ID, an ongoing task can be cancelled.

**URL Structure**

> **\[DELETE]** /api/v2.1/dtable-io-status/

**Request Authentication**

> User Authentication (Token)

**Sample Request (200)**

Cancel the ongoing exporting process with the following `task_id` and `dtable_uuid`:

> ```
> curl -X DELETE \
> -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" \
> https://cloud.seatable.io/api/v2.1/dtable-export-content/?task_id=1582970912441&dtable_uuid=d09b6bcc-b6e5-4b8c-b9e2-c4329a8af482&task_type=export
>
> ```

**Input Parameters**

**task_id** _\[int, required]_

> Automatically generated and returned ID of the importing/exporting task.

**dtable_uuid** _\[int, required]_

> Automatically generated base identification code when creating or importing a new base.

**task_type** _\[string(__`export`__ or __`import`__), required]_

> Announce the ongoing type of task to be cancelled.

**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

> ```
> {
>    "success": true
> }
>
> ```


