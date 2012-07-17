---
layout: default
---

# API Ping

Allows you to test if the API is operational at all.

## Ping with text response

This is the simplest test possible to run against the Intigi API. It doesn't require authentication or special formats.

### Resource URL

`GET https://intigi.com/api/v1/ping`

### Example

Request:

`GET https://intigi.com/api/v1/ping`

Response:

{% highlight javascript %}
"pong (as text)"
{% endhighlight %}

## Ping with JSON response

This test allows you to test the JSON response format.

### Example

Request:

`GET https://intigi.com/api/v1/ping.json`

Response:

{% highlight javascript %}
{ "success": "pong" }
{% endhighlight %}
