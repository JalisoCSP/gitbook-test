---
description: Create an organisation
---

# Organisations

{% swagger method="get" path="/api/v1/organisations" baseUrl="https://[your-domain]" summary="List all organisations" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="page" %}
Pagination page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="per_page" %}
Number of results per page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="query" %}
Search term to reduce the number of results. Works for name, title or company.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" %}
Your API token in the format Token token=\<token>
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Successfully retrieved" %}
```javascript
{
  "organisations": [
    {
      "id": 1,
      "name": "Organisation Name",
      "email": "info@organisation.com",
      "profile": "Profile information",
      "address": "123 Organisation Street",
      "country": "GB",
      "website_url": "https://organisation.com"
    }, {
      "id": 2,
      "name": "Another Organisation",
      "email": "another@organisation.com",
      "profile": "Profile information",
      "address": "456 Organisation Street",
      "country": "GB",
      "website_url": "https://organisation.com"
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://[your-domain]" path="/api/v1/organisations" method="post" summary="Create an organisation" %}
{% swagger-description %}
This endpoint allows you to create a new Organisation record. See cURL example below:\
`curl -i -X "POST" "https://[your-domain]/api/v1/organisations"`\
`-H 'Authorisation: Token token=[your-token]'`\
`-d $'{ "organisation": { "name": "Organisation Name", "email": "example@email.com", "public_email": "example@email.com", "profile": "Some profile content", "address": "123 Your Street, AB1 2CD", "country": "GB", "website_url": "https://youramazingwebsite.com", "public_phone_number": "07123 456 789", "remote_avatar_url": "https://youramazingwebsite.com/image/123" } }'`
{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" type="string" %}
Authentication token in the format "Token token=\[your api token]"
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[name]" type="string" %}
The desired name of the new Organisation
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[email]" type="string" %}
The email of the organisation
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[public_email]" type="string" %}
The public facing email of the organisation
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[profile]" type="string" %}
The profile content of your Organisation
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[address]" type="string" %}
The address of your Organisation
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[country]" type="string" %}
The country of your Organisation
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[website_url]" type="string" %}
The website url
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[public_phone_number]" type="string" %}
The public facing phone number of your Organisation
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[remote_avatar_url]" type="string" %}
The profile image of your Organisation, usually a logo
{% endswagger-parameter %}

{% swagger-response status="200" description="Organisation successfully created." %}
```
{
  "organisation": {
    "id": 123,
    "name": "Organisation Name",
    "email": "example@email.com",
    "public_email": "example@email.com",
    "profile": "Some profile content",
    "address": "123 Your Street, AB1 2CD",
    "country": "GB",
    "website_url": "https://youramazingwebsite.com",
    "public_phone_number": "07123 456 789",
    "remote_avatar_url": "https://youramazingwebsite.com/image/123"
  }
}
```
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Organisation with that email already exists" %}
```javascript
{
    errors: "Organisation with this email address already exists",
    id: 123 // ID of the duplicate Organisation
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
        "email": [
            "can't be blank"
        ],
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="put" path="/api/v1/organisations/:id" baseUrl="https://[your-domain]" summary="Update an organisation" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" %}
ID of the Organisation
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" %}
Your API token in the format Token token=\<your token>
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[name]" %}
The name of the Organisation
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[email]" %}
The email address
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[public_email]" %}
The publicly displayed email address
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[profile]" %}
The profile paragraph
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[address]" %}
The organisation address
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[country]" %}
The organisation country
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[website_url]" %}
The displayed website
{% endswagger-parameter %}

{% swagger-parameter in="query" name="organisation[public_phone_number]" %}
The publicly displayed phone number
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="If the response is successful, a 200 response code is returned along with a confirmation of the final saved Ogranisation attributes in JSON format" %}
```javascript
{
    "organisation": {
        "id": 123456,
        "name": "Zapnito",
        "email": "email@zapnito.com",
        "public_email": "public@zapnito.com",
        "profile": "<p>Zapnito is the SaaS online community platform for intelligence-driven organizations. We power branded, expert communities that allow members to learn, share knowledge and collaborate.</p>\n<p>An all-in-one community and learning platform, Zapnito provides all the tools you need to engage, retain and grow your communities so they stay longer, spend more, and encourage others to do the same.</p>",
        "address": "86-90 Paul St, London EC2A 4NE",
        "country": "GB",
        "website_url": "https://zapnito.com/",
        "public_phone_number": "+44 207 859 4272"
    }
}
```
{% endswagger-response %}
{% endswagger %}

