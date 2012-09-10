---
layout: default
---

# Buckets

Returns a list of all *Buckets* for the authenticated user.

### Resource URL

`GET https://intigi.com/api/v1/buckets.json`

### Request Parameters

N/A

### Response Attributes

The response is an array of *Bucket* objects with the following attributes:

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>id</td><td>The Bucket's id.</td>
  </tr>
  <tr>
    <td>name</td><td>The Bucket's name.</td>
  </tr>
  <tr>
    <td>atom_feed_url</td><td>The ATOM feed URL for this bucket's items.</td>
  </tr>
</table>

### Example

Request:

`GET https://intigi.com/api/v1/buckets.json`

Response:

{% highlight javascript %}
[
  {
    "id": 1789,
    "name": "Content Marketing Feed",
    "atom_feed_url": "https://intigi.com/users/123/buckets/1789-content-marketing-feed.atom"
]
{% endhighlight %}
