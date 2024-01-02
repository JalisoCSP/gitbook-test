---
description: >-
  The Group Membership Rest Hook allows you to submit a URL endpoint of your
  choosing that subscribes to be notified when a user joins a group on your
  Zapnito community.
---

# User Added To Group

When you subscribe to the Group Membership REST Hook, your nominated URL will be sent a JSON payload containing details of the membership, this includes:

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
  "user_id" : "1",
  "name" : "John Anderson",
  "email" : "john.anderson@acme.com",
  "group_uuid" : "a1ecad96-8849-45ba-821e-20199cde45cd",
  "group_name" : "Awesome Group"
}

```

{% swagger baseUrl="https://[your-domain]" path="/api/v1/rest_hooks/group_membership_created/subscriptions" method="post" summary="Create a new Group Membership REST Hook Subscription" %}
{% swagger-description %}
The REST Hook endpoint allows registering a URL that subscribes to all group membership created events.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Your API token in the format Token token=\<your-token>
{% endswagger-parameter %}

{% swagger-parameter in="body" name="url" type="string" required="true" %}
The URL you want to be notified on when a user joins a group
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

{% swagger baseUrl="https://[your-domain]" path="/api/v1/rest_hooks/group_membership_created/subscriptions/:id" method="delete" summary="" %}
{% swagger-description %}
This allows you to remove a previously registered URL for the Group Membership Created REST Hook.
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="integer" %}
The ID number of the subscription that was previously created
{% endswagger-parameter %}

{% swagger-response status="204" description="204 No Content is returned when the subscription is successfully deleted" %}
```
```
{% endswagger-response %}

{% swagger-response status="404" description="404 Not Found is returned when no subscription is found matching the provided ID" %}
```
```
{% endswagger-response %}
{% endswagger %}
