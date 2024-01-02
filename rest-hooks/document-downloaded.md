---
description: >-
  The Document Downloaded REST Hook allows you to submit a URL endpoint of your
  choosing that subscribes to be notified when a user downloads a document on
  your Zapnito community.
---

# Document Downloaded

When you subscribe to the Document Deleted REST Hook, your nominated URL will be sent a JSON payload containing details of the user deleted, this includes:

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
  "user_id" : 1,
  "name" : "John Anderson",
  "email" : "john.anderson@acme.com",
  "document_id" : 100,
  "title" : "Document Title",
  "downloaded_at" : "2021-02-24T13:40:35+00:00"
}
```

{% swagger baseUrl="https://[your-domain]" path="/api/v1/rest_hooks/document_downloaded/subscriptions" method="post" summary="Create new Document Downloaded REST Hook subscription" %}
{% swagger-description %}
This REST Hook endpoint allows registering a URL that subscribes to all document downloaded events.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Your API token in the format Token token=\<your-token>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="url" type="string" required="true" %}
The URL you want to be notified on when a document is downloaded
{% endswagger-parameter %}

{% swagger-parameter in="body" name="authorization_token" %}
An authorization token value that you want to be sent in the Header of the request back to your URL endpoint.   The token value will be added to the Authorization Header in the format \`Token token=abcdefgh\`
{% endswagger-parameter %}

{% swagger-response status="201" description="" %}
```
{
  "id" : "27"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://[your-domain]" path="/api/v1/rest_hooks/document_downloaded/subscriptions/:id" method="delete" summary="Delete an existing subscription to the Document Downloaded REST Hook" %}
{% swagger-description %}
This allows you to remove a previously registered URL for the Document Downloaded REST Hook.
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="integer" %}
The ID number of the subscription that was previously created.
{% endswagger-parameter %}

{% swagger-response status="204" description="204 No Content is returned when the subscription is successfully deleted" %}
```
```
{% endswagger-response %}

{% swagger-response status="404" description="404 Not Found is return when no subscription is found matching the provided ID" %}
```
```
{% endswagger-response %}
{% endswagger %}
