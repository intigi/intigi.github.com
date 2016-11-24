---
layout: default
---

## Welcome to the ContentGems Website Widget V1 documentation

The ContentGems Website Widget lets you embed curated content from
ContentGems into your website.

### Getting started

Copy and paste the code below, on you website right before the head tag.


{% highlight javascript %}
<div id="ContentGemsWidget"></div>

<script>
window.ContentGemsWidgetOptions = {
  feed_id: 'YOUR_FEED_ID'
}

!function(){function t(){var t=a.createElement("script");t.type="text/javascript",t.async=!0,t.src="https://assets.contentgems.com/website-widget/1.1.0/website-widget.js";var e=a.getElementsByTagName("script")[0];e.parentNode.insertBefore(t,e)}var e=window,a=document;e.attachEvent?e.attachEvent("onload",t):e.addEventListener("load",t,!1)}();
</script>
{% endhighlight %}


### Configuration options

Below is an example of how you would configure the options available for the website widget:

{% highlight javascript %}
window.ContentGemsWidgetOptions = {
  // enabled or disable debug mode
  debug: false,

  // max number of items to display
  max: 50,

  // breakpoint sizes in pixels
  breakpoints: {
    large: 1200,
    medium: 992,
    small: 768
  },

  // use widget stylesheet
  stylesheet: true,

  // default initial view mode, 'grid', 'compact', 'list'
  view: 'grid',

  // id selector for the widget, where to place the widget
  selector: 'ContentGemsWidget',

  // show or hide the contentgems powered by logo
  poweredby: true,

  // classes for widget
  classes: {
    loading: 'cgw-loading',
    loaded: 'cgw-loaded',
    done: 'cgw-done',

    columnPrefix: 'cgw-col',

    container: 'cgw-container',

    viewToggle: 'cgw-view-toggle',
    viewPrefix: 'cgw-view',

    list: 'cgw-list',

    item: 'cgw-item',
    itemContent: "cgw-item--content",
    itemTitle: 'cgw-item--title',
    itemSource: 'cgw-item--source',
    itemImage: 'cgw-item--image',
    itemExcerpt: 'cgw-item--excerpt'
  }
};
{% endhighlight %}

<div class="table-responsive">
<table class="table table-bordered table-striped">
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>debug</td>
      <td>boolean</td>
      <td>false</td>
      <td><p>Enable or disable debug mode.</p></td>
    </tr>
    <tr>
      <td>max</td>
      <td>integer</td>
      <td>50</td>
      <td><p>Max number of items to display.</p></td>
    </tr>

    <tr>
      <td>breakpoints</td>
      <td>object</td>
      <td>
<pre>{
  large: 1200,
  medium: 992,
  small: 768
}</pre>
      </td>
      <td><p>The widget layout adapts at these width thresholds.</p></td>
    </tr>

    <tr>
      <td>stylesheet</td>
      <td>boolean</td>
      <td>true</td>
      <td>Whether to use the default widget stylesheet. Set to false to provide your own stylesheet.</td>
    </tr>
    <tr>
      <td>view</td>
      <td>string</td>
      <td>grid</td>
      <td><p>Default initial view mode, <code>'grid'</code>, <code>'compact'</code>, <code>'list'</code></p></td>
    </tr>
    <tr>
      <td>selector</td>
      <td>string</td>
      <td>"ContentGemsWidget"</td>
      <td>
        <p>ID selector for the widget, where to place the widget</p>
        <pre><div id="ContentGemsWidget"></div></pre>
      </td>
    </tr>
    <tr>
      <td>poweredBy</td>
      <td>boolean</td>
      <td>true</td>
      <td><p>Show or hide the ContentGems powered by logo.</p>
        <img src="/images/poweredBy.png" alt="">
      </td>
    </tr>
    <tr>
      <td>classes</td>
      <td>object</td>
      <td>
<pre>{
  loading: "cgw-loading",
  loaded: "cgw-loading",
  done: "cgw-done",
  columnPrefix: "cgw-col",
  container: "cgw-container",
  viewToggle: "cgw-view-toggle",
  viewPrefix: "cgw-view",
  list: "cgw-list",
  item: "cgw-item",
  itemContent: "cgw-item--content",
  itemTitle: "cgw-item--title",
  itemSource: "cgw-item--source",
  itemImage: "cgw-item--image",
  itemExcerpt: "cgw-item--excerpt"
}</pre>
      </td>
      <td>
        <p>Classes used by the widget, you can override them here.</p>
        <p>
          <code>cgw-container</code> will have the classes
          <code>cgw-done</code> when load is done, <code>cgw-loading</code> and when the widget is loading.
        </p>
        <p>
          <code>cgw-view-grid</code>,
          <code>cgw-view-list</code>,
          <code>cgw-view-compact</code> will be toggle on <code>cgw-container</code> for the different view modes
        </p>
        <p><code>cgw-item--image</code> the <code>img</code> will be loaded in, and have the class <code>cgw-loading</code>
        once the image has been loaded it will have the class <code>cgw-loaded</code>. You can see this below.
        </p>
<pre>&lt;div class="cgw-container"&gt;
  &lt;div class="cgw-list"&gt;

    &lt;div class="cgw-item cgw-col-3"&gt;
      &lt;a&gt;
        &lt;div class="cgw-item--image"&gt;
          &lt;img class="cgw-loaded"&gt;&lt;/div&gt;
        &lt;div class="cgw-item--title"&gt;&lt;/div&gt;
        &lt;div class="cgw-item--source"&gt;
          &lt;img/&gt;
          &lt;span&gt;&lt;/span&gt;
        &lt;/div&gt;
        &lt;div class="cgw-item--excerpt"&gt;&lt;/div&gt;
      &lt;/a&gt;
    &lt;/div&gt;

    ...

  &lt;/div&gt;
&lt;/div&gt;</pre>
      </td>
    </tr>
  </tbody>
</table>
</div>
