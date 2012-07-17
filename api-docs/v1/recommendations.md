---
layout: default
---

# Recommendations

Returns the top *Recommendations* for one of your *Interests* or *Interest Folders*.

## Recommendations for Interests

### Resource URL

`GET https://intigi.com/api/v1/interests/<interest_id>/recommendations.json`

### Request Parameters

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>interest_id</td><td>The id of the Interest.</td>
  </tr>
  <tr>
    <td>max_items</td><td>Optional. The maximum number of Recommendations to return. Default: 5.</td>
  </tr>
</table>

### Response Attributes

The response is an array of *Recommendation* objects. Each *Recommendation* has the following attributes:

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>url</td><td>The URL of the recommended article.</td>
  </tr>
  <tr>
    <td>excerpt</td><td>The first 300 characters of the recommended article.</td>
  </tr>
  <tr>
    <td>found_at</td><td>The date and time in UTC when Intigi found the article.</td>
  </tr>
  <tr>
    <td>host_name</td><td>The host name of the URL.</td>
  </tr>
  <tr>
    <td>popularity</td><td>A measure of the recommended article's popularity on a scale of 0 to 100. 0 means not popular, 100 means extremely popular.</td>
  </tr>
  <tr>
    <td>title</td><td>The HTML document title of the recommended article, or the URL if no title is present.</td>
  </tr>
</table>

### Example

Request:

`GET https://intigi.com/api/v1/interests/1433/recommendations.json`

Response:

{% highlight javascript %}
[
  {
    "url": "https://intigi.com",
    "excerpt": "Lorem ipsum ...",
    "found_at": "Fri Jul 21 13:58:46 +0000 2012",
    "host_name": "intigi.com",
    "popularity": 70,
    "title": "Accelerate your content marketing"
  },
  ...
]
{% endhighlight %}

## Recommendations for Interest Folders

### Resource URL

`GET https://intigi.com/api/v1/interest_folders/<interest_folder_id>/recommendations.json`

### Request Parameters

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>interest_folder_id</td><td>The id of the Interest Folder.</td>
  </tr>
  <tr>
    <td>max_items</td><td>Optional. The maximum number of Recommendations to return. Default: 5.</td>
  </tr>
</table>

### Response Data

Same as response data for *Interests*. Please see above for details.

### Example

Request:

`GET https://intigi.com/api/v1/interest_folders/1789/recommendations.json`

Response:

Same as response data for *Interests*. Please see above for details.