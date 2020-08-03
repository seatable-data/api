# Org admin work weixin

## Update Organization Social Settings

Like [update organization settings](https://docs.seatable.io/published/seatable-api/dtable-web-v2.1-org/org-admin-settings.md#user-content-Update%20Org%20Settings), but request parameters are

* **workwx_corpid**: corpid of work weixin
* **workwx_secret**: secret of a work weixin app

## List Bound Work Weixin Departments

**GET** /api/v2.1/org/:org_id/admin/work-weixin/departments/

**Request Params:**

* **department_id**: the id of work weixin department, if none, list from root department

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/org/23/admin/work-weixin/departments/' \
--header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6'

```

**Sample Response**

```
{
    "errcode": 0,
    "errmsg": "ok",
    "department": [
        {
            "id": 2,
            "name": "dev",
            "parentid": 1,
            "order": 100000000
        },
        {
            "id": 3,
            "name": "front",
            "parentid": 2,
            "order": 100000000
        },
        {
            "id": 4,
            "name": "vue",
            "parentid": 3,
            "order": 100000000
        }
    ]
}

```

## List Members of a Bound Work Weixin Department

**GET** /api/v2.1/org/:org_id/admin/work-weixin/departments/:department_id/members/

**Request Params:**

* **fetch_child**: whether to list members recursively, true/false, optional false

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/org/23/admin/work-weixin/departments/2/members/' \
--header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6'

```

**Sample Response**

```
{
    "errcode": 0,
    "errmsg": "ok",
    "userlist": [
        {
            "userid": "LiuLiWei",
            "name": "LiuLiWei",
            "department": [
                4,
                2
            ],
            "position": "",
            "mobile": "13212345678",
            "gender": "1",
            "email": "",
            "avatar": "http://wework.qpic.cn/bizmail/7mo92QoFXInrZ5qic1hiaMDanep0ictenialVvWNv3gJshERKcAic5eibpdg/0",
            "status": 1,
            "enable": 1,
            "isleader": 0,
            "extattr": {
                "attrs": []
            },
            "hide_mobile": 0,
            "telephone": "",
            "order": [
                0,
                0
            ],
            "external_profile": {
                "external_attr": [],
                "external_corp_name": ""
            },
            "main_department": 2,
            "qr_code": "https://open.work.weixin.qq.com/wwopen/userQRCode?vcode=vqcd45aa0b600db45f",
            "alias": "",
            "is_leader_in_dept": [
                0,
                0
            ],
            "address": "",
            "thumb_avatar": "http://wework.qpic.cn/bizmail/7mo92QoFXInrZ5qic1hiaMDanep0ictenialVvWNv3gqshERKuAic5eibpdg/100",
            "contact_email": ""
        }
    ]
}

```

## Import Users from Work Weixin

**POST** /api/v2.1/org/:org_id/admin/work-weixin/users/batch/

**Request Params**:

* **user_list**: the list of user returned from [work weixin department members](<#List Members of a Bound Work Weixin Department>)

**Sample Request**

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/org/23/admin/work-weixin/users/batch/' \
--header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
--header 'Content-Type: application/json' \
--data-raw '{
    "userlist": [
        {
            "userid": "LiuLiWei",
            "name": "LiuLiWei",
            "department": [
                4,
                2
            ],
            "position": "",
            "mobile": "13212345678",
            "gender": "1",
            "email": "",
            "avatar": "http://wework.qpic.cn/bizmail/7mo92QoFXInrZ5qic1hiaMDanep0icteniaxVvWNv3gJshERKuAic5eibpdg/0",
            "status": 1,
            "enable": 1,
            "isleader": 0,
            "extattr": {
                "attrs": []
            },
            "hide_mobile": 0,
            "telephone": "",
            "order": [
                0,
                0
            ],
            "external_profile": {
                "external_attr": [],
                "external_corp_name": ""
            },
            "main_department": 2,
            "qr_code": "https://open.work.weixin.qq.com/wwopen/userQRCode?vcode=vcvd45aa0b600db45f",
            "alias": "",
            "is_leader_in_dept": [
                0,
                0
            ],
            "address": "",
            "thumb_avatar": "http://wework.qpic.cn/bizmail/7mo92QoFXInrZ5qic1hiaMDanep0ictenialVvWNv3gJshERKuoic5eibpdg/100",
            "contact_email": ""
        }
    ]
}'

```

**Sample Response**

```
{
    "success": [
        {
            "userid": "LiuLiWei",
            "name": "LiuLiWei",
            "email": "2132b57ceb5b4382bfd7b14e8c75818a@auth.local"
        }
    ],
    "failed": []
}

```

## Import a Work Weixin Department

**POST** /api/v2.1/org/:org_id/admin/work-weixin/departments/import/

**Request Params:**

* **work_weixin_department_id**: the id of work weixin department

**Sample Request**

```
curl --request POST 'https://cloud.seatable.io/api/v2.1/org/23/admin/work-weixin/departments/import/' \
--header 'Authorization: Token 95ca2c5f0bf469742f21023b191520f5a5c63eb6' \
--form 'work_weixin_department_id=2'

```

**Sample Response**

```
{
    "success": [
        {
            "type": "department",
            "department_id": 2,
            "department_name": "dev",
            "group_id": 121
        },
        {
            "type": "department",
            "department_id": 3,
            "department_name": "front",
            "group_id": 122
        },
        {
            "type": "department",
            "department_id": 4,
            "department_name": "vue",
            "group_id": 123
        },
        {
            "type": "user",
            "email": "2132b57ceb5b4382bfd7b14e8c75818a@auth.local",
            "api_user_name": "LiuLiWei",
            "department_id": 4,
            "group_id": 123
        },
        {
            "type": "user",
            "email": "e0d3910c20294bf4b11d8ae68a09c9d2@auth.local",
            "api_user_name": "ChengXiongChao",
            "department_id": 3,
            "group_id": 122
        }
    ],
    "failed": [
        {
            "type": "user",
            "email": "2132b57ceb5b4382bfd7b14e8c75818a@auth.local",
            "api_user_name": "LiuLiWei",
            "department_id": 2,
            "msg": "部门成员已存在"
        }
    ]
}

```

[update organization settings](https://docs.seatable.io/published/seatable-api/dtable-web-v2.1-org/org-admin-settings.md#user-content-Update%20Org%20Settings)

[update organization settings](https://docs.seatable.io/published/seatable-api/dtable-web-v2.1-org/org-admin-settings.md#user-content-Update%20Org%20Settings)
