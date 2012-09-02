---
name: convert-to-media-queries-ems
type: function
user-level: User
layout: post
---

# function convert-to-media-queries-ems

This function is especific to convert the values to ems for media queries.
Because the media queries only have in consideration the browser default font size, and we have no way to know what are the current settings, we will use the default font size for most browsers that is 16px.

<p class="note">It does not have in consideration your base font size.</p>

<p class="atention">Warning: Currently we only support convertions from px to ems.</p>

## Declaration

{% highlight sass %}
@function convert-to-media-queries-em(
	$value-to-convert
)
{% endhighlight %}

## Parameters

### $value-to-convert

Currently we only accept px as a source value to convertion.

## Examples

480px = 30em.