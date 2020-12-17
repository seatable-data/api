# Base Star

You can add a star to a base, so as to make it "Favorite". Adding a star to a base will:

* Put on a star sign besides the base's name in the base library;
* List this base in the "Favorites" in the base library.

## List Starred (Favorite) Bases

List all the "favorite" bases which have stars.


**URL Structure**

> **\[GET]** /api/v2.1/starred-dtables/


**Request Authentication**

> User Authentication (Token)


**Sample Request**

> ```
> curl --request GET \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/starred-dtables/' 
> ```


**Input Parameters**

None.


**Return Values**

JSON-object with the list of details of the starred bases.


**Sample Response (200)**

The response lists off two starred bases with their details:

> ```
> {
>     "user_starred_dtable_list": [
>         {
>             "id": 355,
>             "workspace_id": 3277,
>             "uuid": "9fd8b71c-84c7-4a16-b314-94c886dc170b",
>             "name": "Surveys",
>             "creator": "Robert Teamplayer",
>             "modifier": "Robert Teamplayer",
>             "created_at": "2020-11-17T15:39:26+00:00",
>             "updated_at": "2020-12-14T14:26:29+00:00",
>             "color": null,
>             "text_color": null,
>             "icon": null
>         },
>         {
>             "id": 375,
>             "workspace_id": 1327,
>             "uuid": "v0543a04-39b7-4ce7-aa08-7fe1f4dad0b6",
>             "name": "Database",
>             "creator": "Robert Teamplayer",
>             "modifier": "Robert Teamplayer",
>             "created_at": "2020-11-19T14:43:24+00:00",
>             "updated_at": "2020-11-19T14:43:24+00:00",
>             "color": "#7626FD",
>             "text_color": "#7626FD",
>             "icon": "icon-software-test-management"
>         }
>     ]
> }
> ```
If the user doesn't have any starred base, an empty list will be returned without error message.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```



## Add A Star to A Base

Give a star to a base, to make it a "favorite" base.


**URL Structure**

> **\[POST]** /api/v2.1/starred-dtables/


**Request Authentication**

> User Authentication**


**Sample Request**

> ```
> curl --request POST \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/starred-dtables/' \
> --form 'dtable_uuid=00390415b6dc416a8f2a70a3a1356a18'
> ```



**Input Parameters**

**dtable_uuid** _\[int, required]_
> The ID of the base.


**Return Values**

JSON-object with the result of the operation.



**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```
This request makes sure there's a star on the base. So when you repeat this operation, you'll always get the "success" response.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the requested base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found with the given ID:
> ```
> {
>     "error_msg": "Table not found."
> }
> ```

## Delete Star of A Base

Remove the star from a favorite base.

**URL Structure**

> **\[DELETE]** /api/v2.1/starred-dtables/?dtable_uuid=`<dtable_uuid>`



**Sample Request**

> ```
> curl --request DELETE \
> --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
> 'https://cloud.seatable.io/api/v2.1/starred-dtables/?dtable_uuid=00390415b6dc416a8f2a70a3a1356a18'
> ```


**Input Parameters**

**dtable_uuid** _\[int, required]_
> The ID of the base.


**Return Values**

JSON-object with the result of the operation.



**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```
This request makes sure the base is not a favorite any more. So when you repeat this operation, or do it to a base that's not a favorite, you'll always get the "success" response.



**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have access to the requested base:
> ```
> {
>     "error_msg": "Permission denied."
> }
> ```

404 Not Found: The base was not found with the given ID:
> ```
> {
>     "error_msg": "Table not found."
> }
> ```

