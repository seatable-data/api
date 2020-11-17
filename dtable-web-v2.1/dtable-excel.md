# Export to Excel/Import from Excel

## Export Rows of a Table to Excel

**GET** api/v2.1/workspace/\<workspace_id>/dtable/\<name>/export-excel/

**Request parameters**

* workspace_id, the ID of the workspace where your base is
* name, the name of the base
* table_name, the name of the table in the base
* view_name, optional, if not given, rows of Default View will be exported

**Sample request**

```
curl -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" http://127.0.0.1:8001/api/v2.1/workspace/1/dtable/t1/export-excel/?table_name=Table1

```

**Sample response**

 .xlsx file
