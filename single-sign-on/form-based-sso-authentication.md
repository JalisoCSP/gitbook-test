---
description: >-
  This guide walks through the main steps for setting up form based
  Authentication on Zapnito through to a 3rd party system.
---

# Form Based SSO Authentication

Use this guide when you want to delegate user authentication to a 3rd party system and not use the Zapnito native authentication. &#x20;

You will need software development resources to build and configure an API endpoint that can receive user credentials and provide an HTTP response that provides user account information.

Once the pre-requisites listed below have been met we will disabled the native Zapnito authentication process.

{% hint style="warning" %}
**Important** - Using this method of SSO will require that many of the Zapnito standard user journey's for registration, invitation and bulk upload will be disabled.
{% endhint %}

## Requirements / Pre-requisites

1. **Login API Endpoint** - You must provide an API endpoint that accepts a POST request located at the following URL - **https://\<your-domain>/api/auth/client/1/login** \[the path defined here is mandatory]
2. **BASIC Authentication** - The Login endpoint above should be secured using BASIC Authentication - please provide the username/password through a secure channel
3. **Registration URL** - You must provide a URL that we can link to that allows users to click through to a registration form
4. **Shared Key -** we will provide you with a shared key secret that is sent through the API and matched on each request

### 1. Login API Endpoint

The Login API endpoint should expect the following JSON structure in the HTTP Request body

#### Request Body

```javascript
{
  "clientId" : "1",
  "sharedKey" : "01fc02aa-6251-4e90-b21d-81bb079319a7",
  "username" : "user-login-email@example.com",
  "password" : "users-password",
  "persistUserLogin" : "1"
}
```

#### Response Body

Assuming the user is authenticated with the provided username and password, the response from the Login API Endpoint should provide the following JSON data with a 200 HTTP response code.

```javascript
{
  "UserProfile" : 
  {
    "FirstName" : "Joe",
    "LastName" : "Bloggs",
    "Email" : "joe.bloggs@acme.com",
    "Title" : "Chief Blogger",
    "CompanyName" : "ACME Inc."
  } 
}
```

{% hint style="info" %}
&#x20;The first time a user logs in via this method, an account will be created for that email address if an account doesn't already exist.
{% endhint %}



