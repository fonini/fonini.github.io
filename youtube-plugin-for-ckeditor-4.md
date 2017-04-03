---
title: Youtube Plugin for CKEditor 4
author: fonini
layout: page
---
CKEditor Plugin to embed Youtube videos.

## Download

Checkout the <a href="https://github.com/fonini/ckeditor-youtube-plugin" target="_blank">repository on Github</a> or download from the latest stable version from [the plugin&#8217;s page](http://ckeditor.com/addon/youtube) on <a href="http://ckeditor.com/addons/plugins/all" target="_blank">CKEditor Plugin Repository</a>

## Installation

Follow these steps:

  1. Extract the downloaded file into the CKEditor **plugins**? folder.
  2. Enable the plugin by changing or adding the extraPlugins line in your configuration (config.js):

{% highlight js %}config.extraPlugins = "youtube";{% endhighlight %}

**Protip:** If you would like to use more than one extra plugin, use a comma to separate the plugin names. Do not put any space around the commas.
  
Example:
  
{% highlight js %}config.extraPlugins = "youtube,plugin2,plugin3";{% endhighlight %}

In CKEditor 4.1 or higher you need to disable ACF (Advanced Content Filter) in the config.js file:
  
{% highlight js %}config.allowedContent = true;{% endhighlight %}

## How to use

If everything is ok, a Youtube icon should appear on the CKEditor toolbar. Click it, paste your embed code or video URL and the video will be inserted.