# Tequilla

If everyone else can name their sass modules after alcoholic beverages, why don't I
do it too?



## Whats under the hood?


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
