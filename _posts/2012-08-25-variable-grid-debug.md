---
name: grid-debug
type: variable
user-level: User
layout: post
---

# variable grid-debug

This variable control if you are in debug mode or not.

When you activate the debug mode, all the grid units background will have a different color so that you can se where your units are.

<p class="note">The debug mode is a excelent tool for responsive designs, because each time you set the grid unit properties, the background will have a new color. That makes the changes in the responsive design visible.</p>

It also controls the output trace types. When not in debug mode, only errors will be sent to the output window. But in debug mode traces of information, warnings and errors will be outputed giving the user the maximum information possible.

You can change the default behaviour of the debug mode changing the following settings:
- $debug-properties-to-color
- $gridgs-debug-minimum-trace-level-in-debug
- $gridgs-debug-minimum-trace-level

<p class="note">You can activate and deactivate the debug mode in the code as you want. Only the code that will between activations will be debugged.</p>

## Declaration

{% highlight sass %}
//De/Activates the debug mode.
$grid-debug: false !default;
{% endhighlight %}

Default value: false.

## Examples

{% highlight sass %}
@include grid-unit(); // Not debugged
$grid-debug: true;
@include grid-unit(); // Debugged
$grid-debug: false;
@include grid-unit(); // Not debugged
{% endhighlight %}