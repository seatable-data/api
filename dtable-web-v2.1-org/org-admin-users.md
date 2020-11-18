# Org admin users

## List Users

**GET** /api/v2.1/org/{org_id}/admin/users/

**Request Params**

* **is_staff**: whether list admin users, true or false
* **page**: for pagination
* **per_page**: for pagination

**Sample request**

```
curl -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/org/12/admin/users/curl -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95"

```

**Sample response**

```
{
	"user_list": [{
		"email": "0f57ceedc87049a2af1b2726c147c617@auth.local",
		"name": "org~4-member-1",
		"contact_email": "org~4-member-1@seafile.com",
		"quota_usage": 0,
		"quota_total": -2,
		"last_login": "2020-05-20T07:11:51+00:00",
		"id": 155,
		"is_active": true,
		"ctime": "2020-04-10T09:52:41+00:00",
		"self_usage": 0,
		"quota": -2
	}],
	"per_page": 100,
	"page": 1,
	"page_next": false
}

```

## Add User

**POST** /api/v2.1/org/{org_id}/admin/users/

Request Params

* email: user's email
* name: user's name
* password: user's password

**Sample request**

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/org/23/admin/users/' --header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' --form 'email=org~4-member-3@seafile.com' --form 'name=org~4-member-3' --form 'password=123'

```

**Sample response**

```
{
    "id": 169,
    "is_active": true,
    "ctime": "2020-05-20T07:48:11+00:00",
    "name": "org~4-member-3",
    "email": "4b2160a16f4f49d8aa5ece84520d519b@auth.local",
    "contact_email": "org~4-member-3@seafile.com",
    "last_login": null,
    "self_usage": 0,
    "quota": -2
}

```

## Update User

**PUT** /api/v2.1/org/{org_id}/admin/users/{email}/

**Request Parameters**

choose one attribute to update

* name
* contact_email
* is_active
* is_staff

**Sample request**

```
curl -X PUT -d "name=o2aa" -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/org/12/admin/users/o2a@o2a.com/curl -X PUT -d "name=o2aa" -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95"

```

**Sample response**

```
{
	"email": "5ef77767e76345bdb72469923f2c2904@auth.local",
	"name": "o2aa",
	"contact_email": "org~4-member-2@seafile.com",
	"quota_usage": 0,
	"quota_total": -2,
	"is_active": false,
	"id": 168,
	"ctime": "2020-05-20T07:35:24+00:00",
	"last_login": null,
	"self_usage": 0,
	"quota": -2,
	"email_sent": false
}

```

## Delete User

**DELETE** /api/v2.1/org/{org_id}/admin/users/{email}/

**Sample request**

```
curl -X DELETE -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/org/12/admin/users/o2a@o2a.com/curl -X DELETE -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95"

```

**Sample response**

```
{
    "success": true
}

```

## Reset User Password

**PUT** /api/v2.1/org/{org_id}/admin/users/{email}/set-password/

**Sample request**

```
curl -X PUT -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95" -H 'Accept: application/json; indent=4' https://cloud.seatable.io/api/v2.1/org/12/admin/users/o2a@o2a.com/set-password/curl -X PUT -H "Authorization: Token 3f1e23157c3a1fd740e9dc1c5d748929fe319b95"

```

**Sample response**

```
{
    "new_password": "PcqK9nwSR0"
}

```


