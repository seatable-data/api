#  Notifications

## Delete User's Notifications

Delete all the current notifications sent to the user.


**URL Structure**

> **\[DELETE]** /api/v2.1/notifications/


**Request Authentication**

> User Authentication (Token)

**Sample Request**

> ```
> curl --request DELETE \
> --header 'Authorization: Token 60ba962845e8380d25948b95c3c439165fafbff1' \
> 'https://cloud.seatable.io/api/v2.1/notifications/' 
> ```


**Input Parameters**

None.


**Return Values**

JSON-object with the result of the operation.

**Sample Response (200)**

> ```
> {
>     "success": true
> }
> ```
This request makes sure all notifications are deleted, and will not return an error if there's no notifications.


**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```



