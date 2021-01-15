# Seafile connectors

## DTable file save to seafile task

**POST** /api/v2.1/seafile-connectors/\<dtable-uuid>/file-transfer-task/

**Request parameters**

* **files_map：**Content type of file_list must be `application/json` and passed through POST request's body.
* **parent_dir: **the path which you will upload file in, default / if not set
* **relative_path：**optional，sub-folder of "parent_dir", if this sub-folder does not exist, Seafile will create it recursively. When you upload a folder, you should set this parameter to the uploaded folder's name.
* **replace：**whether to overwrite file when it already exists. 1 for replace, 0 for not replace. If existing file is not replaced, the uploaded file will be renamed to the form "filename (1).txt". default false if not set


```
{
    "files_map": {
        "file1": "filename1",
        "file2": "filename2"
    },
    "relative_path":"my_repo_2",
	"replace":0,
	"parent_dir":"my_repo"
}

```

**Note: **the key and value of the dict_like 'files_map' represent the original file name saved in seatable and custom name by which will be saved into seafile respectively, if you want to use the same name as seatable, just set the value "" as bellow

```
{
    "files_map": {
        "file1": "",
        "file2": ""
    },
    .....
}

```

---

**Sample request**

```
curl -X POST https://cloud.seatable.io/api/v2.1/seafile-connectors/3a9d826678774355bb7abb9e2ad67f09/file-transfer-task/ -H 'Authorization: Token 9308058de7056a5213d55831e184eb443c1936b4' -H 'Content-Type: application/json' -d '{
"files_map":{"files/2020-12/file_1.txt": "a.txt","files/2020-12/file_2.txt": "b.txt","files/2020-12/file_3.txt": "c.txt"},"relative_path":"my_repo_2","replace":0,"parent_dir":"my-repo"}'

```

**Sample response**

```none
{"task_id": "1608887738065"}

```


