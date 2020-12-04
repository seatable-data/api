# External Links

## List All External Links

List all the external links generated in the system.

**URL Structure**

> **\[GET]** /api/v2.1/admin/dtables/


**Request Authentication**

> Admin Authentication (Token)


**Sample request**

List 3 external links in the current system:

> ```
> curl \
> -H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
> -H 'Accept: application/json; indent=4' \
> "https://cloud.seatable.io/api/v2.1/admin/external-links/?page=1&per_page=3"
> 
> ```


**Input Parameters**

**page** _\[numeric, optional, 1 by default]_ 
> Page number of the returned link list.

**per_page** _\[numeric, optional, 25 by default]_
> Number of links displayed on each page.



**Sample response**

Response from the sample request shows Page 1 with 3 external links and their detailed infos. The returned "has_next_page" value indicates that there are more external links in the system:

>```
>{
>    "has_next_page": true,
>    "external_link_list": [
>        {
>            "id": 1,
>            "from_dtable": "test",
>            "creator": "f926c9c169fd48f9ba1861371cf487f1@auth.local",
>            "creator_name": "Susanne Sommer",
>            "token": "ca247ca407eb45f2dd9d",
>            "permission": "r",
>            "create_at": "2020-07-03T11:38:35+00:00",
>            "view_cnt": 2
>        },
>        {
>            "id": 2,
>            "from_dtable": "test",
>            "creator": "f926c9c169fd48f9ba8273771hf485f1@auth.local",
>            "creator_name": "Hans Zimmer",
>            "token": "jzgjjgj",
>            "permission": "r",
>            "create_at": "2020-07-03T11:39:05+00:00",
>            "view_cnt": 0
>        },
>        {
>            "id": 7,
>            "from_dtable": "Bewerbermanagement",
>            "creator": "bbdd1b026e6546d4ab89985a2299945f@auth.local",
>            "creator_name": "da Vinci",
>            "token": "4dcd424d3ddd4d82bd15",
>            "permission": "r",
>            "create_at": "2020-07-10T11:07:37+00:00",
>            "view_cnt": 0
>        }
>    ]
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

## Delete An External Link By Token

An external link can be deleted by its token. 

**URL Structure**

> **\[DELETE]** /api/v2.1/admin/dtables/<token>/

**Request Authentication**

> Admin Authentication (Token)

**Sample Request**

Delete the external link with the token acbdef3e30a3404084b6:

>```
>curl -X DELETE \
>-H 'Authorization:Token 5f971000df0d6f35ed7c59580766329a5b37a6df' \
>-H 'Accept: application/json; indent=4' \
>"https://cloud.seatable.io/api/v2.1/admin/external-links/acbdef3e30a3404084b6/"
>
>```

**Input Parameters**

**token** _\[string, required]_
> As an external link is generated, its token is used as the suffix to its link: https\://cloud.seatable.io/dtable/external-links/<token>/

**Sample Response**

Response from the sample request indicates the successful deletion of the external link with the given token:

>```
>{
>    "success": true
>}
>```
This API call ensures that the external link with the given token will not exist in the system after the request, therefore when an invalid token is given, the response will also indicate success.

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


