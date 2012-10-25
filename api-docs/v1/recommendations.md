---
layout: default
---

# Recommendations

This endpoint returns the top *Recommendations* for:

* one of your [*Interests*](#interests)
* one of your [*Interest Folders*](#interest_folders)
* an ad-hoc [*Query*](#query)

## Recommendations for Interests<a name="interests">&nbsp;</a>





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
    "excerpt": "Lorem ipsum ...",
    "found_at": "Fri Jul 21 13:58:46 +0000 2012",
    "host_name": "intigi.com",
    "images": [
      { "url": "http://static.intigi.com/image1.jpg" },
      { "url": "http://static.intigi.com/image2.jpg" }
    ],
    "popularity": 42,
    "title": "Accelerate your content marketing",
    "url": "https://intigi.com",
    "videos": [
      { "url": "http://static.intigi.com/video1.mp4" },
      { "url": "http://static.intigi.com/video2.mp4" }
    ],
    "word_count": 256
  },
  ...
]
{% endhighlight %}





## Recommendations for Interest Folders<a name="interest_folders">&nbsp;</a>

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





## Recommendations for ad-hoc queries<a name="query">&nbsp;</a>

### Resource URL

`GET https://intigi.com/api/v1/query/recommendations.json`

If you have a lot of query params, then you can also use a POST request and submit
the params in the request body to avoid length restrictions on URLs for GET requests.

### Request Parameters

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
    <th>Optional, required, defaults</th>
  </tr>
  <tr>
    <td>query</td>
    <td>
      The search query as string. Please see
      <a href="https://intigi.com/help/query_format">query documentation</a>
      for details.<br/>
      Query string example for the required phrase +"San Francisco": <code>query=%2B%22San%20Francisco%22</code>.
    </td>
    <td>Required</td>
  </tr>
  <tr>
    <td>max_items</td>
    <td>
      The maximum number of Recommendations to return.<br/>
      Integer between 1 and 50.
    </td>
    <td>Optional, default: 5</td>
  </tr>
  <tr>
    <td>minimum_score</td>
    <td>
      Results must have a score higher than this. Scores are
      computed by the indexed search engine and typically range from 0.01 to 15.<br/>
      Query string example: <code>minimum_score=0.5</code>
    </td>
    <td>Optional, default: Nil</td>
  </tr>
  <tr>
    <td>found_within</td>
    <td>
      Results must have been found within the given time period. One of
      'last_24_hours' or 'last_7_days'.<br/>
      Query string example: <code>found_within=last_24_hours</code>
    </td>
    <td>Optional, default: 'last_24_hours'</td>
  </tr>
  <tr>
    <td>must_have_image</td>
    <td>
      Results must have images. Boolean true or false.<br/>
      Query string example: <code>must_have_image=true</code>
    </td>
    <td>Optional, default: false</td>
  </tr>
  <tr>
    <td>must_have_video</td>
    <td>
      Results must have videos. Boolean true or false.<br/>
      Query string example: <code>must_have_video=true</code>
    </td>
    <td>Optional, default: false</td>
  </tr>
  <tr>
    <td>min_word_count</td>
    <td>
      Results must have at least this many words.<br/>
      Integer between 1 and 10,000.
    </td>
    <td>Optional, default: Nil</td>
  </tr>
  <tr>
    <td>max_word_count</td>
    <td>
      Results must have at most this many words.<br/>
      Integer between 1 and 10,000.
    </td>
    <td>Optional, default: Nil</td>
  </tr>
  <tr>
    <td>response_fields</td>
    <td>
      List of response fields to return. Array containing any of the following strings:
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
      </ul>
      Query string example: <code>response_fields[]=title&response_fields[]=url</code>
    </td>
    <td>Optional, default: all items marked with *</td>
  </tr>
</table>

### Response Data

Contains all the fields documented under [*Interests*](#interests), with the addition of the following:

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>score</td>
    <td>
      The score computed by the indexed search engine. It typically ranges from
      0.01 to 15.
    </td>
  </tr>
  <tr>
    <td>highlights</td>
    <td>
      Up to 3 document fragments that match the query, with matching terms highlighted.
      This is useful for debugging queries, as well as providing summarized
      context to readers.<br/>
      Example for the query string 'test':
      <pre>
        <code class="javascript">
          {
            'highlights': [
              "Subject: <em>test</em> In a recent post, they report the results",
              "Rorschach <em>test</em> of U.S.-Turkish, with Ankara viewing them"
            ]
          }
        </code>
      </pre>
    </td>
  </tr>
</table>

### Example

Request:

`GET https://intigi.com/api/v1/query/recommendations.json?query=test%20query&response_fields[]=title&response_fields[]=url`

Response:

Same as response data for [*Interests*](#interests). Please see above for details.
