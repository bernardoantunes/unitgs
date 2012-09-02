---
name: grid-line
type: mixin
user-level: User
layout: post
---

# mixin grid-line

The grid-line mixin is responsable of the vertical rythm in containers and text.
Even the grid-unit, internaly uses the grid-line to everything related to the vertical rythm.

You should use it to declare your headers and other text styles, because it will maintain the vertical rythm and makes it very easy to use modular scales.

## Declaration

{% highlight sass %}
@mixin grid-line(
	$font-size: undefined,
	$line-height: undefined,
	$fit-method: undefined,
	$padding-top: undefined,
	$padding-bottom: undefined,
	$margin-top: undefined,
	$margin-bottom: undefined,
	$height: undefined,
	$single-line-vertical-align: undefined
)
{% endhighlight %}

## Parameters

### $font-size

The font-size is set in unitless relative values to the base font size that you set in the settings mixin, imagine it as a rem over your settings.

The font-size in an elastic design is a very important value, because it defines the relative value of the dependent elements.

For example, if you want the font size to be 2 times bigger than the base font size, you will write the following:

{% highlight sass %}
@include grid-line($font-size: 2);
{% endhighlight %}

If the base font size was 1.25em (20px), this will make it 1.25em\*2em (40px).
Although it looks a relative simple setting, it will make the dimentions to be adjusted for that unit and all its contained units.

In the example above, the line height, margins, paddings, etc. all need to be scaled so that they maintain their original dimentions.

In the case of nested units, the grid line becomes even more important.

{% highlight sass %}
@include grid-line($font-size: 2 1.5 1);
{% endhighlight %}

You pass the list of the font-sizes of the parent containers, being the last value the font-size that you want to have. All the values are relative to you base font size, you don't need to make any calculations, the grid will do it for you.

Can you easily calculate in ems the top margin dimentions of your current element? ... probably not that easily, but you can relax because the grid does all the hard work. ;)

Default value: 1.

### $line-height

Allows to specify the ratio between the font-size and the line. Although you have the option to set it, that value will be adjusted to keep the vertical rythm. See the fit-method for your options to control it.

Default value: $unitgs-settings-base-line-height.

### $fit-method

When you set a new font-size, you can easily break the vertical rythm, but the UnitGS controls that and corrects the line height for you so that the vertical rythm is respected.

The grid will try to maintain the porporcionality of the font-size and the line-height. So if you have a ratio of 1.5, it will try to keep that, but in a grid with vertical rythm, that is not a simple matter, you have a rythm to maintain and that makes necessary to make some adjustments to the line-height.

You have 4 methods to decide how the grid will adjust the line-height.

Possible values:
- nearest (default) - Adjust the line height to the next closest line.
- ceil - Adjust the line height to the next line.
- floor - Adjust the line height to the line smaller line.
- bestfit - Ignores the ratio between font size and font size and it makes the best fit possible in the vertical rythm.

Below is an explanation of what each option makes:

#### nearest

If the line rounds do the nearest whole number where the font fits.

Ex: 1.2 = 1, 1.5 = 2, 1.8 = 2.

#### ceil

Always choose the next whole number.

Ex: 1.2 = 2, 1.5 = 2, 1.8 = 2.

#### floor

Always choose the base whole number if the font fits the line.

Ex: 1.2 = 1, 1.5 = 1, 1.8 = 1.

#### bestfit

This setting will ignores the ratio between the font size and the line height, and will set the line height to the lowest number of lines possible.

Default value: nearest.

### $padding-top and $padding-bottom

The vertical padings are defined in number of lines.

The following example sets 1 line padding on top and 2 on the bottom.

{% highlight sass %}
@include grid-unit($padding-top: 1, $padding-bottom: 2);
{% endhighlight %}

You can use fractions for the paddings like 1/2.

{% highlight sass %}
@include grid-unit($padding-top: 3/4, $padding-bottom: 5/4);
{% endhighlight %}

The only rule is that in the end it will give a whole number.
If the value does not give a whole number, it will be adjusted to the line maintaining the porporcionality of the values, but a warning will be on the output window informing what happened.

If no value is specified, no rule will be written to the css. If you want the value 0 to be written or you need to set the parameter to 0.
If you want to set it to the default value, set the parameter to default.

{% highlight sass %}
@include grid-unit($padding-top: 0, $padding-bottom: default); }
{% endhighlight %}

### $margin-top and $margin-bottom

The vertical margins are defined in number of lines.

The following example sets 1 line margin on top and 2 on the bottom.

{% highlight sass %}
@include grid-unit($margin-top: 1, $margin-bottom: 2);
{% endhighlight %}

You can use fractions for the margins like 1/2.

{% highlight sass %}
@include grid-unit($margin-top: 3/4, $margin-bottom: 5/4);
{% endhighlight %}

The only rule is that in the end it will give a whole number.
If the value does not give a whole number, it will be adjusted to the line maintaining the porporcionality of the values, but a warning will be on the output window informing what happened.

If no value is specified, no rule will be written to the css. If you want the value 0 to be written or you need to set the parameter to 0.
If you want to set it to the default value, set the parameter to default.

{% highlight sass %}
@include grid-unit($margin-top: 0, $margin-bottom: default); }
{% endhighlight %}

Default value: undefined.

### $height

You can define a specific height for an grid unit, just set the value in number of lines.

The following example sets grid unit height to 2 lines.

{% highlight sass %}
@include grid-unit($height: 2);
{% endhighlight %}

<p class="note">Note: You cannot use fraction of lines.</p>

Default value: undefined.

### $single-line-vertical-align: default

This parameter allows you to control the position of the text in the line.
This functionality is achieved by controling the text size and the vertical paddings.

It accepts values between 0 and 1:
- 0 - Aligns the text to the top of the line.
- 0\.5 - Aligns the text to the middle of the line.
- 1 - Aligns the text to the bottom of the line.

This work by subtracting the font size from the line height, and that value will be devided between the top and the bottom based on you input.

<p class="atention">Use this parameter if the content will only occupy one and only one line. If the text wraps the vertical rythm will be broken, so you want to ensure that the content will never wrap.
Use this parameter with great care, because you can very easily break the vertical rythm.</p>

Default value: undefined.

## Examples

**example descriptior**

{% highlight sass %}
{% endhighlight %}