# Forms

## List All Forms

List all the forms in the current system.

**URL Structure**

> **\[GET]** /api/v2.1/admin/forms/


**Request Authentication**

> Admin Authentication (Token)


**Sample Request**

List the forms without inputing any parameter:

>```
>curl --request GET \
>--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
>'https://cloud.seatable.io/api/v2.1/admin/forms/' 
>```

**Input Parameters**

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned form list.

**per_page** _\[int, optional, 2 by default]_
> Number of forms displayed on each page.


**Return Values**

JSON-object with the list of forms.


**Sample Response (200)**

Response from the sample request shows the details of 2 forms by default, as the `"page"` and `"per_page"` parameters were not given in the sample request. The returned `"count"` value indicates that there are 46 forms in total:

>```
>{
>    "form_list": [
>        {
>            "id": 5,
>            "form_name": "Input",
>            "username": "Max Mustermann",
>            "dtable_name": "Financials",
>            "token": "428e84b8-c2a2-4ba2-a056-efc395e8f38b",
>            "created_at": null,
>            "submit_count": 3
>        },
>        {
>            "id": 7,
>            "form_name": "Zufriedenheitsanalyse",
>            "username": "Meng Wu",
>            "dtable_name": "Tests",
>            "token": "839697dc-588b-4a0f-92d1-86f05e64d313",
>            "created_at": null,
>            "submit_count": 0
>        }
>    ],
>    "count": 46
>}
>```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```

## Delete a Form

Delete a form with its token.

**URL Structure**

> **\[DELETE]** /api/v2.1/admin/forms/`<token>`/

**Request Authentication**

> Admin Authentication (Token)



**Sample Request**

Delete the form with the token 3f9ee7c8-7338-4ca5-b877-4df454c6ad8b:

>```
>curl --request DELETE \
>--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
>'https://cloud.seatable.io/api/v2.1/admin/forms/3f9ee7c8-7338-4ca5-b877-4df454c6ad8b/' 
>```

**Input Parameters**

**token** _\[string, required]_
> As a form is generated, its token is used as the suffix to its link. For example: https\://cloud.seatable.io/dtable/forms/`<token>`/


**Return Values**

JSON-object with the result of the operation.


**Sample Response (200)**

The form with the token given in the sample request is now deleted:
>```
>{
>    "success": true
>}
>```
This API call ensures that the form with the given token will not exist in the system after the request, therefore when an invalid token is given, the response will also indicate success.



**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```
The token here means the auth token, not the form's token.

403 Forbidden: The user doesn't have admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```


