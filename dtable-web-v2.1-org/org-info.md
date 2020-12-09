# Organization Administration: Information

## Update Organization Information

Update the organization's basic information.


**URL Structure**

> **\[PUT]** /api/v2.1/org/admin/info/


**Request Authentication**

> Org-admin Authentication (Token)

**Sample Request**

Change the name of the organization into "SeaTable":

> ```
> curl -X PUT \
> -H 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
> -H 'Content-Type: multipart/form-data' \
> 'https://cloud.seatable.io/api/v2.1/org/admin/info/' \
> -F 'new_org_name=SeaTable'
> ```


**Input Parameters**

**new_org_name**  _\[string, optional]_
> New name of the organization.


**Return Values**

JSON-object with the result of the operation.


**Sample Response**

The response indicates that the changes were successful:
> ```
> {
>     "success": true
> }
> ```
The same response will be also returned even if the `new_org_name` is identical to the current name, i.e. nothing was changed.

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have org-admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```


