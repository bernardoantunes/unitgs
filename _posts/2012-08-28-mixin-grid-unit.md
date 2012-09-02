---
name: grid-unit
type: mixin
user-level: User
layout: post
---

# mixin grid-unit

The grid-unit mixin is the central mixin of the Unit Grid System. It is through this mixin that you define the units that will be part of your layout.

The reason because we don't call this a column is because it controls much more than a column width. Go through the parameters list and the examples to see all what the grid-unit can do for you.

The grid unit is designed in a way that you only need to set the parameters that you want to set.
If you don't set the values, the default values will take place. The grid-unit will make the assumption that you have reset the margins, paddings and borders of the elements that you will convert in a grid-unit.

The grid-unit does not write all the attributes that you can set, only what it thinks that is necessary for the current instruction. If you want to force a specific behaviour, please set the parameter, don't leave it undefined.

If you want to set a specific parameter to its default/reset value, just set the value to default.

## Declaration

{% highlight sass %}
@mixin grid-unit(
	$width: undefined,
	$position: undefined,
	$margin-top: undefined,
	$margin-right: undefined,
	$margin-bottom: undefined,
	$margin-left: undefined,
	$container-type: undefined,
	$align: undefined,
	$font-size: undefined,
	$fit-method: undefined,
	$line-height: undefined,
	$padding-top: undefined,
	$padding-bottom: undefined,
	$height: undefined,
	$gutter: undefined,
	$single-line-vertical-align: undefined
	)
{% endhighlight %}

## Parameters

### $width

The width of a grid unit is defined in two main ways, or in number of columns or in a fraction of the container.

<p class="tip">The prefered method of setting the grid unit width is in fractions. It is much more intuitive and it has the advantage that if you want to reuse your definitions in a different grid, if the fractions give whole numbers, everything will still work as expected. For example, you will be able to have a top level grid-unit with a width of 1/3 in a 12, 24, even in a 15 columns grid.</p>

<p class="note">Note: Even if you set the width in a fraction value, the grid makes sure that it is a valid fraction for the current number of active columns and it will inform you in the output window.</p>

Default value: $xxx.

<p class="example">To set the grid to 2 columns width, you just have set $width: 2.</p>

<p class="example">To set the grid to 1/2 of the container columns, you just have set $width: 1/2 and the grid will do the math for you.</p>

The width of a column in a fluid design, have to know the parents size in order to correct the percentage of the occupied space.

The grid width parameter, in reality it accept a list of values that will make the calculation for you in the case of nested units.

<div class="example">

<p>We have the following html in a 12 active columns grid:</p>

{% highlight html %}
<div id="divA"></div>
<div id="divB">
	<div id="divBA"></div>
	<div id="divBB">
		<div id="divBBC"></div>
	</div>
	<div id="divBC"></div>
</div>
{% endhighlight %}

<p>We would set the grid-units with the following widths:</p>

{% highlight sass %}
#divA { @include grid-unit(1/2, $container-type: container); }
#divB { @include grid-unit(6, last, $container-type: container); }
#divBA { @include grid-unit(1/2 2, $container-type: contained); }
#divBB { @include grid-unit(6 1/3, middle, $container-type: both); }
#divBBC { @include grid-unit(1/2 1/3 fullrow, fullrow, $container-type: contained); }
#divBC { @include grid-unit(1/2 1/3, last, $container-type: contained); }
{% endhighlight %}

</div>

<p class="note">Note that you can interchange between the integer columns numbers and the fractions. Of course that using always the same base is much easier.</p>

The grid supports two modes of width calculation, the absolute or relative (default).
All the examples above, where using the relative mode.

For more information check the documentation of the $unitgs-settings-grid-unit-width-resolution-mode and the mixins grid-fractions-to-columns, grid-fractions-to-columns-relative and grid-fractions-to-columns-absolute.

If you don't supply a value to the parameter, it set the value to fullrow, that will occupy the entire row.

To change the default value set the $unitgs-settings-grid-unit-default-width to your choice.

### $position

The position parameter indicates the position in the current row.

Possible values:
- fullrow - will occupy all the row.
- first - (default) the first column in the row.
- middle - a middle column in the row.
- last - the last column in the row.

Below is on explanation of what each option makes:

#### fullrow

This will make the unit to occupy the whole row.
If the $unitgs-settings-use-clear is active (it is by default), it will force a clear:both.

#### first

This indicates the grid that it is the first unit in the row.
If the $unitgs-settings-use-clear is active (it is by default), it will force a clear:left to ensure that is nothing its left.

#### middle

This indicates the grid that it is an middle unit in the row.
It will not apply clears.

#### last

This indicates the grid that it is the last unit in the row.
It will not apply clears.

Default value: $unitgs-settings-grid-unit-default-position: first.
You can change its default changing the $unitgs-settings-grid-unit-default-position.

### $margin-left and $margin-right

The margin left and margin right indicate the number of columnns that will be set as margin to the column.

You can use whole column units or fractional values. To understand better how it works, refer to the $width parameter.

<p class="atention">For nested columns, it is mandatory to have the $width defined because it will use the nested parent dimentions to calculate its dimentions.</p>

If no value is specified, no rule will be written to the css. If you want the value 0 to be written or you need to set the parameter to 0.
If you want to set it to the default value, set the parameter to default.

{% highlight sass %}
@include grid-unit($margin-left: 0, $margin-right: default);
{% endhighlight %}

Default value: undefined.

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

### $container-type

Indicates where in the unit is located in the hierarchy.
It is one of the most important parameters because it controls, grid margins and unit gutters.

Possible values:
- none - (default) Indicates that it is a top level column that will not serve as a container.
- container - Indicates that this column is a container for nested columns.
- contained - Indicates that this column is included in another column.
- both - Indicates that this column is included in another column and is a container for other columns.

Below is an explanation of what each option makes:

#### none

It is a top level grid unit.
It is not contained by any other unit.
It will contain content, not other units.
It will define gutters.
Will make the grid to apply margins to the unit if it is a first, last or is a fullrow unit and it has inactive columns.

#### container

It is a top level grid unit.
It is not contained by any other unit.
It will contain other units, not content.
It will not define gutters.
Will make the grid to apply margins to the unit if it is a first, last or is a fullrow unit and it has inactive columns.

#### contained

It is not a top level grid unit.
It will contain content, not other units.
It will define gutters.
Will not make the grid to apply margins.

#### both

It is not a top level grid unit and not the last.
It will not contain content, but other units.
It will not define gutters.
Will not make the grid to apply margins.

This is the most raw/basic type of unit, because it does not apply margins or gutters, it is the most simple container, it will still apply the clearfix.

The grid will try to make assumptions on the nested position of the grid-unit. See the example below.

{% highlight sass %}
@include grid-unit(1/2 1/3);
@include grid-unit(1/2 1/3, $contaiter-type: container);
{% endhighlight %}

In the first line the container type will be changed to contained and in the second line to both, because by the width parameter it infers that it is a contained unit.

Default value: none.

You can change the default value to change the $unitgs-settings-grid-unit-default-container-type to change the grid default behaviour. This migth be useful if you like to have a main container, and then the other inner units, in this scenario, it would be practical to change the default value to contained.

### $align

The aligh parameter allows you to control the float parameter in the units. It is useful in some more specific scenarios with irregular grids.

Possible values:
- left - (default) It applies a float left to the unit.
- right - It applies a float right to the unit.

Default value: left.

### $font-size

The font-size is set in unitless relative values to the base font size that you set in the settings mixin, imagine it as a rem over your settings.

The font-size in an elastic design is a very important value, because it defines the relative value of the dependent elements.

For example, if you want the container font size to be 2 times bigger than the base font size, you will write the following:

{% highlight sass %}
@include grid-unit($font-size: 2);
{% endhighlight %}

If the base font size was 1.25em (20px), this will make it 1.25em\*2em (40px).
Although it looks a relative simple setting, it will make the dimentions to be adjusted for that unit and all its contained units.

In the example above, the line height, margins, paddings, gutters, etc. all need to be scaled so that they maintain their original dimentions.

In the case of nested units, the grid becomes even more important.

{% highlight sass %}
@include grid-unit($font-size: 2 1.5 1);
{% endhighlight %}

You pass the list of the font-sizes of the parent containers, being the last value the font-size that you want to have. All the values are relative to you base font size, you don't need to make any calculations, the grid will do it for you.

Can you easily calculate in ems the dimentions of the left gutter of your current grid unit? ... probably not that easily, but you can relax because the grid does all the hard work. ;)

Default value: 1.

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

### $line-height

Allows to specify the ratio between the font-size and the line. Although you have the option to set it, that value will be adjusted to keep the vertical rythm. See the fit-method for your options to control it.

Default value: $unitgs-settings-base-line-height.

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

### $height

You can define a specific height for an grid unit, just set the value in number of lines.

The following example sets grid unit height to 2 lines.

{% highlight sass %}
@include grid-unit($height: 2);
{% endhighlight %}

<p class="note">Note: You cannot use fraction of lines.</p>

Default value: undefined.

### $gutter

Defines where we want the gutters.

<p class="note">Note: It only applies for container-type none or contained.</p>

Possible values:
- none - Removes the gutters from the column.
- left - Set only the left gutter.
- right - Set only the right gutter.
- both - (default) Sets both gutters.

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

**example description**

{% highlight sass %}
{% endhighlight %}