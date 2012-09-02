---
name: utils-convert-pixels-to-ems
type: function
user-level: User
layout: post
---

# function utils-convert-to-ems

It calculates the ems that correspond to the number of pixels passed.
It uses the base font size, the current scale and the font-size of the grid units where it is contained to do the conversion.

<p class="note">Because the base of the ems is the browsers default font size, the grid as no way to know if the user changed that configuration, so it assumes 16px for the browser's default font size.</p>

<p class="atention">Make the conversion in the context that you want to use, because the result changes depending on the context and a lot of variable values.</p>

## Declaration

{% highlight sass %}
@function utils-convert-pixels-to-ems(
	$number-of-pixels,
	$font-size: 1
)
{% endhighlight %}

## Parameters

### $number-of-pixels

Number of pixels to convert to ems.

### $font-size

The context to where you want to convert to ems.

This parameter is very important to set when you have nested columns that set the font-size parameter.
If none of the grid units set the font size, it is not necessary to set this parameter.

Default value: 1.

## Examples

In an elastic design it is essential to use ems from the beggining to the end, don't fall in the tentation of using px just for this little thing, it will always give bad results in the short term.

{% highlight sass %}
.avatar {
	width: utils-convert-pixels-to-ems(144px);
	height: utils-convert-pixels-to-ems(144px);
}
{% endhighlight %}

Or in case of nested units that have set the font-size.

{% highlight sass %}
.avatar {
	width: utils-convert-pixels-to-ems(144px, 2 1.5);
	height: utils-convert-pixels-to-ems(144px, 2 1.5);
}
{% endhighlight %}