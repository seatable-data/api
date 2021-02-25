# Base Notification Rules

Notification rules are used to automatically notify certain users when certain condition in the base is met. In each notification rule, there are two main parts: the **Trigger conditions** and the **Actions**. 

Currently in SeaTable, you can define the following **Trigger conditions**:

* **Records near deadline**, where you can choose a date column, set number of days before that deadline, and set checking frequency, as well as a notification time during the day (0-23 hours).
* **Records modified**, whenever a record is modified.
* **Records meet specific conditions after modification**, here you can set fields to watch, and add filter conditions as well as filter conjunctions.

And as for the **Actions**, you can either

* Notify one or more specific users, or
* Notify users in a certain collaborator column. 

## List Notification Rules in A Base

Use this request to list all the notification rules saved in a base.


**URL Structure**

> **\[GET]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<base_name>`/notification-rules/



**Request Authentication**

> User Authentication (Token)



**Sample Request**

> ```
> curl \
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/notification-rules/"
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**base_name** _\[string, required]_
> The name of the base.



**Return Values**

JSON-object with the list of notification rules and their details. The `id` returned is the ID of the notification rule.



**Sample Response (200)**

> ```
> {
>     "dtable_notification_rule_list": [
>         {
>             "id": 9,
>             "run_condition": "per_update",
>             "trigger": {
>                 "rule_name": "Ruling",
>                 "table_id": "0000",
>                 "view_id": "Jz4d",
>                 "condition": "rows_modified"
>             },
>             "action": {
>                 "type": "notify",
>                 "default_msg": "Test rule is triggered!",
>                 "users": [
>                     "c7fh3rda6569491ba42905bf1647fd3f@auth.local"
>                 ],
>                 "users_column_key": "LfGJ"
>             },
>             "creator": "Jasmin Tee",
>             "ctime": "2021-02-22T12:15:45+00:00",
>             "last_trigger_time": ""
>         }
>     ]
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have access to the requested base:

> ```
> {
>     "error_msg": "Permission denied."
> }
>
> ```


## Add A Base Notification Rule

Use this request and its parameters to add a new notification rule.

**URL Structure**

> **\[POST]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<base_name>`/notification-rules/



**Request Authentication**

> User Authentication (Token)



**Sample Request**

> ```
> curl -X POST \
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/notification-rules/" \
> -d \
> '{ \
> 	"run_condition": "per_day", \
> 	"trigger": { \
> 		"rule_name": "Test", \
> 		"condition": "rows_modified", \
> 		"table_id":0000, \
> 		"view_id":0000 \
> 	}, \
> 	"action": { \
> 		"type":"notify", \
> 		"users":["c7fh3rda6569491ba42905bf1647fd3f@auth.local"] \
> 	} \
> }'
> ```


**Input Parameters**

**workspace_id** _\[int, required]_
> The ID of the workspace where the base is stored.

**base_name** _\[string, required]_
> The name of the base.

**RuleData** _\[JSON object, required]_
> In this JSON object, use the following params to define this notification rule:
> 
> **run_condition** _\[enum(`per_day`, `per_update`), required]_
>> Define whether the action should be triggered by date or table update. For 'Records near deadline', use `per_day` and for 'Records modified' and 'Records meet specific conditions after modification', use `per_update`. Details see below.
>
> **trigger** _\[JSON object, required]_
>> In this JSON object, define the trigger of the rule with the following params:
>> > **rule_name** _\[string, required]_
>> >> The name of the rule.
>> >
>> > **table_id** _\[string, required]_
>> >> The ID of the table.
>> >
>> > **view_id** _\[string, required]_
>> >> The ID of the view.
>> >
>> > **condition** _\[enum(`rows_modified`, `near_deadline`, `filters_satisfy`), required]_
>> >> * For 'Records near deadline', use `per_day` in the **run_condition** param and `near_deadline` here.
>> >> * For 'Records modified', use `per_update` in the **run_condition** param and `rows_modified` here.
>> >> * For 'Records meet specific conditions after modification', use `per_update` in the **run_condition** param and `filters_satisfy` here.
>> 
>> For the case **Records near deadline**, when `run_condition` is `per_day` and `condition` is `near_deadline`, you'll define which date column to use as deadline dates, and optionally define how many days before and to which time of the day should the notification be sent:
>> >
>> > **date_column_name** _\[string, required]_
>> >> For 'Records near deadline', give the name of the date column that contains the deadline dates. If left blank, the first date column in the table will be taken as deadline.
>> >
>> > **alarm_days** _\[int, optional]_
>> >> Use a number to define how many days before the deadline should the notification be triggered.
>> >
>> > **notify_hour** _\[int(0-23), optional]_
>> >> Specify to which hour of the day should the notification be sent.
>> 
>> For the case **Records modified**, when `run_condition` is `per_update` and `condition` is `rows_modified`, a notification is sent right away inside the base editor. If this notification is not read within two hours, it'll be sent via email, if the receiver has enabled email notification in their personal settings:
>> > There is no further trigger conditions necessary.
>>
>> For the case **Records meet specific conditions after modification**, when `run_condition` is `per_update` and `condition` is `filters_satisfy`, you can define which fields to watch and set filters:
>>
>> > **watch_all_columns** _\[enum(`true`, `false`, optional, `true` by default)]
>> >> Use `true` or leave this param blank, if you want all columns to be watched.
>> >
>> > **column_keys** _\[list, optional]
>> >> When certain columns should be watched, use this list to include their keys, so only when there's modification in these columns, this notification rule will be triggered.
>> >
>> > **filters** and **filter_conjunction** refer to the API Request [**List Rows by Filters**](https://docs.seatable.io/published/seatable-api/dtable-server/rows.md#user-content-List%20Rows%20by%20Filters). You can define filters for all the fields in the table as a combination to the watched fields. So that only when the filtered records in the watched fields are modified, will this notification rule be triggered.
>
> **action** _\[JSON object, required]_
>> In this JSON object, define the users to be notified with the following params:
>> > **type** _\[enum(`notify`), optional]_
>> >> For the moment, there's only one option to notify the user. The `notify` value means a notification will be sent inside the base editor, and when this isn't read within 2 hours, it'll be sent via email to the user, if the user's email setting is activated. In the near future, SeaTable will provide the option to send emails directly to users even outside your organization by configuring an email sending service.
>> >
>> > **users** _\[list, optional]_
>> >> In this list, provide the users' IDs to be notified. Alternatively, use the `users_column_key` to automatically select users from a collaborator column.
>> >
>> > **users_column_key** _\[string, optional]_
>> >> Select users to be notified from a collaborator column by providing its key.
>> > 
>> > **default_msg** _\[string, optional]_
>> >> Here you can write a short message to remind notified users why this notification is sent, for example "The battery has to be changed in 2 days!".


**Return Values**

JSON-object with the details of this notification rule.

**Sample Response (200)**

> ```
> {
>     "dtable_notification_rule_list": [
>         {
>             "id": 9,
>             "run_condition": "per_update",
>             "trigger": {
>                 "rule_name": "Ruling",
>                 "table_id": "0000",
>                 "view_id": "Jz4d",
>                 "condition": "rows_modified"
>             },
>             "action": {
>                 "type": "notify",
>                 "default_msg": "Test rule is triggered!",
>                 "users": [
>                     "c7fh3rda6569491ba42905bf1647fd3f@auth.local"
>                 ],
>                 "users_column_key": "LfGJ"
>             },
>             "creator": "Jasmin Tee",
>             "ctime": "2021-02-22T12:15:45+00:00",
>             "last_trigger_time": ""
>         }
>     ]
> }
> ```
When the params inside the `RuleData` come in conflict (for example, when `run_condition` is `per_day` but `condition` is `rows_modified`), no error will be returned but a new rule will be created with the default values of the `run_condition` or `condition`.


**Possible Errors**

400 Bad Request: The necessary params are missing or misspellt:
> ```
> {
>     "error_msg": "trigger invalid."
> }
> ```
> OR
> ```
> {
>     "error_msg": "action invalid."
> }
> ```

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have access to the requested base:

> ```
> {
>     "error_msg": "Permission denied."
> }
>
> ```




## Update A Base Notification Rule

Update the params of an existing notification rule.

**URL Structure**

> **\[PUT]** /api/v2.1/workspace/`<workspace_id>`/dtable/`<base_name>`/notification-rules/`<notification_rule_id>`/

**Request Authentication**

> User Authentication (Token)

**Sample Request**

> ```
> curl -X PUT \ 
> -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' \
> -H 'Accept: application/json; charset=utf-8; indent=4' \
> "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/notification-rules/2/" \
> -d '{ \
> 	"run_condition": "per_day", \
> 	"trigger": { \
> 		"rule_name": "Test 2", \
> 		"condition": "rows_modified", \
> 		"table_id":"0000", \
> 		"view_id":"0000" \
> 	}, \
> 	"action": { \
> 		"type":"notify", \
> 		"users":["c7fh3rda6569491ba42905bf1647fd3f@auth.local"] \
> 	} \
> }' 
> ```

**Input Parameters**

**notification_rule_id** _\[int, required]_
> The ID of the notification rule to be updated. This can be retrieved with the request **List Notification Rules in A Base**.

For the other params, refer to the API request **Add A Base Notification Rule**.

**Return Values**

JSON-object with the details of the updated notification rule.

**Sample Response (200)**

> ```
> {
>         "id": 2,
>         "dtable": "t1",
>         "run_condition": "per_day",
>         "trigger": {
>             "rule_name": "Test 2"
>             "condition": "rows_modified",
>             "table_id": "0000",
>             "view_id": "0000"
>         },
>         "action": {
>             "type": "notify",
>             "users": [
>                 "c7fh3rda6569491ba42905bf1647fd3f@auth.local"
>             ]
>         },
>         "creator": "admin",
>         "ctime": "2020-04-29T03:00:42+00:00",
>         "last_trigger_time": ""
> }
> ```

**Possible Errors**

401 Unauthorized: The auth token is invalid:

> ```
> {
>    "detail": "Invalid token"
> }
>
> ```

403 Forbidden: The user doesn't have access to the requested base:

> ```
> {
>     "error_msg": "Permission denied."
> }
>
> ```

404 Not Found: Probably was the notification rule ID incorrect:
> ```
> {
>     "error_msg": "notification_rule 1 not found."
> }
> ```

## Delete a Base notification rule

**URL Structure**

> **\[DELETE] **api/v2.1/workspace/`<workspace_id>`/dtable/`<name>`/notification-rules/\<dtable_notification_rule_id>/

**Request Authentication**

> User Authentication (Token)

**Sample request**

> ```
> curl 
> -X DELETE -H 'Authorization: Token e39d9392d02a770e3edccdc5116da293a7773533' 
> -H 'Accept: application/json; charset=utf-8; indent=4' "https://cloud.seatable.io/api/v2.1/workspace/1/dtable/t1/notification-rules/1/"
>
> ```

**Input Parameters**

**workspace_id** _\[int, required]_

> The ID of the workspace where the base is stored.

**name** _\[string, required]_

> The name of the base.

**Return Values**

JSON-object of the Base notification rule' details.

**Sample Response (200)**

```
{
    "success": true
}

```


