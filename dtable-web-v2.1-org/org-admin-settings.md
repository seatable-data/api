# Organization Administration: Settings

## Get Org Settings

Review the current settings of the organization.


**URL Structure**

> **\[GET]** /api/v2.1/org/admin/settings/


**Request Authentication**

> Org-admin Authentication (Token)



**Sample Request**

> ```
> curl --request GET \
> --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
> 'https://cloud.seatable.io/api/v2.1/org/admin/settings/' 
> ```


**Input Parameters**

None.


**Return Values**

JSON-object with details of the settings:
* `enable_force_2fa`: `true` if the two-factor-authentication is forced
* `enable_new_user_email`: `true` if an email will be sent to the newly added user
* `enable_external_user_access_invite_link`: `true` if sharing bases to external users per invite link is allowed


**Sample Response (200)**

The sample response indicates the current org settings:

>```
>{
>    "enable_force_2fa": false,
>    "enable_new_user_email": true,
>    "enable_external_user_access_invite_link": true
>}
>```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have org-admin permission for the given organization:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```



## Update Org Settings

Update the settings of the organization.


**URL Structure**

> **\[PUT]** /api/v2.1/org/admin/settings/



**Request Authentication**

> Org-admin Authentication (Token)



**Sample Request**

Change the settings:

> ```
> curl --location --request PUT \
> --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
> 'https://cloud.seatable.io/api/v2.1/org/admin/settings/' \
> --form 'enable_force_2fa=1'
> --form 'enable_new_user_email=0'
> --form 'enable_external_user_access_invite_link=0'
> ```


**Input Parameters**

**enable_force_2fa** _\[enum(`true` or `1`, `false` or `0`), optional]_
> Enable (`true` or `1`) or disable (`false` or `0`) the forced 2FA when users log in. Any other values than `true`, `1`, `false`, or `0` will be ignored.

**enable_new_user_email** _\[enum(`true` or `1`, `false` or `0`), optional]_
> Enable (`true` or `1`) or disable (`false` or `0`) email to newly added users. Any other values than `true`, `1`, `false`, or `0` will be ignored.

**enable_external_user_access_invite_link** _\[enum(`true` or `1`, `false` or `0`), optional]_
> Enable (`true` or `1`) or disable (`false` or `0`) sharing bases to external users per invite link. Any other values than `true`, `1`, `false`, or `0` will be ignored.


**Return Values**

JSON-object with details of the settings:
* `enable_force_2fa`: `true` if the two-factor-authentication is forced
* `enable_new_user_email`: `true` if an email will be sent to the newly added user
* `enable_external_user_access_invite_link`: `true` if sharing bases to external users per invite link is allowed



**Sample Response (200)**

The response from the sample request confirms the change of settings:

>```
>{
>    "enable_force_2fa": true,
>    "enable_new_user_email": false,
>    "enable_external_user_access_invite_link": false
>}
>```

**Possible Errors**

401 Unauthorized: The auth token is invalid:
>```
>{
>    "detail": "Invalid token"
>}
>```

403 Forbidden: The user doesn't have org-admin permission for the given organization:
> ```
> {
>     "detail": "You do not have permission to perform this action."
> }
> ```
