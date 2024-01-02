---
description: >-
  This guide walks through the main steps for setting up Token based SSO
  Authentication on Zapnito through to a 3rd party system.
---

# Token Based SSO Authentication

Use this guide when you want to delegate user authentication to a 3rd party system and not use the Zapnito native authentication. &#x20;

You will need software development resources to build and configure a token exchange workflow and associated API endpoints that can initiate an authentication workflow that sends user session information in response to receiving a valid session token and provide an HTTP response that provides user account information to the Zapnito platform.

Once the pre-requisites listed below have been met we will disabled the native Zapnito authentication process.

{% hint style="warning" %}
**Important** - Using this method of SSO will require that many of the Zapnito standard user journey's for registration, invitation and bulk upload will be disabled.
{% endhint %}

## Requirements / Pre-requisites

1. **At least one link** that links to your Zapnito community with an authentication token in the query parameters - for example https://your-community.com?authenticationKey=auth-token
2. **GetCurrentUserProfile API Endpoint** (see below for details) - You must provide an API endpoint that accepts a POST request located at the example following URL _https://www.example.com/api/auth/client/1/GetCurrentUserProfile_
3. **BASIC Authentication** - The Login endpoint above should be secured using BASIC Authentication - please provide the username/password through a secure channel
4. **Registration URL** - You must provide a URL that we can link to that allows users to click through to a registration form
5. **Shared Key -** we will provide you with a shared key secret that is sent through the API and matched on each request

{% swagger baseUrl="" path="/api/auth/client/1/GetCurrentUserProfile" method="post" summary="GetCurrentUserProfile API Endpoint" %}
{% swagger-description %}
The GetCurrentUserProfile API endpoint should support a POST HTTP Request as follows:
{% endswagger-description %}

{% swagger-parameter in="body" name="redirectUrl" type="string" %}
Redirect to a desired URL after completion. This must include the protocol (http/https).
{% endswagger-parameter %}

{% swagger-parameter in="body" name="authenticationKey" type="string" %}
The session token provided by your system in the original request, this is passed back when we request the user profile data.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sharedKey" type="string" %}
The shared secret key between your system and Zapnito
{% endswagger-parameter %}

{% swagger-response status="200" description="The response should include the first name, last name and email address of the user to allow Zapnito to create an account and create an active session." %}
```
{
  "FirstName" : "Joe",
  "LastName" : "Bloggs",
  "Email" : "joe.bloggs@acme.com",
  "Title" : "CEO",
  "CompanyName" : "ACME Inc."
}
```
{% endswagger-response %}
{% endswagger %}

