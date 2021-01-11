# Organization
## Get an Organization

Get the basic infos of your organization.


**URL Structure**

> **\[GET]** /api/v2.1/organizations/`<org_id>`/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

> ```
> curl --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/organizations/23/' 
> ```

**Input Parameters**

**org_id** _\[int, required]_
> The ID of the queried organization.


**Return Values**

JSON-object with the basic info of the organization.



**Sample Response**

> ```
> {
>     "org_id": 23,
>     "org_name": "Sales Team"
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: You probably queried an organization which you are not in:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```


## Migrate User Self to An Organization

Sometimes, personal accounts can be registered without joining any organization. To migrate to an organization and become a team account user, you can use this API request.


**URL Structure**

> **\[POST]** /api/v2.1/user/migrate-org/


**Request Authentication**

> User Authentication (Token)





**Sample Request**

Migrate your personal account to the organization with the ID of 23:
> ```
> curl --request POST \
> --header 'Authorization: Token c20d7a808581d3a0c267dc745e5edce6b9d44d89' \
> 'https://cloud.seatable.io/api/v2.1/user/migrate-org/' \
> --form 'org_id=23'
> ```


**Input Parameters**

**org_id** _\[int, required]_
> The ID of the target organization.


**Return Values**

JSON-object with the result of the operation.


**Sample Response**
> ```
> {
>     "success": true
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```