# Third Party Resources

{% swagger method="get" path="/api/v1/third_party_resources" baseUrl="https://[your-domain]" summary="List all resources" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" %}
Your API token in the format Token token=\<token>
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" %}
Pagination page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="per_page" %}
Number of results per page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="query" %}
Search term to reduce the number of results. Works for title or third\_party\_ref.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Contents successfully retrieved." %}
```javascript
{
  "third_party_resources": [
    {
      "id": 1,
      "third_party_id": "1",
      "title": "Resource Title",
      "description": "Description",
      "canonical_url": "https://link.to/resource",
      "thumbnail_url": "https://link.to/thumbnail",
      "open_in_new_tab": true,
      "category": "Heading",
      "tags": []
    },
    {
      "id": 2,
      "third_party_id": "ABC123",
      "title": "Resource Title",
      "description": "Description",
      "canonical_url": "https://link.to/resource",
      "thumbnail_url": "https://link.to/thumbnail",
      "open_in_new_tab": true,
      "category": "Heading",
      "tags": ["Special", "Publishers"]
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/third_party_resources/:third_party_ref" baseUrl="https://[your-domain]" summary="View a specific resource" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" %}
Authentication token in the format "Token token=\[your api token]"
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-parameter in="path" name="third_party_ref" type="String" required="false" %}
ID of the resource from your external system
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Content successfully retrieved." %}
```javascript
{
  "third_party_resource": {
    "id": 5,
    "third_party_ref": "ABC123",
    "title": "Resource Title",
    "description": "Description",
    "canonical_url": "https://link.to/resource",
    "thumbnail_url": "https://link.to/thumbnail",
    "open_in_new_tab": false,
    "category": "Heading",
    "tags": ["Private"]
  }
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Record not found" %}
```javascript
{
   "Resource not found for ID: 1"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/api/v1/third_party_resources" baseUrl="https://[your-domain]" summary="Create a resource" %}
{% swagger-description %}
This endpoint allows you to create a new record. See example cURL below:

`curl -i -X "POST" "https://[your-domain]/api/v1/third_party_resources" -H 'Authorization: Token token=[your-token]' -H 'Content-Type: application/json' -d $'{ "third_party_resource": { "third_party_ref": "ABC123", "title": "Resource Title", "description": "Description", "canonical_url": "https://link.to/resource", "thumbnail_url": "https://link.to/thumbnail", "category_name": "Heading", "open_in_new_tab": true, "published_at": "2022-01-14T09:25:00", "tags": ["Private"] } }'`
{% endswagger-description %}

{% swagger-parameter in="body" name="third_party_resource[third_party_ref]" type="String" %}
ID of the resource from your external system
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" name="third_party_resource[title]" type="String" %}
The desired title of the new resource
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[description]" type="String" %}
Description, about or body of the resource
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" name="third_party_resource[canonical_url]" type="String" %}
The url of the external resource
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[thumbnail_url]" type="String" %}
The url of the desired thumbnail
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" name="third_party_resource[category_name]" type="String" %}
The category the resource belongs to
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" required="true" type="String" %}
Authentication token in the format "Token token=\[your api token]"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[open_in_new_tab]" type="Boolean" %}
If you want your canonical url to open in a new tab (Default: false)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[published_at]" type="String" %}
The published at date and time. For accuracy, ISO8601 format is best.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[tags]" type="Array" required="true" %}
The name of the desired tags. This does not create new tags, they must already exist.
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Content-Type" type="String" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Resource successfully created" %}
```javascript
{
  "third_party_resource": {
    "id": 1,
    "third_party_ref": "ABC123",
    "title": "Resource Title",
    "description": "Description",
    "canonical_url": "https://link.to/resource",
    "thumbnail_url": "https://link.to/thumbnail",
    "open_in_new_tab": false,
    "category": "Heading",
    "tags": ["Private"]
  }
}
```
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="Required parameter is missing" %}
```javascript
// Required parameters are missing
{
    "errors": {
        "title": [
            "can't be blank"
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="put" path="/api/v1/third_party_resources/:third_party_ref" baseUrl="https://[your-domain]" summary="Update a resource" %}
{% swagger-description %}
This endpoint allows you to update an existing record. See example cURL below:

`curl -i -X "PUT" "https://[your-domain]/api/v1/third_party_resources/[:third_party_id]" -H 'Authorization: Token token=[your-token]' -H 'Content-Type: application/json' -d $'{ "third_party_resource": { "third_party_ref": "ABC123", "title": "Resource Title", "description": "Description", "canonical_url": "https://link.to/resource", "thumbnail_url": "https://link.to/thumbnail", "category_name": "Heading", "open_in_new_tab": true, "published_at": "2022-01-14T09:25:00", "tags": ["Private"] } }'`
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" %}
Your API token in the format Token token=\<your-token>
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[third_party_ref]" type="String" %}
ID of the resource from your external system
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[title]" type="String" %}
The desired title of the resource
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[description]" type="Sting" %}
Description, about or body of the resource
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[canonical_url]" type="String" %}
The url of the external resource
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[thumbnail]" type="String" %}
The url of the desired thumbnail
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[category_name]" type="String" %}
The category the resource belongs to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="third_party_resource[open_in_new_tab]" type="Boolean" %}
If you want your canonical url to open in a new tab (Default: false)
{% endswagger-parameter %}

{% swagger-parameter in="path" name="third_party_ref" type="String" %}
Third party identifier from your external system
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="third_party_resource[published_at]" %}
The published at date and time. For accuracy, ISO8601 format is best.
{% endswagger-parameter %}

{% swagger-parameter in="body" type="Array" name="third_party_resource[tags]" required="true" %}
The name of the desired tags. This does not create new tags, they must already exist.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Resource successfully updated" %}
```javascript
{
  "third_party_resource": {
    "id": 1,
    "third_party_ref": "ABC123",
    "title": "Resource Title",
    "description": "Description",
    "canonical_url": "https://link.to/resource",
    "thumbnail_url": "https://link.to/thumbnail",
    "open_in_new_tab": false,
    "category": "Heading",
    "tags": ["Private"]
  }
}
```
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="Required parameters are missing" %}
```javascript
// Required parameters are missing
{
    "errors": {
        "title": [
            "can't be blank"
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="delete" path="/api/v1/third_party_resources/:third_party_ref" baseUrl="https://[your-domain]" summary="Delete a resource" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" %}
Your API token in the format Token token=\<your-token>
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="String" %}
application/json; charset=utf-8
{% endswagger-parameter %}

{% swagger-parameter in="path" name="third_party_ref" type="String" %}
ID of the resource from your external system
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Record successfully removed" %}
```javascript
{
  "message": "Resource ABC123 deleted"
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Record not found" %}
```javascript
{
   "Resource not found for ID: 1"
}
```
{% endswagger-response %}
{% endswagger %}
