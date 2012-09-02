---
name: unitgs-set-grid-settings
type: mixin
user-level: User
layout: post
---

# mixin unitgs-set-grid-settings

This mixin is used to set the grid-settings and pre-calculate values that the grid will use.

It does not emit output, so you can call it whereever you want but before the grid-init.

<p class="note">Note: It must be called before the unitgs-init-grid (or any other grid mixin or function). If you will not call it, the unitgs-init-grid will call it without parameters, applying the default values.</p>

<p class="atention">Atention: Always set the grid settings through this mixin, otherwise you run the risk of getting an unstable grid.</p>

## Declaration

{% highlight sass %}
@mixin unitgs-set-grid-settings(
	$number-of-columns: $unitgs-settings-number-of-columns,
	$number-of-active-columns: $unitgs-settings-number-of-active-columns,
	$font-size: $unitgs-settings-base-font-size,
	$line-height: $unitgs-settings-base-line-height,
	$gutter-width: $unitgs-settings-base-gutter-width,
	$use-last-right-margins: $unitgs-settings-use-last-right-margins,
	$use-clear: $unitgs-settings-use-clear
)
{% endhighlight %}

## Parameters

### $number-of-columns

Defines the number of total columns of the grid.

Default value: $unitgs-settings-number-of-columns.

### $number-of-active-columns

Defines the number of active columns for the grid.

Default value: $unitgs-settings-number-of-active-columns.

<p class="note">Note: Your design will always be relative to the number of active columns.</p>

### $font-size

Base font-size, by which all the other values will relate to.

Insert the value in unitless values.

<p class="example">Example: 1.25. This will make the font 25% bigger than the browser's default font size.
Normally we assume that the browser's default font size is 16px, but the user can always change it to his needs.
Assuming a 16px browser's default font size, setting $font-size to 1.25 will set the font-size to 1.25em that would represent a font size of 20px.</p>

Default value: $unitgs-settings-base-font-size.

### $line-height

Defines the ratio between the font-size and the line.
This value will define the vertical rythm for the grid.

<p class="example">Example: 1.6. This will create a line height that is 60% bigger than the font size specified in the $font-size parameter.</p>

Default value: $unitgs-settings-base-line-height.

### $gutter-width

Defines the size of the gutter relative to the $line-height.
The gutter is divided by the left and right padding.

<p class="atention">Atention: The gutters are elastic, not fluid, that means that they will always be in sync with the vertical rythm.</p>

<p class="example">Example: $gutter-width: 1.2. Will create a gutter that is 20% bigger than the value set in the $line-height parameter.</p>

Default value: $unitgs-settings-base-gutter-width.

### $use-last-right-margins

Indicates if the last column uses a margin.

This is will force a right margin on the grid-units that are last in the row, this will prevent any content to float to the right of the grid unit.

Default value: $unitgs-settings-use-last-right-margins.

### $use-clear

Indicates if the design uses the clear on the first and fullrow columns.

This will ensure that the column will be the first, forcing a clear left. 

Default value: $unitgs-settings-use-clear

## Examples

Lets declare a 14 columns grid, with 12 active columns (that means that you will have 12 columns to workwith and 1 column margin on eacd side).

{% highlight sass %}
@include unitgs-set-grid-settings(
	$number-of-columns: 14,
	$number-of-active-columns: 12)
{% endhighlight %}

Lets a standard 12 active columns grid, it will have no margins but the left gutter of the first column.
<p class="note">If you want to include a margin, you will have to do it <em>outside</em> the grid with a wrapper.</p>

We will also define the default font size as 20px and a line height of 1.6, that will originate in the init mixin a font-size of 1.2em and a line-height of 1.2.
Also we will include a smaller gutter of 0.8.

{% highlight sass %}
@include unitgs-set-grid-settings(
	$number-of-columns: 12,
	$number-of-active-columns: 12,
	$font-size: 20,
	$line-height: 1.2,
	$gutter-width: 0.8)
{% endhighlight %}

As you can see, it is very intuitive, just declare your intentions and the grid will obey! ;\)