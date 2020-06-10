# Image and file URLs

## Images

### Normal image url

```
/workspace/<workspace_id>/asset/<dtable_id>/<path>

```

Example

```
http://127.0.0.1:8000/workspace/36/asset/63c21c34-f480-46c0-9e2e-a83f4919b80d/images/7945c2fd9b3098c5066fa9c1e5f796e1.jpg

```

### Image thumbnail url

```
/thumbnail/workspace/<workspace_id>/asset/<dtable_id>/<path>?size=xxx

```

Example

```
http://127.0.0.1:8000/thumbnail/workspace/36/asset/63c21c34-f480-46c0-9e2e-a83f4919b80d/images/7945c2fd9b3098c5066fa9c1e5f796e1.jpg?size=1024

```

Note: the `<path>` in thumbnail url should be same as `<path>` in normal url.

### Form upload image url

```
/dtable/forms/<form_token>/asset/<img_name>?token=<form_id>

```

Example

```
http://127.0.0.1:8000/dtable/forms/4c32cb1b-acb0-4715-8996-ecaf115ddfc0/asset/container-life-cycle.png?token=rmZ9

```

## Files

### Preview

```
/workspace/<workspace_id>/asset-preview/<dtable_id>/<path> 

```

Example

```
http://127.0.0.1:8000/workspace/36/asset-preview/63c21c34-f480-46c0-9e2e-a83f4919b80d/files/%C2%BB%C3%BA%C3%86%C3%B7%C3%88%C3%8B.pdf

```

### Download

```
/workspace/<workspace_id>/asset/<dtable_id>/<path>?dl=1

```

Example

```
http://127.0.0.1:8000/workspace/36/asset/63c21c34-f480-46c0-9e2e-a83f4919b80d/files/»úÆ÷ÈË.pdf?dl=1

```


