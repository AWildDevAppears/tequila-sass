# Tequilla

If everyone else can name their sass modules after alcoholic beverages, why don't I
do it too?



## Whats under the hood?

### Generators

#### Angle
```
.class-name {
    @include angle(after, false, 1.5deg);
}
```
Angle is a mixin for drawing slanted boxes (because svgs are annoying to maintain).
It takes 3 parameters, the first is the psuedo selector that the slanted section
should be placed onto; before, after or both.

The second parameter if whether the angle should be flipped or not, depending on
which direction you want the slant to go.

The third and final parameter is the angle at which you want the slant to go.

This feature was taken from
[here](https://viget.com/inspire/angled-edges-with-css-masks-and-transforms)

### Utilities

#### Ghost vertical align
```
.class-name {
    @extend ghost-vertical-align;
    ...
}
```
Used for aligning the unknown to the center of a container.
More info can be [found here](https://css-tricks.com/centering-in-the-unknown/)


#### Psuedos

```
.class-name{
    ...
    @include psuedos() {
        color: red;
        ...
    }
}
```
For applying styles to the hover, focus and active psuedo selectors at the same time.
Styles for these are placed within the curly braces after the parentheses.


#### Selection

```
@include selection() {
    color: red;
    ...
}
```
For manipulating the visual styling of the `:selection` psuedo element.


#### Text hide
```
.class-name {
    @include text-hide();
    ...
}
```
For hiding the text within a container
(good for icons set on backgrounds for screen readers)

#### Hex RGBA

```
.class-name {
    background-color: hex-rgba(#eeeeee, .5);
}
```
This function is for adding alpha to a color that you only have the hex value
for.


### Other

#### Parse font families
```
@include parse-font-families($font-1, $font-2, ...)
```

Takes infinite font families and makes sure they all have at least one fallback.
