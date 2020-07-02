# DTable Snapshot

## Restore DTable Snapshot

**POST** /api/v2.1/workspace/:workspace_id/dtable/:table_name/snapshots/:commit_id/restore/

**Request Params**:

* **snapshot_name**: the name of new dtable which is from restoring snapshot, required

**Sample Request**

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/workspace/107/dtable/for-add/snapshots/aaeea690cfddb542627d0223426ba0840c03c7de/restore/' \
--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
--form 'snapshot_name=for-add-restore-4'

```

**Sample Response**

```
{
    "dtable": {
        "id": 353,
        "workspace_id": 107,
        "uuid": "016cdc8b-ecbb-4c03-8c9a-5ecb4d744230",
        "name": "for-add-restore-4",
        "creator": "admin",
        "modifier": "admin",
        "created_at": "2020-06-22T07:25:38+00:00",
        "updated_at": "2020-06-22T07:25:38+00:00"
    }
}

```


