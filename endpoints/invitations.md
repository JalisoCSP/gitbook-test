---
description: >-
  Trigger invitation emails to your community and automatically place invited
  users into a specific group.
---

# Invitations

{% swagger baseUrl="https://[your-domain]" path="/api/v1/invitations" method="post" summary="Trigger an Invitation" %}
{% swagger-description %}
This endpoint allows you to trigger an Invitation to user to allow that user to join your Zapnito community. You can also use the same API to invite a user to a specific group or room.\
\
An example of a correctly formatted cURL Request:\
\
`curl -i -X "POST" "https://[your-domain]/api/v1/invitations"`  \
&#x20; `-H 'Authorization: Token token=[your-api-token]'`  \
&#x20; `-H 'Content-Type: application/json; charset=utf-8'`  \
&#x20; `-d $'{ "user": { "name": "Joe Mac", "email": "joe-mac@mac.com", "invited_by_email": "admin@your-community.com" } }'`
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" %}
application/json; charset=utf-8\

{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Authentication token in the format ''Token token=\[your api token]
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[name]" type="string" %}
The full name of the individual being invited
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[email]" type="string" %}
The email address of the individual being invited
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[invited_by_email]" type="string" %}
The email address of the person that is sending the invitation and had the necessary invitation abilities
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[origin_content_url]" type="string" %}
The origin content that you wish the user to be redirect to after completing the invitation process
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[group_uuid]" type="string" %}
The UUID of the Group that you wish to add the user to once they accept the invitation.  The UUID can be found on the Groups settings in your Zapnito site.\

{% endswagger-parameter %}

{% swagger-response status="200" description="Invitation successfully triggered." %}
```javascript
{ "invitation" :
  {
    "name" : "Joe Expert",
    "email" : "joe@expert.com",
    "invited_by_email" : "admin@community.com",
    "origin_content_url" : "https://community.com/content-to-redirect-to.html",
    "group_uuid" : "a1ecad96-8849-45ba-821e-20199cde45cd"
  }
}
```
{% endswagger-response %}

{% swagger-response status="401" description="Where the API token provided is not recognised or badly formatted.   Ensure HTTP_ AUTHORIZATION header value is `Token token=your-tokenhere` " %}
```
"HTTP Token: Access denied."
```
{% endswagger-response %}

{% swagger-response status="403" description="403: Forbidden is returned in two scenarios where the specified sender account does not have the correct permissions to send an invitation. 

Where you do not specify the optional *group_uuid* parameter the API will try to use the "create_invitation" ability.  This is where the user is placed into the default Group.  If the sender account does not have this "create_invitation" ability you will get the first error shown below.

If you are specifying the *group_uuid" parameter the sender account must have the "create_invitation_with_group" ability.

" %}
```javascript
{ 
  "error" : "admin-1@zapnito.com does not have the 'create_invitation' ability"
}

or 

{
  "error" : "admin-1@zapnito.com does not have the 'create_invitation_with_group' ability"
}
```
{% endswagger-response %}

{% swagger-response status="404" description="404: Not found can be returned in two scenarios, one where the Group is not found for the specified UUID, or when the user account is not found for the specified sender account in invited_by_email.
" %}
```javascript
// Where the UUID for the Group is not recognised
{
  "error": "Group not found for provided UUID 'uuid-that-does-not-exist'"
}

// Where the user account for authorised sender is not found
{ 
  "error" : "User account for sender sender-not-found@gmail.com not found"
} 
```
{% endswagger-response %}

{% swagger-response status="422" description="The email address for the invited individual is not a valid format" %}
```javascript
{  
  "errors" : 
    { "email" : [ "is invalid" ] }
}
```
{% endswagger-response %}
{% endswagger %}

