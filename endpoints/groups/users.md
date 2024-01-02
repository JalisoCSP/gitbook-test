---
description: >-
  These APIs allows you to search groups for existing users, and also add and
  remove known users to/from groups.
---

# Users

{% swagger baseUrl="https://[your-domain]" path="/api/v1/groups/:uuid/users" method="get" summary="Find users in a group " %}
{% swagger-description %}
Allows you to determine if a user already exists in a group or not.  Matching results are returned in an array.
{% endswagger-description %}

{% swagger-parameter in="path" name="uuid" type="string" %}
Group UUID to uniquely identify the group
{% endswagger-parameter %}

{% swagger-parameter in="query" name="query" type="string" %}
The email address or partial email address that you would like match on the group users
{% endswagger-parameter %}

{% swagger-response status="200" description="Returns an array of matching users.  When not match is found an empty array is returned." %}
```
{
 "users" : [
   {
     "name" : "Joe Smith",
     "email" : "joe.smith@smiths.com",
     "title" : "Chief Smith"
   },
   {
     "name" : "Joe Bloggs",
     "email" : "joe.bloggs@bloggs.com",
     "title" : "Chief Blogger"
   }
 ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://[your-domain]" path="/api/v1/groups/:uuid/users" method="post" summary="Add a known user to a group" %}
{% swagger-description %}
This endpoint allows you add a known user to a group.\
\
Example cURL request:\
\
`curl -X "POST" "https://[your-domain]/api/v1/groups/hd28d8dj-2982hd-2982jd0/users" \`\
&#x20;    `-H 'Authorization: Token token=28273njwh28hu2h22u872yd8ddh28h' \`\
&#x20;    `-H 'Content-Type: application/json; charset=utf-8' \`\
&#x20;    `-d $'{ "user": { "email": "user-to-add@something.com" } }'`
{% endswagger-description %}

{% swagger-parameter in="path" name="uuid" type="string" %}
UUID of the group that you want to add the user to.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" %}
application/json; charset=utf-8\

{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
You API token in the format Token token=\<your-token>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[email]" type="string" %}
The email address of the user to be added to the group
{% endswagger-parameter %}

{% swagger-response status="200" description="A 200 will be returned if the user is successfully added to the group, or if the user already belongs to the group." %}
```
{
  "message": "User user-to-add@something.com added to group Expert Users with UUID hd28d8dj-2982hd-2982jd0"
}

or

{
  "errors" : User user-to-add@something.com already belongs to group Expert Users with UUID 2dhdhd8-289d222-2323"
}
```
{% endswagger-response %}

{% swagger-response status="401" description="A 401 will be returned if your API is invalid, expired or badly formatted." %}
```
HTTP Token: Access denied.
```
{% endswagger-response %}

{% swagger-response status="404" description="Could not find a group matching this query." %}
```javascript
{
   "Group not found for UUID: '2dhdhd8-289d222-2323'"
}

or 

{
   "User not found for email: 'user-to-remove@something.com'"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://[your-domain]" path="/api/v1/groups/:uuid/users" method="delete" summary="Remove a known user from a group" %}
{% swagger-description %}
This endpoint allows you to remove a known user from a group\
\
`curl -X "DELETE" "https://[your-domain]/api/v1/groups/2dhdhd8-289d222-2323/users" \`\
&#x20;    `-H 'Authorization: Token token=2891u928ue98dd28ud982dd89' \`\
&#x20;    `-H 'Content-Type: application/json; charset=utf-8' \`\
&#x20;    `-d $'{ "user": { "email": "user-to-remove@something.com" } }'`
{% endswagger-description %}

{% swagger-parameter in="path" name="uuid" type="string" %}
UUID of the group that you want to remove the user from
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Your API token in the format Token token=\<your-token>
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[email]" type="string" %}
The email address of the user to be removed from the group
{% endswagger-parameter %}

{% swagger-response status="200" description="A 200 will be returned if the user is successfully removed from the group, or is already not in the group." %}
```
{
  "message": "User user-to-add@something.com removed from group Expert Users with UUID hd28d8dj-2982hd-2982jd0"
}

or

{
  "errors" : "User user-to-remove@something.com does not currently belong to group Expert Users with UUID 2dhdhd8-289d222-2323"
}
```
{% endswagger-response %}

{% swagger-response status="401" description="A 401 will be returned if your API key is incorrect or expired." %}
```
HTTP Token: Access denied.
```
{% endswagger-response %}

{% swagger-response status="404" description="404 may be returned if a group is not found for the given UUID or if a user is not found for the given email address" %}
```
{
   "Group not found for UUID: '2dhdhd8-289d222-2323'"
}

or 

{
   "User not found for email: 'user-to-remove@something.com'"
}
```
{% endswagger-response %}
{% endswagger %}
