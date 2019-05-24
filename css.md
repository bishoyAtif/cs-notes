# Introduction
- CSS "Cascading Style Sheets" is the language that styles the html page structure.
- CSS associates rules "Styles" with HTML elements.
- CSS Rule contains a selector to select html elements and a declaration "property and value" to style it. For example,
  ```css
  p { /* Selector */
    someProperty: value;
    aontherProperty: anotherValue;
  }
  ```
# Where to write css
- Inline css is written within HTML tags using the ```style``` attribute. As is ```<p style="color:red;font-size:30px">This is a paragraph</p>```
- Internal css is written within ```<style>``` tag in the ```<head>``` section.
  ```css
  <style>
    p {
      color:red;
      font-size:30px;
    }            
  </style>
  ```
- External css is written in a separate file with ```.css``` extention and linked to the HTML file using ```<link>``` tag. ```<link href="path/to/file" rel="stylesheet" type="text/css">```

# Selectors
- ```element {}``` selects all the elements that match the html tag specified.
- ```.cls {}``` selects all elements with class named ```cls```.
- ```p.cls {}``` selects all ```p``` elements with class ```cls```
- ```#some-id {}``` selects the element with id named ```some-id```
- ```* {}``` is called "universal selector". It selects every element in the page.
- ```parent descendant {}``` selects all the elements under a specific parent __recursively__.
- ```element + adjacent {}``` selects the first adjacent "the element after" of an element.
- ```element, another-element {}``` selects all elements specified.
- ```a[attribute="value"] {}``` selects an element with a specific attribute.
- ```a[attribute="value"][attribute="value"]``` selects elements with multiple attributes.
- ```element:nth-of-type(order)``` selects the nth element in each scope  with an index starting with 1.
- ```element>child {}``` selects the child for the element but doesn't select the element itself.
- ```element ~ adjacent {}``` selects all the adjacent elements of the element.
- Psudo Selectors 
  - ```element:hover``` selects the element when hovering over it.
  - ```a:visited``` selects the visited link.
  - ```a:active``` selects the active state of a link "the state when you click the link before redirecting".
  - ```element:first-child```, ```element:last-child``` selects the element when it's the last or the first child.
  - ```element:first-of-type```, ```element:last-of-type``` selects the first or the last element for any parent.
  - ```input:checked``` selects the checked checkbox or the radio button.
  - ```p::first-letter``` checks the first letter of the element.

# Specificity
- If an element inherits multiple styles from many selectors, then the applied style is the closest one to it.
- Type < Type Type < class < attribute < psudo class < id < inline
- ```ul``` < ```ul li``` < ```.highlighted``` < ```input[type="text"]``` < ```li:hover``` < ```#specific``` < ```<h1 style=""></h1>```
  > You can add ```!important``` after any property value to indicate that it should be considered more important than other rules that apply to the same element. Like ```p b { color:red !important; }```
- When using the same selector. the last rule is applied.
  - The latter declaration of a value will override the previous ones.
  - This works even on the included style sheets .. the latter file included will override the declarations of the previous ones. 
  - It can used to overwrite some values in frameworks like bootstrap by including the overwriting file after it

# Inheritance
- Any rule applied on a parent of many nodes affects all the children nodes.
- If element styling is made, it will overwrite the inherited style from the parent "Specificity".
- Some rules can't be inherited like border. But you can make the descendant inherit it by using inherit keyword after the rule.
  ```css
  body {border: 1px solid black;}
  p {border: inherit;}
  ```

# Representing Colors
- Absolute: ```red```, ```green```, ```purple```, ```black``` and so on.
- RGB: ```rgb(red-value, green-value, blue-value)``` Any value is an integer ranging from 0 - 255.
- HEX: ```#FF0055``` contains 6 digits hex number. Each ranges from 0 - F.
  - It can be represented by 3 digits. For example, #0F2 equals #00FF22. 
- RGBA: ```rgba(red, green, blue, trasparency "0->1")```

# Font Units
- ```#px``` sets the font to static number of pixels.
- ```#em``` dynamically takes a ratio of the font-size of the enclosing element.
- ?rem //Takes a ratio of the root element.

# CSS Properties
## General
- ```color: colorValue;```

## Background
- ```background-color: color;```
- ```background-image: url('path/to/image');```
- ```background-repeat: value;``` selects the repetition criteria for the background image.
  - ```repeat``` It's the default value. It repeats the background on both x and y axis. 
  - ```no-repeat``` doesn't repeat the background image.
  - ```repeat-x``` repeats the background image for the x axis only.
  - ```repeat-y``` repeats the background image for the y axis only.
- backfround-attachment: scroll(default) || fixed
- background-position: X% Y% >> makes the center of the background image as a percentage of the div height and width.
- background-size
  - cover //Stretches the image to cover all the html vertically and at least the the page full screen. 
  - contain //Resizes to contain all your html entities.
- background: url() || none _ repeat mode _ Position _ Attachment _ Color //One line declaration.

## Border
- ```border: widthpx color style;```
- ```border-color: color;```
- ```border-width: width-in-pixels;```
- ```border-style: solid | dashed;```

## Font
- ```font-size: size;```
- ```font-family: "Font Name";```
- ```font-weight: normal | bold;```
  > The weight of some fonts can be assigned to a numeric value ranging from 100 - 800 with 100 step. Like 100, 200, 300 and so on.
- ```line-height: height-ratio;``` multiplies the base height of the font with the ratio specified.
- ```letter-spacing: #;``` sets the number of pixels between each letter.

## Text
- ```direction: ltr | rtl```
- ```text-decoration: underline | overline | line-through | blink```
- ```text-transform: uppercase | lowercase | capitalize | inherit | initial```
- ```text-align: center | left | right```
  
# CSS Box Model
- Each element is represented as a rectangular box, with the box's __content__, __padding__, __border__, and __margin__ built up around one another like the layers of an onion.
- You should think as if there is a box around each CSS element. For the block-level elements, The box takes all the line it is on. But the inline-level elements can be part of the line.
- __content__ is the box of the actual data, text or image placed within the element.
  - manipulating ```width``` or ```height``` attributes edits the size of the content box. It can be a ratio of its parent element. Like ```width: 30%;```
- __padding__ represents the inner margin of a CSS box — the space between the outer edge of the content box and the inner edge of the border. 
  - Shortcut for declaring the four sides. ```padding: ?px ?px ?px ?px``` clockwise from the top.
  - ```padding: 1px 2px``` will make the top and the bottom sides 1px padding and will make the left and the right sides 2px padding.
- __border__ is sitting between the outer edge of the padding and the inner edge of the margin.
- __margin__ represents the outer area surrounding the CSS box, which pushes up against other CSS boxes in the layout.
- You can manipulate margin, border and padding by using ```boxProperty-direction: #px```. Like ```margin-top```, ```margin-left```, ```border-right```, ```padding-left``` and so on.
- Use ```auto``` for the side that you want css to style it dynamically.
- ```float: left | right | none | inline-start | inline-end``` specifies the direction that an element should be placed within its container.