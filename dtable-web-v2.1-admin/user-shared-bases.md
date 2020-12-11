# User shared bases

## List Bases Shared to A User

List all the bases shared to a certain user with the user's ID (`<email>`).

**URL Structure**

> **\[GET]** /api/v2.1/admin/users/`<email>`/shared-dtables/


**Request Authentication**

> Admin Authentication (Token)


**Sample Request**

List 1 base that is shared to the user with ID `9f11ca9949b946a3b2pad55db5de1d23@auth.local`:

>```
>curl --request GET \
>--header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e' \
>'https://cloud.seatable.io/api/v2.1/admin/users/9f11ca9949b946a3b2pad55db5de1d23@auth.local/shared-dtables/?page=1&per_page=1' 
>```

**Input Parameters**

**email** _\[string, required]_
> The internal ID (`<email>`) of the requested user, ends with `@auth.local`.

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned base list.

**per_page** _\[int, optional, 25 by default]_
> Number of bases displayed on each page.


**Return Values**

JSON-object with the list of bases.


**Sample Response (200)**

The response from the sample request lists 1 base that is shared to the user, with details of the base including the ID of the `from_user`, the returned `"count"` value indicates there are 3 bases shared to this user in total:
>```
>{
>    "dtable_list": [
>        {
>            "id": 312,
>            "workspace_id": 179,
>            "uuid": "fa282c65-9d94-4f97-b6fe-8b5509b5aa87",
>            "name": "old",
>            "creator": "Max Teamleiter",
>            "modifier": "Max Teamleiter",
>            "created_at": "2020-11-06T09:54:01+00:00",
>            "updated_at": "2020-11-06T09:54:01+00:00",
>            "color": null,
>            "text_color": null,
>            "icon": null,
>            "rows_count": 0,
>            "from_user": "26815cfaf1154efba163f92359f4e580@auth.local",
>            "from_user_name": "Max Teamleiter"
>        }
>    ],
>    "count": 3
>}
>```
If the user was not found, an empty list will be returned without error message.

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
