---
description: >-
  Authenticate your API calls using the `Authorization` header, providing your
  API token.
---

# Authentication

{% swagger baseUrl="https://[your-domain]" path="/api/v1/ping" method="get" summary="Check your API Key is valid" %}
{% swagger-description %}
This endpoint allows you to check that your API key is valid without being concerned with other required parameters for more complicated endpoints.  Simply send your API key in the Authorization header and we'll confirm if it is valid or not.\
\
An example of a correctly formatted cURL request\
\
`curl "https://[your-domain.com]/api/v1/ping"  \`\
&#x20; `-H 'Authorization: Token token=[your-api-key]'  \`\
&#x20; `-H 'Content-Type: application/json; charset=utf-8'` \

{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Authentication token in the format Token token=\<your token>
{% endswagger-parameter %}

{% swagger-response status="200" description="API key is valid." %}
```javascript
{
    "message": "Nice one, your API key is valid"
}
```
{% endswagger-response %}

{% swagger-response status="401" description="" %}
```
HTTP Token: Access denied.
```
{% endswagger-response %}
{% endswagger %}

