# Organization Administrator: Users Operations

## List All Users

List all the users in the current organization.


**URL Structure**

> **\[GET]** /api/v2.1/org/`<org_id>`/admin/users/


**Request Authentication**

> Org-admin Authentication (Token)



**Sample Request**

> ```
> curl --request GET \
> -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" \
> https://cloud.seatable.io/api/v2.1/org/12/admin/users/
> ```



**Input Parameters**

**is_staff** _\[enum(`true` or `1`, `false` or `0`), optional]_
> If `true` or `1`, will only list org-admin users. 

**page** _\[int, optional, 1 by default]_ 
> Page number of the returned user list.

**per_page** _\[int, optional, 100 by default]_
> Number of users displayed on each page.



**Return Values**

JSON-object with the list of users.


**Sample Response**

The response from the sample request lists off two users in the organization. The returned `per_page`, `page` and `page_next` values indicate that all the users in this organization are listed.

> ```
> {
> 	"user_list": [{
> 		"email": "0f57ceedc87049a2af1b2726c147c617@auth.local",
> 		"name": "Org Member",
> 		"contact_email": "org-member@example.com",
> 		"quota_usage": 0,
> 		"quota_total": -2,
> 		"last_login": "2020-05-20T07:11:51+00:00",
> 		"id": 155,
> 		"is_active": true,
> 		"ctime": "2020-04-10T09:52:41+00:00",
> 		"self_usage": 0,
> 		"quota": -2
> 		"is_org_admin": false
> 	}, 
> 	{
> 		"email": "31590xfaf1154efba122f92359f4e580@auth.local",
> 		"name": "Max Teamleader",
> 		"contact_email": "teamleader@sexample.com",
> 		"quota_usage": 0,
> 		"quota_total": -2,
> 		"last_login": "2020-11-08T15:15:16+00:00",
> 		"id": 217,
> 		"is_active": true,
> 		"ctime": "2020-11-06T09:36:39+00:00",
> 		"self_usage": 0,
> 		"quota": -2,
> 		"is_org_admin": true
> 	}],
> 	"per_page": 100,
> 	"page": 1,
> 	"page_next": false
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have org-admin permission in the requested org:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```

## Add A User

Add a new user in the organization and define email, name and password.


**URL Structure**

> **\[POST]** /api/v2.1/org/`<org_id>`/admin/users/


**Request Authentication**

> Org-admin Authentication (Token)


**Sample Request**

> ```
> curl --request POST \
> --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
> 'https://cloud.seatable.io/api/v2.1/org/23/admin/users/' 
> --form 'email=new-user@example.com' \
> --form 'name=New-user' \
> --form 'password=123456' \
> ```


**Input Parameters**

**email** _\[string,required]_ 
> This is the real email address of the user. SeaTable will save this value as `contact_email`.


**password** _\[string,required]_
> The user's password. Minimum length: 6 characters.


**name** _\[string,required]_ 
> Surname and lastname of the user.



**Return Values**

JSON-object with new user's info. The `email` (user's ID in the system) is generated automatically.



**Sample Response**

The new user is added and their `email` (ID) is generated:

> ```
> {
>     "id": 268,
>     "is_active": true,
>     "ctime": "2020-11-08T16:21:47+00:00",
>     "name": "new-user",
>     "email": "d49f768b2425487fa5d6f5b443515a87@auth.local",
>     "contact_email": "new-user@example.com",
>     "last_login": null,
>     "self_usage": 0,
>     "quota": -2
> }
> ```


**Possible Errors**

400 Bad Request: The user's email address is already registered in the system:
> ```
> {
>     "error_msg": "User new-user@example.com already exists."
> }
> ```

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




## Update User

Update the info and settings of a user.


**URL Structure**

> **\[PUT]** /api/v2.1/org/`<org_id>`/admin/users/`<email>`/


**Request Authentication**

> Org-admin Authentication (Token)


**Sample Request**

Change the name of the user with the ID (`email`) of `d49f768b2425487fa5d6f5b443515a87@auth.local`:

> ```
> curl -X PUT \
> -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" \
> https://cloud.seatable.io/api/v2.1/org/12/admin/users/d49f768b2425487fa5d6f5b443515a87@auth.local/ \
> -d "name=Old-user" \
> -d "is_active=false" \
> ```



**Request Parameters**

**name** _\[string, optional]_
> The new name of the user.

**contact_email** _\[string, optional]_
> The new contact email address of the user (currently, user's contact email address cannot be changed on cloud.seatable.io)

**is_active** _\[enum(`true` or `1`, `false` or `0`), optional]_
> Determine if the user is set as active:
> * `false` = user is deactivated and can not login
> * `true` = user is activated

**is_staff** _\[enum(`true` or `1`, `false` or `0`), optional]_
> Determine if the user is set as staff:
> * `false` = normal user
> * `true` = user becomes an org-admin
> * If user is already/not an org-admin, setting this attribute again will cause an error (see the **Possible Errors**)


**Return Values**

JSON-object with the details of the user.



**Sample Response**

The returned values confirm the change:

> ```
> {
> 	"email": "5ef77767e76345bdb72469923f2c2904@auth.local",
> 	"name": "old-user",
> 	"contact_email": "new-user@example.com",
> 	"quota_usage": 0,
> 	"quota_total": -2,
> 	"is_active": false,
> 	"id": 168,
> 	"ctime": "2020-05-20T07:35:24+00:00",
> 	"last_login": null,
> 	"self_usage": 0,
> 	"quota": -2,
> 	"email_sent": false
> }
> ```


**Possible Errors**

400 Bad Request: A user is already (or not) an org-admin:
> ```
> {
>     "error_msg": "d49f768b2425487fa5d6f5b443515a87@auth.local is already organization staff."
> }
> ```

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

## Delete User

Delete a user permanently.


**URL Structure**

> **\[DELETE]** /api/v2.1/org/`<org_id>`/admin/users/`<email>`/



**Request Authentication**

> Org-admin Authentication (Token)



**Sample Request**

Delete the user with ID `d49f768b2425487fa5d6f5b443515a87@auth.local`:

> ```
> curl -X DELETE \
> -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" \
> https://cloud.seatable.io/api/v2.1/org/12/admin/users/d49f768b2425487fa5d6f5b443515a87@auth.local/
> ```


**Input Parameters**

**email** _\[string, required]_
> The ID (not email address) of the user to be deleted.


**Return Values**

JSON-object indicating the result of the operation.



**Sample Response**

Response from the sample request indicates the successful deletion of the user:
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

403 Forbidden: The user doesn't have org-admin permission:
>```
>{
>    "detail": "You do not have permission to perform this action."
>}
>```

404 Not Found: The user's ID was wrong, or not found (already deleted):
> ```
> {
>     "error_msg": "User new-user@example.com not found."
> }
> ```

## Reset User Password

Reset the password of a user.

**URL Structure**

> **\[PUT]** /api/v2.1/org/`<org_id>`/admin/users/`<email>`/set-password/



**Request Authentication**

> Org-admin Authentication (Token)



**Sample Request**

Reset the password of the user with ID `b5cdf2ab97ef426ea00f55f674a74b99@auth.local`:
> ```
> curl -X PUT 
> -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" \
> https://cloud.seatable.io/api/v2.1/org/12/admin/users/b5cdf2ab97ef426ea00f55f674a74b99@auth.local/set-password/
> ```


**Input Parameters**

JSON-object with the new password.



**Sample Response**

A new password is returned:
> ```
> {
>     "new_password": "PcqK9nwSR0"
> }
> ```


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

404 Not Found: The user's ID was wrong, or not found:
> ```
> {
>     "error_msg": "User new-user@example.com not found."
> }
> ```
