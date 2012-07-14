---
layout: default
---

## Intigi Recommendations API

Use this API to get recommendations for the `Interests` you set up earlier in JSON format.

### Example Request

Request:

`GET https://intigi.com/api/recommendations/v1/buckets/2`

Response:

{% highlight json %}
[
  {
    "url": "https://intigi.com",
    "found_at": "Fri Jul 16 16:58:46 +0000 2010",
    "title": "Accelerate your content marketing",
    "excerpt": "Lorem ipsum ...",
    "host_name": "intigi.com",
    "popularity": 70
  }
]
{% endhighlight %}
