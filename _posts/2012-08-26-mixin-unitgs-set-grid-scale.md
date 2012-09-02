---
name: unitgs-set-grid-scale
type: mixin
user-level: User
layout: post
---

# mixin unitgs-set-grid-scale

Defines the scale over wich you want to set the grid.

For example, in a mobile first scenario, you probably want to have a grid scale for that size and other scales to higher dimensions.

<p class="note">To be applied only to the base container of the grid, normally the body.</p>

## Declaration

{% highlight sass %}
@mixin unitgs-set-grid-scale(
	$scale: undefined,
	$wrapper-tag: undefined
)
{% endhighlight %}

## Parameters

### $scale

Defines the scale that you want to set the grid with.

<p class="atention">In the resulting css, the result is extremly simple, but don't do it yourself, the grid needs to keep track of the current scale to be able to make other dimensions calculations.</p>

Default value: 1.

All the grid will be scaled apropriatly.

### $wrapper-tag

Defines the top tag that wraps the grid. Normally is the body tag, but you can set what you want.

If you don't want the grid to wrap the declaration for you, you can set it to none.

See the following examples:

{% highlight sass %}
@include unitgs-set-grid-scale();
{% endhighlight %}

Results in the following css:

{% highlight css %}
body {
	font-size: 1em;
}
{% endhighlight %}

If we set the wrapper tag to none, and wrap it ourselfs like this:

{% highlight sass %}
body {
	@include unitgs-set-grid-scale($wrapper-tag: none);	
}
{% endhighlight %}

We get the same css result.

Default value: body.

You can change the default tag changing the value of $unitgs-settings-default-wrapper-tag so that you don't have to set it all the time.

<p class="example">Example</p>

## Examples

For example, you migth want to have a base font size of 1.25em (20px) but you want to use 16px for mobile. You would do the following:

{% highlight sass %}
@include unitgs-set-grid-scale(0.8);
{% endhighlight %}

You can also indicate your own container:
{% highlight sass %}
@include unitgs-set-grid-scale(0.8, #main-container);
{% endhighlight %}

It will result in the following css:

{% highlight css %}
#main-container {
	font-size: 0.8em;
}
{% endhighlight %}