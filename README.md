# Tequilla

If everyone else can name their sass modules after alcoholic beverages, why don't I
do it too?

## Whats under the hood?

### Basic mixins

#### Define type scale
```
@include define-type-scale((
    scale: 1.414,
    base-size: 1,
    base-weight: 400,
    line-height: 1.45
));
```
Requires [math module](https://github.com/sass-eyeglass/eyeglass-math)

Set up font scaling on your webapp using http://type-scale.com/
If you have a designer, ask them to provide you with a link from this site (if not, grab it yourself) - it should resemble:
http://type-scale.com/?size=16&scale=1.414&text=CSS%20Architecture%20for%20large-scale&webfont=Libre+Baskerville&font-family=gotham&font-weight=400&font-family-headers=&font-weight-headers=inherit&background-color=white&font-color=%23333
The options array takes the same parameters as $type-scale, defaults are defined in $type-scale-base;

### Generators

#### Angle
```
.class-name {
    @include angle(after, false, 1.5deg);
}
```
Angle is a mixin for drawing slanted boxes (because svgs are annoying to maintain).
It takes 3 parameters, the first is the pseudo selector that the slanted section
should be placed onto; before, after or both.

The second parameter if whether the angle should be flipped or not, depending on
which direction you want the slant to go.

The third and final parameter is the angle at which you want the slant to go.

This feature was taken from
[here](https://viget.com/inspire/angled-edges-with-css-masks-and-transforms)

#### Arrow
```
.class-name {
    @include arrow(up, 10px, red);
}
```
This mixin is used to draw arrows on blocks, and takes the parameters: the direction:
which way you want the arrow to point (up, down, left or right); the size:
how big you want the arrow to be and the color that you want the arrow to be.

#### Color set
```
@include color-set(btn, $color-map, true);
```
Color set is a mixin for generating a set of something e.g. buttons. The first
argument is what you want to prepend all of your color scheme classes with (for
buttons it could be btn), the second parameter is a map of all of the different
colors that this component can be (e.g. ( "primary": red, "secondary": blue) for
generating "btn-primary" and "btn-secondary classes"). The third param is whether
this block has a hover state, if your component has hover states you will need to
assign two colors to your map, the first being the neutral state and the second
being the hover state.

### Bullets
```
ul {
    @include bullets(circle, 2em, pink);
}
```
UNSTABLE

Bullets is a mixin to style bullet points, because CSS does not let us style bullet
points easily. With this mixin you can easily style bullet points, changing their color,
size and shape simply by changing the three parameters in the mixin.

As I have mentioned, this feature is really unstable and the maths behind it is pretty weird.

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
    @include pseudos() {
        color: red;
        ...
    }
}
```
For applying styles to the hover, focus and active pseudo selectors at the same time.
Styles for these are placed within the curly braces after the parentheses.


#### Selection

```
@include selection() {
    color: red;
    ...
}
```
For manipulating the visual styling of the `:selection` pseudo element.


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

## Flexbox

Instead of rewriting an entire grid system with fixed sizes (bootstrappy col-md-6 kind of stuff)
I decided to take a freer approach to the grid system in a similar way to susy

You can set options for the flex grid to use by overwriting the map called `$full-flex`
this holds all of the options for the flex grid itself like gutters and things.

### Flex row
 ```
    @include flexrow(stretch);
 ```
`Flexrow` creates a block which displays flex with fallbacks. It also adds negative margin
 around the block. The argument this mixin takes is optional, but if set, changes the flex align of the block


### Flex col
```
    @include flexcol(1, baseline);
```
`Flexcol` sets up an item within a flexrow, the first argument is how much space
the block should take up. Setting this to 1 will allow the block to take up 100%
of the space available to it, meaning that if it is on its own, it will be 100%
of the width. It also means that if you have two of these blocks,
they will take up 50% each, 3 will take up 33.33 respectively, 4, 25% and so on.

You can also set the first argument to either a percentage or a fraction,
this will fix the block to take up this much space and this much space only,
even if there are no more elements or multiple elements

The second argument is optional, pass an alignment to set a particular alignment
on this block (uses align-self)

### Flex col at
```
    @include flexcol-at(1, 300px, baseline, false);
```

Soft requires breakpoint

Same old Flexcol, hooked into breakpoints

The first argument is the same as it was in flexcol, can be 1, a percentage or a
fraction depending on what you want the col to do, the second argument is the breakpoint,
as with the other breakpoint mixins you can either pass a breakpoint to this value
or a max width value. The third argument is your alignment variable,
does exactly the same as the second argument for the normal `flexcol` mixin above
and is still optional. The final argument is the no breakpoint boolean,
used for when you do not have the breakpoint library

## Flexcol - in - depth

The mixins below are for the big features in flexbox


### Display flex
```
    @include display-flex();
```

This one simply sets a block to display flex, use this on the outer row. Flex row uses this

### Display inline flex
```
    @include display-inline-flex();
```

This one simply sets a block to display inline flex, use this on the outer row.

### Flex direction
```
    @include flex-direction(row);
```

This changes the direction that the row will use flex, this defaults to row. To
find out all of the options, see [this link](https://developer.mozilla.org/en/docs/Web/CSS/flex-direction).

### Flex wrap
```
    @include flex-wrap(nowrap);
```

This changes whether the row will wrap or not, this defaults to nowrap.
To find out all of the options, see [this link](https://developer.mozilla.org/en/docs/Web/CSS/flex-wrap).

### Flex flow
```
    @include flex-flow(row nowrap);
```

Flex flow is a shorthand way of calling flex direction and flex flow

For more information see [this link](https://developer.mozilla.org/en/docs/Web/CSS/flex-flow).

### Align items
```
    @include align-items(stretch);
```

This mixin aligns the flex items on the current flex line

For more information see [this link](https://developer.mozilla.org/en/docs/Web/CSS/flex-align).


### Align flex items
```
    @include align-flex-items(stretch);
```

This mixin aligns a flex container's lines within the flex container when there is extra space on the cross-axis.

For more information see [this link](https://developer.mozilla.org/en/docs/Web/CSS/align-content).

### Justify content
```
    @include justify-content(stretch);
```

This mixin aligns a flex container's lines within the flex container when there is extra space on the cross-axis.

For more information see [this link](https://developer.mozilla.org/en/docs/Web/CSS/align-content).

For more information see [this link](https://developer.mozilla.org/en/docs/Web/CSS/align-content).

### Flex
```
    @include flex(0, 1, 1);
```

The flex mixin is a quick way of making flex items, it takes three properties,
all of which are optional, the 1st is the flex grow property, the second,
flex shrink and the third, flex basis.

The flex grow property is the amount of the row you want this item to take up,
the flex shrink property states by which factor the block should be shrunk,
the flex basis sets the base size of the flex item

For basic usage of the flex mixin you should be able to get away with not passing
any arguments to the mixin, for more complex stuff you will need to get to grips
on what the grow, shrink and basis options do

For more information see [this link](https://developer.mozilla.org/en/docs/Web/CSS/flex)
and all will be revealed (hopefully).

### Flex order
```
    @include flex-order(3);
```

This mixin adjusts the position of a flex item, reordering it in the DOM

For more information see [this link](https://developer.mozilla.org/en/docs/Web/CSS/order).

### Align flex self
```
    @include align-flex-self(3);
```

This mixin works a lot like `align-flex` except it acts on a single flex item</p>

For more information see [this link](https://developer.mozilla.org/en/docs/Web/CSS/align-self">this link</a>.</p>



### Other

#### Parse font families
```
@include parse-font-families($font-1, $font-2, ...)
```

Takes infinite font families and makes sure they all have at least one fallback.
