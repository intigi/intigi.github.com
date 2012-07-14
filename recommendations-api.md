---
layout: default
---

# Intigi Recommendations API

Returns the top matching results for one of your `Interests` in JSON format.

## Resource URL

`GET https://intigi.com/api/recommendations/v1/buckets/<interest_id>.<format>`

## Parameters

| interest_id | The id of the `Interest` you want recommendations for. Please see [How to set up Interests](/) for details. |
| format | One of `json` or `xml` |
| count | The maximum number of recommendations to return |

## Example

Request:

`GET https://intigi.com/api/recommendations/v1/buckets/2.json`

Response:

{% highlight javascript %}
[
  {
    "url": "https://intigi.com",
    "found_at": "Fri Jul 16 16:58:46 +0000 2010",
    "title": "Accelerate your content marketing",
    "excerpt": "Lorem ipsum ...",
    "host_name": "intigi.com",
    "popularity": 70
  },
  {
    "url": "https://intigi.com",
    "found_at": "Fri Jul 16 16:58:46 +0000 2010",
    "title": "Accelerate your content marketing",
    "excerpt": "Lorem ipsum ...",
    "host_name": "intigi.com",
    "popularity": 70
  },
]
{% endhighlight %}
