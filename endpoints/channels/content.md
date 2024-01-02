---
description: Get all content by channel
---

# Contents

{% swagger baseUrl="https://[your-domain]" path="/api/v1/channels/:channel_id/contents" method="get" summary="Get content by channel" %}
{% swagger-description %}
This endpoint allows you to get an index of all the content allocated to the given channel.
{% endswagger-description %}

{% swagger-parameter in="path" name="channel_id" type="number" %}
ID of the channel to get content for
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Your API key in the format "Token token=\<api-key>"
{% endswagger-parameter %}

{% swagger-parameter in="query" name="per_page" type="string" %}
Limit the amount of content per page
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="string" %}
Paginate the content
{% endswagger-parameter %}

{% swagger-response status="200" description="Channel content successfully retrieved." %}
```javascript
{:contents=>
  [{:id=>3,
    :type=>"Document",
    :title=>"Document title 1",
    :introduction=>"Some introduction",
    :canonical_url=>"http://test.host/users/3-test-user/documents/3-document-title-1",
    :thumbnail_url=>"https://images.stage-zapnito.com/users/3/documents/3/",
    :published_at=>"2019-09-19T07:46:03Z",
    :created_at=>"2019-09-19T07:47:03Z"},
   {:id=>2,
    :type=>"Post",
    :title=>"Post title 1",
    :introduction=>"Some introduction",
    :canonical_url=>"http://test.host/users/2-test-user/posts/2-post-title-1",
    :thumbnail_url=>nil,
    :published_at=>"2019-09-19T07:45:03Z",
    :created_at=>"2019-09-19T07:47:03Z"},
   {:id=>1,
    :type=>"Video",
    :title=>"Video title 1",
    :introduction=>"The video introduction",
    :canonical_url=>"http://test.host/users/1-test-user/videos/1-video-title-1",
    :thumbnail_url=>"https://images.stage-zapnito.com/static-assets/images/default_lrg_video_thumb.png",
    :published_at=>"2019-09-19T07:44:03Z",
    :created_at=>"2019-09-19T07:47:03Z"}]}
```
{% endswagger-response %}

{% swagger-response status="404" description="Could not find a channel matching this query." %}
```javascript
```
{% endswagger-response %}
{% endswagger %}

