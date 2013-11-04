---
layout: default
---

# Interest Folders and Interests

Returns a list of all *Interest Folders* and their included *Interests* for the authenticated user.

### Resource URL

`GET https://contentgems.com/api/v1/interest_folders.json`

### Request Parameters

N/A

### Response Attributes

The response is an array of *Interest Folder* objects with the following attributes:

**Interest Folder Attributes**:

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>id</td><td>The Interest Folder's id.</td>
  </tr>
  <tr>
    <td>name</td><td>The Interest Folder's name.</td>
  </tr>
  <tr>
    <td>interests</td><td>A list of Interests inside the current Interest Folder. See below for the Interest attributes.</td>
  </tr>
</table>

**Interest Attributes**:

<table>
  <tr>
    <th>Name</th><th>Description</th>
  </tr>
  <tr>
    <td>id</td><td>The Interest's id.</td>
  </tr>
  <tr>
    <td>name</td><td>The Interest's name.</td>
  </tr>
  <tr>
    <td>query</td><td>The Interest's query.</td>
  </tr>
</table>


### Example

Request:

`GET https://contentgems.com/api/v1/interest_folders.json`

Response:

{% highlight javascript %}
[
  {
    "id": 1789,
    "name": "Content Marketing",
    "interests": [
      {
        "id": 1433,
        "name": "Curation",
        "query": "curation \"content curation\" curate"
      },
      ... (more interests)
    ]
  },
  ... (more interest folders)
]
{% endhighlight %}

