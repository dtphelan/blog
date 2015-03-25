---
layout:     post
title:      "Jekyll and Unique Post CSS"
subtitle:   "Adding page-specific assets to a post"
date:       2015-03-25 08:51:00
author:     "Daniel Phelan"
header-img: "img/post-bg-04.jpg"
comments:   true
---
One of my goals for this thing is to turn my work papers into digital-first documents. NRRI is really focused on a simple Word-to-PDF publishing process, but most of the publishing world has moved onto digital publications. I'm trying to imagine what our papers would like like when they're focused on being read digitally, and that's why I'm putting up the Nuclear Retention paper. I'll probably be adding in "features" as I go along, and the first one I wanted to add was page-specific CSS and JS.

The standard formatting from Clean Blog is really nice, but I want to see if I can do some more customized things on these kind of "feature" posts. I didn't want to just add these things to the main CSS and JS files; they're a bit cumbersome to work with, the files are large, and I didn't want to bloat it up with redundant, page-specific classes.

I tried creating custom post layouts, but couldn't get things quite lined up right. There'd be a missing file, things would render incorrectly, all sorts of issues that kept happening. The Jekyll documentation isn't incredibly clear on how layouts work, so the process was a bit frustrating. There are a lot of tutorials out there that involve setting up your default layout, but none moving beyond that.

Eventually, I found <a href="http://mattgemmell.com/page-specific-assets-with-jekyll/">this post by Matt Gemmell.</a> Works like a charm. In your post's front matter, you add:
<pre><code>
  ___
  custom_css: custom
  custom_js:  custom
  ___
</code></pre>
Then, wherever your Head is:
<pre><code>
  {% if page.custom_css %}
    {% for stylesheet in page.custom_css %}
    <link rel="stylesheet" href="/css/{{ stylesheet }}.css" media="screen" type="text/css">
    {% endfor %}
  {% endif %}

  {% if page.custom_js %}
    {% for js_file in page.custom_js %}
    <script src='/javascripts/{{ js_file }}.js' type="text/javascript"></script>
    {% endfor %}
  {% endif %}
</code></pre>
This pulls in custom.css and custom.js to your post. Excellent.
