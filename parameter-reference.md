# SeaTable API Parameter Reference

## What are SeaTable API Parameters?
Basically, the SeaTable API parameters are the values to specify your request. For example, the name of a base, a table, or the ID of a row, or even the page number of a returned list. 

There are basically two ways to use a SeaTable API parameter:
* In the URL of a request. This parameter is directly included in the URL, for example:
> ```
> http://cloud.seatable.io/api/v2.1/dtable-activities/?page=1
> ```
* In a request body. Sometimes there're quite a few parameters to include in a single request, for example:
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


## What is included in this reference?
This parameter reference lists off the most general parameters used in the most SeaTable API requests. Some specific parameters are not listed here, but explicitly described in the specific API requests in their documentation.

## How to use this reference?
For each parameter, this reference explains its name, format, and, when applicable, its default value. You can use these values in your API requests directly by importing this documentation in your Postman and selecting the Environment **API Request Examples (cloud<span>.seatable.io)** and customizing the pre-filled example values.

## SeaTable API Parameter Reference

**server_address** _\[URL]_
> The address of your server. For example, "cloud<span>.seatable.io". As each API request in this documentation begins with an "/", do not include this symbol at the end of this parameter.

**username** _\[email]_
> The username you use to log in to SeaTable. Usually, this is the email address you have registered your SeaTable account with.

**password** _\[string]_
> Your login password.

**admin_token** _\[string]_
> The auth token of a system administrator.

**org_admin_token** _\[string]_
> The auth token of a team (organization) administrator.

**user_token** _\[string]_
> The auth token of a user.

**org_id** _\[int]_
> The ID of the organization. It is unique in a system.

**workspace_id** _\[int]_
> The ID of a workspace. A workspace is a place to store bases. This could be a user's "My bases", or the shared space of a team, etc. It is unique in a system.

**group_id** _\[int]_
> The ID of a group. A group is a shared space by multiple users inside an organization. The group's ID is unique in a system.

**user_id** _\[string]_
> The ID of a user, unique in a system. It consists of a 32-digit string with numbers (0-9) and letters (a-z) with a suffix "@auth.local". For historic reasons, sometimes this parameter is called `email` in the SeaTable API requests. This shouldn't be confused with the user's `contact_email` which is indeed the email address of the user.

**base_name** _\[string]_
> The name of a base. For historic reasons, sometimes this is called `dtable_name` in the SeaTable API requests.

**base_id** _\[int]_
> The numeric ID of a base. For historic reasons, sometimes this is called `dtable_id` or `id` in the SeaTable API requests.This ID is seen in some SeaTable API requests or responses. Not to be confused with the `base_uuid`.

**base_uuid** _\[string]_
> A 36-digit string combined with numbers (0-9) and letters (a-z) with a "`-`" on the 9th, 14th, 19th and 24th digit. For historic reasons, in some SeaTable API requests and responses it's seen as `dtable_uuid`. 

**table_name** _\[string]_
> The name of a table. When a new base is created, it's first table's name is "Table1" by default.

**table_id** _\[string]_
> The ID of a table. Also used as `tid`. The default ID of the first table in a base is always "0000".

**row_id** _\[string]_
> The ID of a row. Unique in a base.

**column_key** _\[string]_
> The ID of a column, in most cases used as `key`. Unique in a table. The default key of a first column in a table is always "0000".

**column_name** _\[string]_
> The name of a column.

**column_type** _\[string]_
> Choose one of the following strings to define the column type:
> ```
> 'number'              // For the column type Number.
> 'checkbox'            // For the column type Checkbox.
> 'date'                // For the column type Date.
> 'text'                // For the column type Text.
> 'single-select'       // For the column type Single Select.
> 'long-text'           // For the column type Long Text.
> 'image'               // For the column type Image.
> 'file'                // For the column type File.
> 'multiple-select'     // For the column type Multiple Select.
> 'collaborator'        // For the column type Collaborator.
> 'link'                // For the column type Link Other Records.
> 'formula'             // For the column type Formula.
> 'creator'             // For the column type Creator.
> 'ctime'               // For the column type Created Time.
> 'last-modifier'       // For the column type Last Modifier.
> 'mtime'               // For the column type Last Modified Time.
> 'geolocation'         // For the column type Geolocation.
> 'auto-number'         // For the column type Auto Number.
> 'url'                 // For the column type URL.
> 'email'               // For the column type Email.
> 'duration'            // For the column type Duration.
> ```
> For more details, refer to [SeaTable Manual - Column Types](https://seatable.io/en/docs/user-manual/datenmanagement/feld-typen/).

**view_name** _\[string]_
> Name of the view. The default name of the first view is always "Default View".

**view_id** _\[string]_
> ID of the view. Also used as `vid`. The default ID of the default view is always "0000".


**filters** _\[list]_

> In this list, compose one or more filter conditions. For each specific column type, these conditions can be:
>
> **For the column types Text、Geolocation**
>
> * `filter_predicate`: contains, does_not_contain, is, is_not, is_empty, is_not_empty
> * `filter_term`: a string or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column type Number**
>
> * `filter_predicate`: equal, not_equal, less, greater, less_or_equal, greater_or_equal, is_empty, > is_not_empty
> * `filter_term`: a string containing the number  (like "10") or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column type Checkbox**
>
> * `filter_predicate`: is
> * `filter_term`: true or false
> * `filter_term_modifier`: an empty string
>
> **For the column type Single-select**
>
> * `filter_predicate`: is, is_not, is_empty, is_not_empty
> * `filter_term`: a string containing the name of option (like "seaTable") or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column type Multiple-select**
>
> * `filter_predicate`: has_any_of, has_all_of, has_none_of, is_exactly, is_empty, is_not_empty
> * `filter_term`: an array that some items are the names of options or an empty array or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column types Date、Ctime、Mtime**
>
> * `filter_predicate`: is, is_within, is_before, is_after, is_on_or_before, is_on_or_after, is_not, > is_empty, is_not_empty
> * `filter_term`: a date string (like "2020-10-27 12:00") or an empty string
> * `filter_term_modifier`: changes with the change of `filter_predicate`
>   * if `filter_predicate` is 'is_within', it can be one of the_past_week, the_past_month, the_past_year, this_week, this_month,    this_year, the_next_week, the_next_month, the_next_year, the_next_numbers_of_days, the_past_numbers_of_days.
>   * if `filter_predicate` is 'is_empty' or 'is_not_empty', it is an empty string.
>   * Otherwise,  it can be one of today, tomorrow, yesterday, one_week_ago, one_week_from_now, one_month_ago, one_month_from_now, number_of_days_ago, number_of_days_from_now, exact_date or an empty string.
>
> **For the column type Collaborator**
>
> * `filter_predicate`:  has_any_of, has_all_of, has_none_of, is_exactly, is_empty, is_not_empty, include_me
> * `filter_term`: an array or an empty array or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column types Creator、Last_modifier**
>
> * `filter_predicate`: contains, dost_not_contain, include_me, is, is_not
> * `filter_term`: an array or an empty array or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column type Formula**
>
> * If the result type is 'string' or 'bool', process according to the text column type.
> * If the result type is 'date', process according to the date column type.
> * If the result type is 'number', process according to the number column type.
>
> **For the column type Link**
>
> * `filter_predicate`: contains, dost_not_contain, is_empty, is_not_empty
> * `filter_term`: a string or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column type Auto-number**
>
> * `filter_predicate`: contains, dost_not_contain, is, is_not
> * `filter_term`: a string or an empty string
> * `filter_term_modifier`: an empty string
>
> **For the column types File、Image、Long_text、URL**
>
> * not supported yet 
>
> For more details, refer to the [SeaTable Manual - Grouping, sorting, and filtering](https://seatable.io/en/docs/user-manual/datenmanagement/gruppierung-sortierung-filter/).

**filter_conjunction** _\[enum(__`And`__, __`Or`__)]_
> The conjunction type of multiple filter conditions. 



**external_link_token** _\[string]_
> The suffix of an external link, like in "https<span>://cloud.seatable.io/dtable/external-links/`<external_link_token>`/".

**invite_link_token** _\[string]_
> The suffix of an invite link, like in "https<span>://cloud.seatable.io/dtable/links/`<invite_link_token>`/".

**page** _\[int]_
> The page number of a returned list. This parameter can be used in some requests, and has a default value of 1.

**per_page** _\[int]_
> The items to display on each page, urually used in combination with `page`. This parameter has the default value of 10 or 25, depending on the specific requests.