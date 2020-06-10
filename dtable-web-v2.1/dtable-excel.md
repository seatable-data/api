# Export to Excel/Import from Excel

## Export Rows of a Subtable to Excel

**GET** api/v2.1/workspace/\<workspace_id>/dtable/\<name>/export-excel/

**Request parameters**

* table_name, the name of the sub-table in the dtable
* view_name, optional, if not given, rows of Default View will be exported

**Sample request**

```
curl -H "Authorization: Token f6c14812c5403b361b7f8cd61ac8d969cbca63a0" http://127.0.0.1:8001/api/v2.1/workspace/1/dtable/export-excel/?table_name=t1&subtable_name=Table1

```

**Sample response**

 .xlsx file
