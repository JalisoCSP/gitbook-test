---
description: List API allows you to list all content
---

# Contents

{% swagger baseUrl="https://[your-domain]" path="/api/v1/contents" method="get" summary="Get Contents" %}
{% swagger-description %}
This endpoint allows you to list all content
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Your API token in the format Token token=\<token>
{% endswagger-parameter %}

{% swagger-parameter in="query" name="tag" type="string" %}
The URL Encoded tag name that you would like to filter the results set by.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="per_page" type="number" %}
Limit the amount of content
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="number" %}
Paginate the content
{% endswagger-parameter %}

{% swagger-response status="200" description="Contents successfully retrieved." %}
```javascript
{
  "contents": [
    {
      "type": "Document",
      "title": "Title",
      "introduction": "Document description",
      "url": "https://community.com/documents/3-document-title-2",
      "canonical_url": "https://community.com/users/3-test-user/documents/3-document-title-2",
      "thumbnail_url": "https://community.com/image.png",
      "published_at": "2019-08-28T11:29:42Z",
      "created_at": "2019-08-28T11:30:42Z"
    },
    {
      "type": "Post",
      "title": "Title",
      "introduction": "Post description",
      "url": "https://community.com/posts/2-post-title-2",
      "canonical_url": "https://community.com/users/2-test-user/posts/2-post-title-2",
      "thumbnail_url": null,
      "published_at": "2019-08-28T11:28:42Z",
      "created_at": "2019-08-28T11:30:42Z"
    },
    {
      "type": "Video",
      "title": "Title",
      "introduction": "Video description",
      "url": "https://community.com/videos/1-video-title-2",
      "canonical_url": "https://community.com/users/1-test-user/videos/1-video-title-2",
      "thumbnail_url": "https://community.com/image.png",
      "published_at": "2019-08-28T11:27:42Z",
      "created_at": "2019-08-28T11:30:42Z"
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

