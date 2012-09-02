---
name: unitgs-init-grid
type: mixin
user-level: User
layout: post
---

# mixin unitgs-init-grid

This mixin initiates the grid for you, it will set the base definitions for you.

<p class="note">Note: Apply before start using the grid and after defining the grid-settings.</p>

<p class="atention">This mixin must be called inside the body tag or in your toplevel tag.</p>

## Declaration

{% highlight sass %}
@mixin unitgs-init-grid(
	$scale: undefined,
	$wrapper-tag: undefined,
	$reset-tags-list: undefined)
{% endhighlight %}

## Parameters

### $scale

The scale defines how the grid will be scaled based on the base font size set in the unitgs-set-grid-settings mixin.

This is important to set when you want to start with a different scale from your base definition.

Internaly it calls the unitgs-set-grid-scale to set the scale.

Default value: undefined 1.

### $wrapper-tag

The wrapper tag is the tag or identifier where the init will take place.
By default the body tag is used, but you can use another.

If you don't want the init grid to do the  wrapping for you, set the $wrapper-tag: none.

Default value: undefined body

### $reset-tags-list

The grid to work correctly needs that the tags be reseted to zero in the margin, border and paddings. With the exception of the form tags. This parameter allows you to specify which are the tags that you want to reset.

You can deactivate the reset completly by setting the $reset-tags-list: none.

Default value: undefined.

## Examples

Normal initialization of a grid. This will wrap the initialization in the body tag and will reset the margins, paddings and borders.

{% highlight sass %}
@include unitgs-init-grid();
{% endhighlight %}

If you want a grid based on a 20px font size and you want to scale down the grid to 16px for your mobile first design, you would write.

{% highlight sass %}
body {
	@include unitgs-init-grid(0.8, $wrapper-tag: none);
}
{% endhighlight %}