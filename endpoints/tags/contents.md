---
description: >-
  Interact with content within the context of Tags.   For example, assign
  content to a tag
---

# Contents

{% swagger baseUrl="https://[your-domain" path="/api/v1/tags/content" method="put" summary="Assign a list of content to a tag" %}
{% swagger-description %}
This endpoint allows you to assign a list of content items to an existing tag.  You can define the content either by URL or by Slug, or both.  \
\
`curl -X "PUT" "http://[your-domain]/api/v1/tags/contents?parent_name=food" /` \
`-H 'Authorization: Token token=123456789' /` \
`-H 'Content-Type: application/json; charset=utf-8' /` \
`-d $'{ "tag": {` \
&#x20; `"name": "Potato",` \
&#x20; `"content_urls": [` \
&#x20;   `"http://[your-domain]/posts/my-thoughts-on-video-panels-versus-webinars",     "http://your-domain/documents/zapnito-community-boost-workbook"` \
&#x20;   `],`\
&#x20; `"content_slugs": [`\
&#x20;   `"my-thoughts-on-video-panels-versus-webinars"`\
&#x20; `]`\
`}` \
`}'`
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Authentication token in the format 'Token token=123456789'
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tag[content_slugs]" type="array" %}
An array of slug strings of content that should be assigned to the tag
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tag[content_urls]" type="array" %}
An array of URLs of content that should be assigned to the tag
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tag[name]" type="string" %}
The name of the tag that should be assigned to the content
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tag" type="object" %}
The tag record that the content will be assigned to
{% endswagger-parameter %}

{% swagger-response status="200" description="Content successfully assigned to a tag." %}
```
{ "tag" : {    
  "name": "Cheddar", 
  "external_url": "http://www.cheese.com", 
  "external_id": "1221", 
  "parent_name": "Cheese",
  "content_urls": [
    "http://[your-domain]/posts/my-thoughts-on-video-panels-versus-webinars",
    "http://your-domain/documents/zapnito-community-boost-workbook"
  ]
}
```
{% endswagger-response %}

{% swagger-response status="404" description="A 404 Not Found status will be returned if no content items are found matching the provided URL or Slugs" %}
```
{
  "errrors" : 
    "content_urls": ["No matching items of content found"]
}
```
{% endswagger-response %}
{% endswagger %}

