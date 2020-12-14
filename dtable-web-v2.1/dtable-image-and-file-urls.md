# Images and Files URLs

This article introduces how to formulate the external URLs to images and files attached to your SeaTable bases.

## Images URLs

### Normal Images URLs

URLs to the full sized images attached to your bases.

**URL Structure**


> /workspace/`<workspace_id>`/asset/`<dtable_uuid>`/`<path>`


**Example URL**

The URL for the image `images/2020-11/sample.jpg` in the base with the given `dtable_uuid` and `workspace` ID:
> ```
> https://cloud.seatable.io/workspace/1/asset/63c21c34-f480-46c0-9e2e-a83f4919b80d/images/2020-12/sample.jpg
> ```



**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**dtable_uuid** _\[string, required]_
> The ID of the base where the asset is stored.

**path** _\[string, required]_
> The path and file name to the target file/image. Use relative path like `images/2020-11/sample.jpg` where `2020-11` also represents the uploading date.


**Return Values**

File or image download.

**Possible Errors**

The file doesn't exist, or the path is wrong:
> ```
> Asset file does not exist.
> ```

The user doesn't have access to the base:
> ```
> Permission denied.
> ```

### Image Thumbnail URL

URLs to a customized size (e.g. thumbnail) of the images attached to your bases.

**URL Structure**

> /thumbnail/workspace/`<workspace_id>`/asset/`<dtable_id>`/`<path>`?size=`<size>`


**Example URL**

The URL for the image `images/2020-11/sample.jpg` in the base with the given `dtable_uuid` and `workspace` ID as thumbnail with the size of 300 pixels:
> ```
> https://cloud.seatable.io/thumbnail/workspace/1/asset/63c21c34-f480-46c0-9e2e-a83f4919b80d/images/2020-12/sample.jpg?size=300
> ```

**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**dtable_uuid** _\[string, required]_
> The ID of the base where the asset is stored.

**path** _\[string, required]_
> The path and file name to the target file/image. Use relative path like `images/2020-11/sample.jpg` where `2020-11` also represents the uploading date.

**size** _\[int, required]_
> The maximum size (length or width) of the thumbnail to be displayed. If the image is smaller than the `size`, the original image size will be displayed.


**Return Values**

Image with the size smaller than or equal to the given size.

**Possible Errors**

The user doesn't have access to the base:
> ```
> Permission denied.
> ```

### Form upload image url

```
/dtable/forms/<form_token>/asset/<img_name>?token=<form_id>

```

Example

```
https://cloud.seatable.io/dtable/forms/4c32cb1b-acb0-4715-8996-ecaf115ddfc0/asset/container-life-cycle.png?token=rmZ9

```

## Files

### Preview

Open a preview of the target file in a base.


**URL Structure**

> /workspace/`<workspace_id>`/asset-preview/`<dtable_uuid>`/`<path>` 



**URL Example**

Open a preview of the `sample.pdf` file in the base with the following `dtable_uuid` in the workspace `1`:

> ```
> https://cloud.seatable.io/workspace/1/asset-preview/63c21c34-f480-46c0-9e2e-a83f4919b80d/files/2020-11/sample.pdf
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**dtable_uuid** _\[string, required]_
> The ID of the base where the asset is stored.

**path** _\[string, required]_
> The path and file name to the target file. Use relative path like `files/2020-11/sample.jpg` where `2020-11` also represents the uploading date.


**Return Values**

HTML5 reader of the file.

**Sample Response**

A website with the built-in preview of the targeted file.


**Possible Errors**

The file doesn't exist, or the path is wrong:
> ```
> Asset file does not exist.
> ```

The user doesn't have access to the base:
> ```
> Permission denied.
> ```


### Download

Download the attached file directly without previewing.


**URL Structure**

> /workspace/`<workspace_id>`/asset/`<dtable_id>`/`<path>`?dl=1


**URL Example**

> ```
> https://cloud.seatable.io/workspace/1/asset/63c21c34-f480-46c0-9e2e-a83f4919b80d/files/2020-11/sample.pdf?dl=1
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**dtable_uuid** _\[string, required]_
> The ID of the base where the asset is stored.

**path** _\[string, required]_
> The path and file name to the target file. Use relative path like `files/2020-11/sample.jpg` where `2020-11` also represents the uploading date.

**dl** _\[int, optional]_
> Some browsers will open PDF files in built-in readers. To void this and proceed to the download directly, set `?dl=1` as suffix to the download URL.


**Possible Errors**

If the user is not logged in, the login page will prompt.

