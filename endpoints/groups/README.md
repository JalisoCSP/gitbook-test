---
description: Create a group
---

# Groups

{% swagger baseUrl="https://[your-domain]" path="/api/v1/groups" method="post" summary="Create a group" %}
{% swagger-description %}
This endpoint allows you to create a new Group record. See cURL example below:\
`curl -i -X "POST" "https://[your-domain]/api/v1/groups"`\
`-H 'Authorisation: Token token=[your-token]'`\
`-d $'{ "group": { "name": "Group Name", "group_type": "Person", "user_type": "Admin" } }'`
{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" type="string" %}
Authentication token in the format "Token token=\[your api token]"
{% endswagger-parameter %}

{% swagger-parameter in="query" name="group[name]" type="string" %}
The desired name of the new Group
{% endswagger-parameter %}

{% swagger-parameter in="query" name="group[group_type]" type="string" %}
The group type. Must be "Person" or "Organisation"
{% endswagger-parameter %}

{% swagger-parameter in="query" name="group[user_type]" type="string" %}
The user type. Must be "Admin" or "Student"
{% endswagger-parameter %}

{% swagger-response status="200" description="Group successfully created." %}
```
{
  "group": {
    "name": "Group Name 2",
    "group_type": "Person",
    "user_type": "Student",
    "uuid": "105fc15d-fe53-4ffd-ad66-1c49f53542de"
  }
}
```
{% endswagger-response %}

{% swagger-response status="422" description="422: Unprocessable Entity can be returned when a required parameter is missing." %}
```
{
    "errors": {
        "name": [
            "can't be blank"
        ],
        "group_type": [
            "must be one of: Person/Organisation"
        ],
        "user_type": [
            "must be one of: Admin/Student"
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}

