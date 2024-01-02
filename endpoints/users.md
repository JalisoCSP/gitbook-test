---
description: Find and update user profile data on your community
---

# Users

{% swagger method="get" path="/api/v1/users" baseUrl="https://[your-domain]" summary="List all users" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" %}
Your API token in the format Token token=\<token>
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" %}
Pagination page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="per_page" %}
Number of results per page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="query" %}
Search term to reduce the number of results. Works for name, title or company.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "users": [
    {
      "id": 1,
      "email": "users@email.com",
      "name": "Name",
      "title": "Title",
      "company": "Company",
      "professional_reg_number": "ABC123",
      "country_code": "GB",
      "custom_field_options": []
    }, {
      "id": 2,
      "email": "another@email.com",
      "name": "Another",
      "title": "Title",
      "company": "Company",
      "professional_reg_number": "XYZ345",
      "country_code": "GB",
      "custom_field_options": []
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/users/:email" baseUrl="https://[your-domain]" summary="View a specific user" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" %}
Your API token in the format Token token=\<token>
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-parameter in="path" name="email" %}
The email of the user
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="User successfully retreived" %}
```javascript
{
  "user": {
    "id": 1,
    "email": "users@email.com",
    "name": "Name",
    "title": "Title",
    "company": "Company",
    "professional_reg_number": "ABC123",
    "country_code": "GB",
    "custom_field_options": []
  }
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Record not found" %}
```javascript
{
  "User not found for email: 'requested@email.com'"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://[your-domain]" path="/api/v1/users/:email" method="put" summary="Update a registered users profile information" %}
{% swagger-description %}
This endpoint allows update a user's profile information such as name, job title, company and country as well as assign or remove their selected custom field options.\
\
An example of a correctly formatted cURL request:\
\
`curl -X "PUT" "https://[www.your-domain.com]/api/v1/users/mike.smith@acme.com"`  \
&#x20; `-H 'Authorization: Token token=abcdefghijklmnop'`  \
&#x20; `-H 'Content-Type: application/json; charset=utf-8'`  \
&#x20; `-d $'{ "user": {` \
&#x20;    `"name": "Michael Smith",`\
&#x20;    `"title": "Vice President - Sales",`\
&#x20;    `"country_code": "US",`\
&#x20;    `"company": "ACME Inc.",`\
&#x20;    `"custom_field_option_ids": [ 2508, 2509 ]` \
&#x20;  `}` \
`}'`\

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Your API token in the format Token token=\<your token>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[custom_field_option_ids]" type="array" %}
An array of integers representing the ID numbers of the custom field options that the user is matched to.&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[country_code]" type="string" %}
The two letter ISO country code of the user, for example "GB" or "US"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[company]" type="string" %}
The name of the user's company
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[title]" type="string" %}
The job title of the user, if provided the user's job title will be modified to this value
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user[name]" type="string" %}
The name of the user, if provided the user's name will be modified to reflect the value passed into the API
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user" type="object" %}
JSON object encapsulating the user attributes to be modified
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
The email address of the user that you would like to modify
{% endswagger-parameter %}

{% swagger-parameter in="path" name="email" %}
The email of the user
{% endswagger-parameter %}

{% swagger-response status="200" description="If the update it successful, a 200 response code is returned along with a confirmation of the final saved user attributes in a JSON object." %}
```javascript
{
  "user": {
    "name": "Michael Smith",
    "title": "Vice President - Sales",
    "country_code": "US",
    "company": "ACME Inc.",
    "custom_field_option_ids": [2508, 2509]
  }
}
```
{% endswagger-response %}

{% swagger-response status="404" description="If no user is found for the given email address a 404 will be returned." %}
```javascript
{
    "message": "User not found for email: 'user-does-not-exist@here.com'"
}
```
{% endswagger-response %}
{% endswagger %}

