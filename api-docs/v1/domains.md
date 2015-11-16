---
layout: default
---

# Domains

This endpoint allows you to retrieve the ContentGems `domain_id` for a given *Domain*. This is used for blocking *Recommendations* from certain *Domains*.

Please follow this procedure for every *Domain* you want to block:

* Retrieve the `domain_id` for the *Domain* using this API endpoint.
* Add the `domain_id` to a list of `domain_ids` you want to block on your end.
* Add the `domain_ids_to_exclude` request parameter to your *Recommendations* API requests. Use the list of `domain_ids` as value.

### Resource URL

`GET https://contentgems.com/api/v1/domains/lookup_id.json`

### Request Parameters

<table>
  <tr>
    <th>Name</th><th>Description</th><th>Optional, required, defaults</th>
  </tr>
  <tr>
    <td>domain_name</td><td>The name of the domain. The primary domain <code>contentgems.com</code> is considered different from the subdomain <code>www.contentgems.com</code>. This parameter is case insensitive.</td><td>Required</td>
  </tr>
</table>

### Response Attributes

The response is a Domain JSON object with the following attributes:

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>domain_name</td><td>The name of the domain after it has been normalized by ContentGems.</td>
  </tr>
  <tr>
    <td>domain_id</td><td>The id of the domain if it exists. Otherwise <code>null</code>.</td>
  </tr>
  <tr>
    <td>error</td><td>An error message if there is a problem handling the request.</td>
  </tr>
</table>

### Example

Request:

`GET https://contentgems.com/api/v1/domains/lookup_id.json?domain_name=ContentGems.com`

Response:

{% highlight javascript %}
{
  "domain_name": "contentgems.com",
  "domain_id": 962209
}
{% endhighlight %}
