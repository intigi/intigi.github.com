---
layout: default
---

# Recommendations

This endpoint returns the top *Recommendations* for:

* one of your [*Interests*](#interests)
* an ad-hoc [*Query*](#query)

Make sure to review the [*API query documentation*](#api_queries).

## Recommendations for Interests<a name="interests"> </a>

### Resource URL

`GET https://contentgems.com/api/v1/interests/<interest_id>/recommendations.json`

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
      A string to be appended to the query defined on the interest to further refine the recommendations.
      Example: On a "Restaurants" base query, you might want to add +"San Francisco" as a refinement.
      Please see the <a href="#api_queries">query documentation</a> for syntax and operators.
      Also make sure to URL encode any special characters. The earlier example would look like this:
      <code>GET https://contentgems.com/api/v1/interests/123/recommendations.json?query_refinement=%2B%22San%20Francisco%22</code>
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
    <td>found_at</td><td>The date and time in UTC when ContentGems found the article.</td>
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

`GET https://contentgems.com/api/v1/interests/1433/recommendations.json`

Response:

{% highlight javascript %}
[
  {
    "excerpt": "Lorem ipsum ...",
    "found_at": "Fri Jul 21 13:58:46 +0000 2012",
    "host_name": "contentgems.com",
    "images": [
      { "url": "http://static.contentgems.com/image1.jpg" },
      { "url": "http://static.contentgems.com/image2.jpg" }
    ],
    "popularity": 42,
    "title": "Accelerate your content marketing",
    "url": "https://contentgems.com",
    "videos": [
      { "url": "http://static.contentgems.com/video1.mp4" },
      { "url": "http://static.contentgems.com/video2.mp4" }
    ],
    "word_count": 256
  },
  ...
]
{% endhighlight %}





## Recommendations for ad-hoc queries<a name="query"> </a>

### Resource URL

`GET https://contentgems.com/api/v1/query/recommendations.json`

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
      <a href="#api_queries">query documentation</a>
      for details.<br/>
      Query string example for the required phrase +"Content Marketing":
      <code>query=%2B%22Content%20Marketing%22</code>.
      Query string example for the two required fuzzy terms "+solar~0.3 +panels~0.3":
      <code>query=%2Bsolar~0.3%20%2Bpanels~0.3</code>
    </td>
    <td>Required</td>
  </tr>
  <tr>
    <td>dedup_similarity_threshold</td>
    <td>
      ContentGems removes duplicate articles from the recommendations. It computes the <a href="https://en.wikipedia.org/wiki/Jaccard_index">Jaccard index</a> for each article pair in the result set and groups together any articles with very high Jaccard similarity indexes, only showing the most popular one. The `dedup_similarity_threshold` determines at what Jaccard index two articles are considered duplicates. Practical values are between 0.5 (vaguely similar article body text) and 0.99 (identical article body text).
    </td>
    <td>Optional, default: 0.85</td>
  </tr>
  <tr>
    <td>domain_ids_to_exclude</td>
    <td>
      List of domain ids to exclude from recommendations. No URLs from any of the excluded domains will be included in recommendations.<br/>
      Query string example: <code>domain_ids_to_exclude[]=1&amp;domain_ids_to_exclude[]=2</code>.
      You can retrieve a <em>Domain Name's</em> <code>domain_id</code> using the
      <a href="/api-docs/v1/domains.html">Domains API endpoint</a>.
      Note: You can also get a recommendation’s domain_id from a result in the web UI by hovering over the result‘s ‘Block Domain’ link and reading out the `i_source_id` parameter.<br/>
    </td>
    <td>Optional, default: [] (empty array, no exclusions)</td>
  </tr>
  <tr>
    <td>feed_bundle_ids_to_exclude</td>
    <td>
      List of Feed bundle ids to exclude from recommendations. No URLs from any of the excluded feed bundles will be included in recommendations.<br/>
      Query string example: <code>feed_bundle_ids_to_exclude[]=1&amp;feed_bundle_ids_to_exclude[]=2</code>.
      You can retrieve a <em>Feed Bundle's</em> <code>id</code> from the web UI: Go to "Manage Sources" / "Manage Bundles". Hover over the "Edit" link for the bundle you want and read out the number after the <code>/i_feed_bundles/</code> segment in the URL.
    </td>
    <td>Optional, default: [] (empty array, no exclusions)</td>
  </tr>
  <tr>
    <td>feed_bundle_ids_to_use</td>
    <td>
      List of Feed bundle ids to limit recommendations to. Only URLs from the used feed bundles will be included in recommendations.<br/>
      Query string example: <code>feed_bundle_ids_to_use[]=1&amp;feed_bundle_ids_to_use[]=2</code>.
      You can retrieve a <em>Feed Bundle's</em> <code>id</code> from the web UI: Go to "Manage Sources" / "Manage Bundles". Hover over the "Edit" link for the bundle you want and read out the number after the <code>/i_feed_bundles/</code> segment in the URL.
    </td>
    <td>Optional, default: [] (empty array, no limitations)</td>
  </tr>
  <tr>
    <td>found_within</td>
    <td>
      Recommendations must have been found within the given time period. One of
      'last_24_hours' or 'last_7_days'.<br/>
      Query string example: <code>found_within=last_24_hours</code>
    </td>
    <td>Optional, default: 'last_24_hours'</td>
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
    <td>max_word_count</td>
    <td>
      Recommendations must have at most this many words.<br/>
      Integer between 1 and 10,000.
    </td>
    <td>Optional, default: Nil</td>
  </tr>
  <tr>
    <td>minimum_popularity</td>
    <td>
      Recommendations must have a popularity equal to or higher than this.<br/>
      One of:<br/>
      <code>"none"</code>, <code>"very_low"</code>, <code>"low"</code>, <code>"medium"</code>, <code>"high"</code>, or <code>"very_high"</code>.
    </td>
    <td>Optional, default: "none"</td>
  </tr>
  <tr>
    <td>minimum_score</td>
    <td>
      Recommendations must have a score higher than this. Scores are
      computed by the indexed search engine and typically range from 0.01 to 15.<br/>
      Query string example: <code>minimum_score=0.5</code>
    </td>
    <td>Optional, default: Nil</td>
  </tr>
  <tr>
    <td>min_word_count</td>
    <td>
      Recommendations’ body text must have at least this many words.<br/>
      Integer between 1 and 10,000.
    </td>
    <td>Optional, default: Nil</td>
  </tr>
  <tr>
    <td>min_word_count_title</td>
    <td>
      Results’ title must have at least this many words.<br/>
      Integer between 1 and 10,000.
    </td>
    <td>Optional, default: Nil</td>
  </tr>
  <tr>
    <td>must_have_image</td>
    <td>
      Recommendations must have images. Boolean true or false.<br/>
      Query string example: <code>must_have_image=true</code>
    </td>
    <td>Optional, default: false</td>
  </tr>
  <tr>
    <td>must_have_video</td>
    <td>
      Recommendations must have videos. Boolean true or false.<br/>
      Query string example: <code>must_have_video=true</code>
    </td>
    <td>Optional, default: false</td>
  </tr>
  <tr>
    <td>rank_by</td>
    <td>
      Recommendations will be ranked by this attribute before the top items are selected. One of
      'relevancy' or 'popularity'.<br/>
      Query string example: <code>rank_by=popularity</code>
    </td>
    <td>Optional, default: 'popularity'</td>
  </tr>
  <tr>
    <td>response_fields</td>
    <td>
      List of response fields to return. Array containing any of the following strings:
      <ul>
        <li>excerpt</li>
        <li>found_at</li>
        <li>host_name</li>
        <li>images</li>
        <li>popularity</li>
        <li>score</li>
        <li>title</li>
        <li>url</li>
        <li>videos</li>
        <li>word_count</li>
        <li>highlights</li>
      </ul>
      Query string example: <code>response_fields[]=title&amp;response_fields[]=url</code>
    </td>
    <td>Optional, default: all fields</td>
  </tr>
  <tr>
    <td>sort_by</td>
    <td>
      Recommendations will be sorted by this attribute after the top items are selected. One of
      'date', 'relevancy' or 'popularity'.<br/>
      Query string example: <code>sort_by=date</code>
    </td>
    <td>Optional, default: 'date'</td>
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
      Example highlights for the query string 'test':
      <pre><code class="javascript">{
  'highlights': [
    "Subject: &lt;em&gt;test&lt;/em&gt; In a recent post, they report the results",
    "Rorschach &lt;em&gt;test&lt;/em&gt; of U.S.-Turkish, with Ankara viewing them"
  ]
}</code></pre>
    </td>
  </tr>
</table>

### Example

Request:

`GET https://contentgems.com/api/v1/query/recommendations.json?query=test%20query&response_fields[]=title&response_fields[]=url`

Response:

Same as response data for [*Interests*](#interests). Please see above for details.

## API queries<a name="api_queries"> </a>

Below is a list of ContentGems Recommendation API query examples. You need to URL encode each plain text query before submitting it to the ContentGems API.

<table>
  <tr>
    <th>Description</th>
    <th>Plain text query</th>
    <th>URL encoded query</th>
  </tr>
  <tr>
    <td>Basic query: Article must contain "banana".</td>
    <td><code>+banana</code></td>
    <td><code>%2Bbanana</code></td>
  </tr>
  <tr>
    <td>Phrases: Article must contain "banana boat".</td>
    <td><code>+"banana boat"</code></td>
    <td><code>%2B%22banana%20boat%22</code></td>
  </tr>
  <tr>
    <td>Multiple terms: Article must contain "apple" and "banana".</td>
    <td><code>+banana +apple</code></td>
    <td><code>%2Bbanana%20%2Bapple</code></td>
  </tr>
  <tr>
    <td>Should, must, must-not terms: Article should contain "apple" and/or "banana", must contain "lemon", and must not contain "pear".</td>
    <td><code>apple banana +lemon -pear</code></td>
    <td><code>apple%20banana%20%2Blemon%20-pear</code></td>
  </tr>
  <tr>
    <td>Field specifiers: Article must contain "apple" in the title and "banana" in the excerpt.</td>
    <td><code>title:+apple excerpt:+banana</code></td>
    <td><code>title%3A%2Bapple%20excerpt%3A%2Bbanana</code></td>
  </tr>
  <tr>
    <td>Boolean OR: Article must contain "apple" or "banana" in the title.</td>
    <td><code>title:+(apple banana)</code></td>
    <td><code>title%3A%2B%28apple%20banana%29</code></td>
  </tr>
  <tr>
    <td>Wildcards: Article must contain words that start with "banana", e.g., "banana" and "bananas".</td>
    <td><code>+banana*</code></td>
    <td><code>%2Bbanana%2A</code></td>
  </tr>
  <tr>
    <td>Boosting: Prefer articles that contain "apple" over those that contain "banana" or "pear".</td>
    <td><code>apple^2 banana pear</code></td>
    <td><code>apple%5E2%20banana%20pear</code></td>
  </tr>
  <tr>
    <td>Fuzzy matches: Match both "color" as well as "colour".</td>
    <td><code>~color0.3</code></td>
    <td><code>~color0.3</code></td>
  </tr>
</table>

### Available fields

* `title` - this matches the title only
* `body` - this matches the entire result body text
* `excerpt` - this matches the text body's first 300 characters

### URL encoding

All your API queries must be URL encoded before you submit them to ContentGems. You can use an [online URL encoder](https://www.urlencoder.org/) or do it manually.

Some common encoded characters:

* `+` (plus sign) => `%2B`
* (space) => `%20`
* `"` (double quote) => `%22`
* `^` (boost operator) => `%5E`

### Further information

Please see the [ContentGems help documentation](http://support.contentgems.com/interests/keywords-queries) for more information on queries.
