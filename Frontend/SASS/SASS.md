# SASS

`Summary by Ahmad Wali Sharify`

<h2 style="color:purple">Syntactically Awesome StyleSheet </h2>

### Sass is a CSS pre-processor.
 - Sass reduces repetion of CSS and therefore saves time.
 - is a extension for CSS
 - Sass lets  you use features that do not exist in CSS, like variables, nested rules, mixins,  imports,  inheritance, built-in functions, and other stuff.

## Comments 
```
// or /*  */
```

<br>

## Variables 
---
 - Variables are a way to store information that you can re-use later.

 - Sass uses the $ symbol, followed by a name, to declare variables:

```scss
$variablename: value; 
```
Ex:
```scss
$myFont: Helvetica, sans-serif;
$myColor: red;
$myFontSize: 18px;
$myWidth: 680px;

body {
  font-family: $myFont;
  font-size: $myFontSize;
  color: $myColor;
}

#container {
  width: $myWidth;
}
```

<br>

## Nesting 

Sass lets you nest CSS selectors in the same way as html.

```scss
nav {
  ul {
    margin: 0;
       padding: 0;
    list-style: none;
  }
  li {
    display: inline-block;
  }
  a {
    display:    block;
    padding: 6px 12px;
       text-decoration: none;
  }
  &:hover {
  // it is hover for nav
  background-color: red
  }
}
```
Sass Nested Properties
Many CSS properties have the same prefix, like font-family, font-size, font-weight or text-align and text-transform.

```scss
font: {
  family: Helvetica, sans-serif;
  size: 18px;
     weight: bold;
}

text: {
  align: center;
     transform: lowercase;
  overflow: hidden;
}
```

<br>

## @use, @import
---
Sass keeps the CSS code DRY (Don't Repeat Yourself). One Way is to write code in a separate file.

You can create small files with CSS snippets to include with @use or @import in other Sass files. Examples  of such files can be: reset file, variables, colors, fonts, font-sizes, etc. 


Ex:

***reset.scss***
```scss
html,
body,
ul,
ol {
  margin: 0;
  padding: 0;
}
```
***standard.scss***
```scss
/* omit .scss */
@import "reset";

body {
    font-family: Helvetica, sans-serif;
    font-size: 18px;
    color: red;
}
```

<br>

## Partials 

By default, Sass Transpiles all the .scss files directly, if you don't want it. just use underscore before name of .scss file.
```
_filename.scss // a partial.
```
```scss
_colors.scss
$myPink: #EE82EE;
$myBlue: #4169E1;
$myGreen: #8FBC8F;  
```
standard.scss
```scss
@import "colors";

body {
    font-family: Helvetica, sans-serif;
    font-size: 18px;
    color: $myBlue;
}
```

<br>

## @mixin and @include
---

the `@mixin` directive lets you create CSS code that is to be reused throughout the app.
the @include directive is created to let you use `@include` the mixin.

```scss
@mixin mixin_name {
  property: value;
  property: value;
     ...
} 

selector {
  @include mixin-name;
}
```
Mixin accept arguments:

```scss
@mixin bordered($color, $width) {
border: $width solid $color
}
/* with default value */
@mixin borderd($color: blue ){
  border: 2px solid $color
}
```

<br>

## @extend and Inheritance 
---

the `@extend` directive lets you share a set of CSS properties from one selector to another.

it is useful if you have a major style, with additional styles for another.

```scss
.button-basic  {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

.button-report  {
  @extend .button-basic;
     background-color: red;
}

.button-submit  {
  @extend .button-basic;
  background-color: green;
  color: white;
}
```

<br>

## Themeing and Using CSS Varialbes
---
```scss
@use "sass:color";

$primary: yellow;
$red: red;
$third: black;
:root {
  --primary: #{$primary};
  --secondary: #{$red};
  --third: #{$black};
}

nav {
  a {
    background-color: var(--primary);
  }
  &:hover {
    background-color: color.scale($primary, $lightness:40%);
  }
}
```

<br>

## Links:
https://devhints.io/sass