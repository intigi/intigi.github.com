---
layout: default
---

# Recommendations

This endpoint returns the top *Recommendations* for:

* one of your [*Interests*](#interests)
* one of your [*Interest Folders*](#interest_folders)
* an ad-hoc [*Query*](#query)

## <a id="interests"></a> Recommendations for Interests

### Resource URL

`GET https://intigi.com/api/v1/interests/<interest_id>/recommendations.json`

### Request Parameters

<table>
  <tr>
    <th>Name</th><th>Description</th><th>Optional, required, defaults</th>
  </tr>
  <tr>
    <td>interest_id</td><td>The id of the Interest.</td><td>Required</td>
  </tr>
  <tr>
    <td>max_items</td><td>The maximum number of Recommendations to return.</td><td>Optional, default: 5</td>
  </tr>
  <tr>
    <td>query_refinement</td><td>
      A string to be appended to the query defined on the interest to further refine the results.
      Example: On a "Restaurants" base query, you might want to add +"San Francisco" as a refinement.
      Please see the <a href="https://intigi.com/help/query_format">query documentation</a> for syntax and operators.
      Also make sure to URL encode any special characters. The earlier example would look like this:
      <code>GET https://intigi.com/api/v1/interests/123/recommendations.json?query_refinement=%2B%22San%20Francisco%22</code>
    </td>
    <td>Optional, default: nil</td>
  </tr>
</table>

### Response Attributes

The response is an array of *Recommendation* objects. Each *Recommendation* has the following attributes:

<table>
  <tr>
    <th>Name</th><th>Description</th>
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
    <td>images</td><td>An array of image urls.</td>
  </tr>
  <tr>
    <td>popularity</td><td>
      A measure of the recommended article's popularity on a scale of 0 to 100.<br/>
      0 means not popular, 100 means extremely popular.
    </td>
  </tr>
  <tr>
    <td>title</td><td>The HTML document title of the recommended article, or the URL if no title is present.</td>
  </tr>
  <tr>
    <td>url</td><td>The URL of the recommended article.</td>
  </tr>
  <tr>
    <td>videos</td><td>An array of video urls.</td>
  </tr>
  <tr>
    <td>word_count</td><td>The number of words in the recommended article.</td>
  </tr>
</table>

### Example

Request:

`GET https://intigi.com/api/v1/interests/1433/recommendations.json`

Response:

{% highlight javascript %}
[
  {
    "title": "Accelerate your content marketing",
    "host_name": "intigi.com",
    "url": "https://intigi.com",
    "found_at": "Fri Jul 21 13:58:46 +0000 2012",
    "excerpt": "Lorem ipsum ...",
    "popularity": 42,
    "word_count": 256,
    "images": [
      { "url": "http://static.intigi.com/image1.jpg" },
      { "url": "http://static.intigi.com/image2.jpg" }
    ],
    "videos": [
      { "url": "http://static.intigi.com/video1.mp4" },
      { "url": "http://static.intigi.com/video2.mp4" }
    ],
  },
  ...
]
{% endhighlight %}

## <a id="interest_folders"></a> Recommendations for Interest Folders

### Resource URL

`GET https://intigi.com/api/v1/interest_folders/<interest_folder_id>/recommendations.json`

### Request Parameters

<table>
  <tr>
    <th>Name</th><th>Description</th><th>Optional, required, defaults</th>
  </tr>
  <tr>
    <td>interest_folder_id</td><td>The id of the Interest Folder.</td><td>Required</td>
  </tr>
</table>

### Response Data

Same as response data for [*Interests*](#interests).

### Example

Request:

`GET https://intigi.com/api/v1/interest_folders/1789/recommendations.json`

Response:

Same as example response for [*Interests*](#interests).


## <a id="query"></a> Ad-hoc query

### Resource URL

`GET https://intigi.com/api/v1/query/recommendations.json`

If you have a lot of query params, then you can also use a POST request and submit
the params in the request body to avoid length restrictions on GET requests.

### Request Parameters

<table>
  <tr>
    <th>Name</th><th>Description</th><th>Optional, required, defaults</th>
  </tr>
  <tr>
    <td>query</td><td>The search query. Please see <a href="https://intigi.com/help/query_format">query documentation</a> for details.</td><td>Required</td>
  </tr>
  <tr>
    <td>max_items</td><td>The maximum number of Recommendations to return.</td><td>Optional, default: 5</td>
  </tr>
  <tr>
    <td>minimum_score</td>
    <td>
      Results must have a score higher than this. Scores are
      computed by the indexed search engine and typically range from 0 to 10.</td><td>Optional, default: 0
    </td>
  </tr>
  <tr>
    <td>found_within</td>
    <td>
      Results must have been found within the given time period. One of
      'last_24_hours' or 'last_7_days'.</td><td>Optional, default: 'last_24_hours'
    </td>
  </tr>
  <tr>
    <td>must_have_image</td><td>Results must have images.</td><td>Optional, default: false</td>
  </tr>
  <tr>
    <td>must_have_video</td><td>Results must have videos.</td><td>Optional, default: false</td>
  </tr>
  <tr>
    <td>min_word_count</td><td>Results must have at least this many words.</td><td>Optional, default: No value</td>
  </tr>
  <tr>
    <td>max_word_count</td>
    <td>
      Results muast have at most this many words. Maximum value is 10,000.</td><td>Optional, default: No value
    </td>
  </tr>
  <tr>
    <td>response_fields</td>
    <td>
      List of response fields to return. One of:
      <ul>
        <li>excerpt*</li>
        <li>found_at*</li>
        <li>host_name*</li>
        <li>images*</li>
        <li>popularity*</li>
        <li>score*</li>
        <li>title*</li>
        <li>url*</li>
        <li>videos*</li>
        <li>word_count*</li>
        <li>highlights</li>
      </ul></td><td>Optional, default: all items marked with *</td>
  </tr>
</table>

other possible request params: source_ids_to_use, source_ids_to_exclude, minimum_should_match, block_repeat_results

### Response Data

Contains all the fields for [*Interests*](#interests), with the addition of the following:

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>score</td><td>The score computed by the indexed search engine.</td>
  </tr>
  <tr>
    <td>highlights</td><td>Document fragments that match the query, with matching terms highlighted. This is useful for debugging queries, as well as providing summarized context to readers.</td>
  </tr>
</table>

### Example

Request:

`GET https://intigi.com/api/v1/query/recommendations.json?query=test%20query`

Response:

Same as response data for [*Interests*](#interests). Please see above for details.
