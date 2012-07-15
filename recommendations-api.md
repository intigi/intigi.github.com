---
layout: default
---

# Recommendations API

Returns the top Recommendations for one of your Interests or Interest Folders in JSON format.

## Recommendations for Interests

### Resource URL

`GET https://intigi.com/api/recommendations/v1/interests/<interest_id>.json`

### Parameters

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>interest_id</td><td>The id of the Interest you want Recommendations for.</td>
  </tr>
  <tr>
    <td>max_items</td><td>Optional. The maximum number of recommendations to return. Default: 5.</td>
  </tr>
</table>

### Example

Request:

`GET https://intigi.com/api/recommendations/v1/interests/2.json`

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

## Recommendations for Interest Folders

### Resource URL

`GET https://intigi.com/api/recommendations/v1/folder/<folder_id>.json`

### Parameters

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>folder_id</td><td>The id of the Interest Folder you want Recommendations for.</td>
  </tr>
  <tr>
    <td>max_items</td><td>Optional. The maximum number of recommendations to return. Default: 5.</td>
  </tr>
</table>

### Example

Request:

`GET https://intigi.com/api/recommendations/v1/folders/2.json`

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

