---
description: >-
  The Content Viewed Rest Hook allows you to submit a URL endpoint of your
  choosing that subscribes to be notified when a piece of content is viewed on
  your community.
---

# Content Viewed

When you subscribe to the Content Viewed REST Hook, your nominated URL will be sent a JSON payload containing details of the content, this includes:

```
REQUEST HEADERS
 
"Accept" => "application/json"

// the hostname of the originating zapnito community
"X-Zapnito-Hostname" => "community.acme.org" 

// your API token if specified when registering the endpoint
"Authorization" => "Token token=abcdefg" 
```

```
{
  user: {
    id: '1',
    name: 'John Anderson',
    email: 'john.anderson@acme.com'
  },
  content: {
    id: '100',
    type: 'Post',
    title: 'Content Title'
  },
  viewed_at: '2021-11-18T13:52:06Z'
}
```

{% swagger method="post" path="/api/v1/rest_hooks/content_viewed/subscriptions" baseUrl="https://[your-domain]" summary="Create a new Content Viewed REST Hook Subscription" %}
{% swagger-description %}
The REST Hook endpoint allows registering a URL that subscribes to all Content Views on your community
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Your API token in the format Token token=\<your-token>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="url" required="true" %}
The URL you want to be notified on when a user views content
{% endswagger-parameter %}

{% swagger-parameter in="body" name="authorization_token" %}
An authorization token value that you want to be sent in the Header of the request back to your URL endpoint.   The token value will be added to the Authorization Header in the format \`Token token=abcdefgh\`
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="" %}
```javascript
{
  "id" : "27"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="delete" path="/api/v1/rest_hooks/content_viewed/subscriptions/:id" baseUrl="https://[your-domain]" summary="" %}
{% swagger-description %}
This allows you to remove a previously registered URL for the Content Viewed RestHook.
{% endswagger-description %}

{% swagger-parameter in="path" required="true" %}
The ID number of the subscription that was previously created
{% endswagger-parameter %}

{% swagger-response status="204: No Content" description="204 No Content is returned when the subscription is successfully deleted" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="404 Not Found is returned when no subscription is found matching the provided ID" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
