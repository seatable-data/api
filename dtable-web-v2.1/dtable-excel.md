# Export to Excel

## Export A Table to Excel

Use this request to export one of the tables in a base to Excel. If there are multiple views in the table, you can choose which view to export so as to decide which rows to export.


**URL Structure**

> **\[GET]** api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/export-excel/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

Export the `Table` in the base `Test` in workspace `1` with its default view to Excel:

> ```
> curl \
> -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" \
> http://cloud.seatable.io/api/v2.1/workspace/1/dtable/Test/export-excel/?table_name=Table1
> ```

**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where your base is

**name** _\[string, required]_
> The name of the base

**table_name** _\[string, required]_
> The name of the table which you are going to export

**view_name** _\[string, optional]_
> The name of the view you are going to export. If not given, all the rows in the default view will be exported.


**Return Values**

.xlsx file.


**Sample Response**

An .xlsx file will be downloaded.


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

404 Not Found: The table or view name was not found:
> ```
> {
>     "error_msg": "Table Projects or View Bigview not found."
> }
> ```