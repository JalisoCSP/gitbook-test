---
description: Provides details of all the channels on your Zapnito network
---

# Channels

{% swagger baseUrl="https://[your-domain]" path="/api/v1/channels" method="get" summary="Get an index of all channels on the network" %}
{% swagger-description %}
This endpoint allows you to get an index of all the channels on your Zapnito network.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Your API key in the format Token token=\<your-api-key>
{% endswagger-parameter %}

{% swagger-response status="200" description="Channels successfully retrieved." %}
```javascript
{:channels=>
  [
    {:id=>2,
    :name=>"Channel Two",
    :description=>"Some description",
    :position=>1,
    :type=>"Channel",
    :pin_to_menu=>false,
    :access_type=>"open",
    :archived=>false,
    :created_at=>"2019-09-19T07:33:40Z"},
   {:id=>1,
    :name=>"Channel One",
    :description=>"Some description",
    :position=>2,
    :type=>"Channel",
    :pin_to_menu=>false,
    :access_type=>"open",
    :archived=>false,
    :created_at=>"2019-09-19T07:33:40Z"
   }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

