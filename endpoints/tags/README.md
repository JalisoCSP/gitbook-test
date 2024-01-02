---
description: Find and create Tags
---

# Tags

{% swagger baseUrl="https://[your domain]" path="/api/v1/tags" method="post" summary="Create a Tag" %}
{% swagger-description %}
This endpoint allows you to create a new Tag record.  See example cURL command below:\
\
`curl -i -X "POST" "https://[your-domain]/api/v1/tags"`\
`-H 'Authorization: Token token=123456789'`\
`-H 'Content-Type: application/json; charset=utf-8'`\
`-d $'{ "tag": { "name": "Cheddar", "external_url": "http://www.cheese.com", "external_id": "1221", "parent_name": "Cheese" } }'`&#x20;
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Authentication token in the format "Token token=\[your token]"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tag[parent_name]" type="string" %}
The name of the parent tag if needed
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tag[external_id]" type="string" %}
The external unique ID for this tag
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tag[external_url]" type="string" %}
The URL that the tag should link to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tag" type="object" %}
The tag object in JSON
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tag[name]" type="string" %}
The name of the tag
{% endswagger-parameter %}

{% swagger-response status="201" description="Tag successfully created." %}
```
{ "tag" : {    
  "name": "Cheddar", 
  "external_url": "http://www.cheese.com", 
  "external_id": "1221", 
  "parent_name": "Cheese"
}
```
{% endswagger-response %}

{% swagger-response status="422" description="Various reasons why a 422 may be returned." %}
```
# Could not find a parent tag matching name provided.
{ "errors" : 
  { "message": "Tag named Cheddar was not created because no parent tag already exists with name: Cheese" }
} 

# Tag with provided name already exists.
{ "errors" : 
  { "name": "has already been taken" }
}

```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://[your-domain]" path="/api/v1/tags" method="get" summary="Get a list of existing tag records" %}
{% swagger-description %}
Get a list of existing tags\
\
`curl -i -X "GET" "https://[your-domain]/api/v1/tags?parent_name=Cheese" -H 'Authorization: Token token=123456789' -H 'Content-Type: application/json; charset=utf-8'`
{% endswagger-description %}

{% swagger-parameter in="path" name="parent_name" type="string" %}
Filter the results by parent\_name
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{ "tags" : [ 
  { "name": "Cheddar", "external_url": "http://www.cheddar.com", "external_id": "", "parent_name": "Cheese" },
  { "name": "Edam", "external_url": "", "external_id": "", "parent_name": "Cheese" },
  { "name": "Ricotta", "external_url": "", "external_id": "", "parent_name": "Cheese" },
  { "name": "Swiss", "external_url": "", "external_id": "", "parent_name": "Cheese" }
]
```
{% endswagger-response %}
{% endswagger %}

