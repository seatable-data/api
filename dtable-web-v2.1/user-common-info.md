# User common info

## Get User Common Info

**GET** /api/v2.1/user-common-info/:email/

**Request Params**

* **email**: the user ID ending with @auth.local, required
* **avatar_size**: the size of info's avatar url, optional

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/user-common-info/xxxxxxx@auth.local/?avatar_size=12' --header 'Authorization: Token 74cb105bbc17f678748a90821045a29e7ae0bf9f'

```

**Sample Response**

```
{
    "email": "xxxxxxx@auth.local",
    "name": "admin",
    "contact_email": "admin@seafiletest.com",
    "avatar_url": "https://cloud.seatable.io/media/avatars/f/c/306ab43564752a999eecb57cabcefe/resized/12/e9d4953412684d3eccf7eaed805541f1_WuoaewF.png"
}

```

**Errors**:

* **404**: User not found.


