---
layout: default
---

# Recommendations API

Returns the top matching results for one of your `Interests` in JSON format.

## Resource URL

`GET https://intigi.com/api/recommendations/v1/buckets/<interest_id>.<format>`

## Parameters

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>interest_id</td><td>The id of the `Interest` you want recommendations for. Please see <a href="/">How to set up Interests</a> for details.</td>
  </tr>
  <tr>
    <td>format</td><td>One of <code>json</code> or <code>xml</code>.</td>
  </tr>
  <tr>
    <td>max_items</td><td>The maximum number of recommendations to return.</td>
  </tr>
</table>

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
