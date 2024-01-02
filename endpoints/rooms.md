---
description: Provides details of all the rooms on your Zapnito network
---

# Rooms

{% swagger method="get" path="/api/v1/rooms" baseUrl="https://[your-domain]" summary="List all rooms" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="page" %}
Pagination page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="per_page" %}
Number of results per page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="query" %}
Search term to reduce the number of results. Works for name.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" %}
Your API token in the format Token token=\<token>
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "rooms": [
    {
      "name"=>"Room 1",
      "description"=>"Room 1 description",
      "about"=>"Room 1 about",
      "position"=>1,
      "type"=>"public",
      "contributor_group_uuid"=>"52218d7c-ff20-4abd-b674-d377d8a8e0ba",
      "member_group_uuid"=>"52218d7c-ff20-4abd-b674-d377d8a8e0bv"
    }, {
      "name"=>"Room 2 name",
      "description"=>"Room 2 description",
      "about"=>"Room 2 about",
      "position"=>2,
      "type"=>"public"
      "contributor_group_uuid"=>"52218d7c-ff20-4abd-b674-d377d8a8e0ba",
      "member_group_uuid"=>"52218d7c-ff20-4abd-b674-d377d8a8e0bv"
    }
  ]
}

```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/rooms/:room_id" baseUrl="https://[your-domain]" summary="View a specific room" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="room_id" %}
ID of the room
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" %}
Your API token in the format Token token=\<token>
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "room": {
    "name"=>"Room 1",
    "description"=>"Room 1 description",
    "about"=>"Room 1 about",
    "position"=>1,
    "type"=>"public",
    "contributor_group_uuid"=>"52218d7c-ff20-4abd-b674-d377d8a8e0ba",
    "member_group_uuid"=>"52218d7c-ff20-4abd-b674-d377d8a8e0bv"
  }
}

```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="" %}
```javascript
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://[your-domain]" path="/api/v1/rooms" method="post" summary="Create a room" %}
{% swagger-description %}
This endpoint allows you to create a new Room record.

See example cURL below:\
`curl -i -X "POST" "https://[your-domain]/api/v1/rooms"`\
`-H 'Authorization: Token token=[your-token]'`\
`-d $'{ "room": { "name": "Room Name", "description": "Your description", "about": "Your about", "position": 1, "owner_email": "your@email.com" } }'`
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Authentication token in the format "Token token=\[your api token]"
{% endswagger-parameter %}

{% swagger-parameter in="query" name="room[name]" type="string" %}
The desired name of the new Room
{% endswagger-parameter %}

{% swagger-parameter in="query" name="room[description]" type="string" %}
The description of the new Room
{% endswagger-parameter %}

{% swagger-parameter in="query" name="room[about]" type="string" %}
The about of the new Room
{% endswagger-parameter %}

{% swagger-parameter in="query" name="room[type]" type="string" %}
The type of the new Room (accepts "public", "private" or "secret"). Defaults to "public"
{% endswagger-parameter %}

{% swagger-parameter in="query" name="room[position]" type="string" %}
The position of the new Room in your room list
{% endswagger-parameter %}

{% swagger-parameter in="query" name="room[owner_email]" type="string" required="true" %}
The email of the Room owner. This will be the initial contributor, usually your own email address. This user must have the ability to create rooms.
{% endswagger-parameter %}

{% swagger-response status="200" description="Room successfully created." %}
```
{ "room" :
  {
    "id": 123,
    "name" : "Room Name",
    "description" : "Your description",
    "about" : "Your about",
    "position" : 1,
    "contributor_group_uuid": "a1ecad96-8849-45ba-821e-20199cde45cd",
    "member_group_uuid": "a1ecad96-8849-45ba-821e-20199cde45cd"
  }
}
```
{% endswagger-response %}

{% swagger-response status="422" description="422: Unprocessable Entity can be returned in two scenarios. One where the user with the email of your "owner_email" parameter is not found, or when the other required parameters are missing or taken." %}
```
// User with the provided email cannot be found
{ errors: { owner_email: ["Couldn't find User"] }}

// Required parameters are missing or taken
{
    "errors": {
        "description": [
            "can't be blank"
        ],
        "name": [
            "has already been taken"
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}
