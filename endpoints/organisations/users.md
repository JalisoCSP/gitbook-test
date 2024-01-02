---
description: These APIs allows you to add and remove known users to/from organisations.
---

# Users

{% swagger baseUrl="https://[your-domain]" path="/api/v1/organisations/:organisation_id/users" method="post" summary="Add a known user to an organisation" %}
{% swagger-description %}
This endpoint allows you add a known user to a group.\
\
Example cURL request:\
\
`curl -X "POST" "https://[your-domain]/api/v1/organisations/123/users" \`\
&#x20;    `-H 'Authorization: Token token=28273njwh28hu2h22u872yd8ddh28h' \`\
&#x20;    `-H 'Content-Type: application/json; charset=utf-8' \`\
&#x20;    `-d $'{ "user": { "email": "user-to-add@something.com", "owner": false } }'`
{% endswagger-description %}

{% swagger-parameter in="path" name="organiation_id" type="string" %}
ID of the organisation that you want to add the user to.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" %}
application/json; charset=utf-8\

{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
You API token in the format Token token=\<your-token>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[email]" type="string" %}
The email address of the user to be added to the organisation
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[owner]" type="Boolean" %}
Default: false\
\
If the user is an owner of the organisation. If true, they will be able to manage the organisation and add/remove other users.
{% endswagger-parameter %}

{% swagger-response status="200" description="A 200 will be returned if the user is successfully added to the group, or if the user already belongs to the group." %}
```
{
  "message": "User 'user-to-add@something.com' added to organisation with ID 123"
}

or

{
  "errors" : User 'user-to-add@something.com' already belongs to organisation with ID 123"
}
```
{% endswagger-response %}

{% swagger-response status="401" description="A 401 will be returned if your API is invalid, expired or badly formatted." %}
```
HTTP Token: Access denied.
```
{% endswagger-response %}

{% swagger-response status="404" description="Could not find an organisation or user matching this query." %}
```javascript
{
   "Organisation not found for ID: 123"
}

or 

{
   "User not found for email: 'user-to-remove@something.com'"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://[your-domain]" path="/api/v1/organisations/:organisation_id/users" method="delete" summary="Remove a known user from an organisation" %}
{% swagger-description %}
This endpoint allows you to remove a known user from a group\
\
`curl -X "DELETE" "https://[your-domain]/api/v1/organisations/123/users" \`\
&#x20;    `-H 'Authorization: Token token=2891u928ue98dd28ud982dd89' \`\
&#x20;    `-H 'Content-Type: application/json; charset=utf-8' \`\
&#x20;    `-d $'{ "user": { "email": "user-to-remove@something.com" } }'`
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" %}
ID of the organisation that you want to remove the user from
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
  "message": "User 'user-to-add@something.com' removed from organisation with ID 123"
}

or

{
  "errors" : "User 'user-to-remove@something.com' does not currently belong to organisation with ID 123"
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
   "Organisation not found for ID: 123"
}

or 

{
   "User not found for email: 'user-to-remove@something.com'"
}
```
{% endswagger-response %}
{% endswagger %}
