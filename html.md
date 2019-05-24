## Introduction
- HTML was created first at 1989/1990 to exchange papers with formatted structure and send it as a text.
- HTML code is made up with elements, each one of them often has two tags.
- A general rule to write html elements is ```<openingTag attribute="value">Some Content</closingTag>```
- Each element acts like a container that tells the browser info about the information between its two tags.
- There are some elements that don't have any text or other elements within and usually have one tag between them called "Empty tags" or "Self closing tags". Like ```<image>``` and ```<br>```
- Attributes provide additional info about the content of the element, it is put in the opening tag. Like ```<openingTag attribte="value">```
- You can declare custom data attributes for any tag by using ```data-attribute="value"```
- Structural VS. Semantic Elements
  - Structural elements is used just to structure a web page element like a paragraph or a list.
  - Semantic elements is not intended to affect the structure of the web page but it adds more information about the element. It helps with SEO and Screen readers. It also helps adding more hooks for html elements to be used by CSS.
  - You shouldn't use the semantic tags to style the text. Use it only to give the text a meaning you want.

## HTML Page Structure
```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Meta data, title, styles, fonts and scripts -->
  </head>
  <body>
    <!-- Content elements of the page -->
  </body>
</html>
```
- DOCTYPE declaration is used to tell the browser which HTML version to render. ```<!DOCTYPE html>``` at the top of the page renders it as HTML5 page.
- ```<html>``` indicates that the enclosing elements are treated as html code.
- ```<head>``` provides meta data for the page "styling, encoding, header scripts and so on".
- ```<body>``` indicates that the enclosing elements are put in the main browser window "things that appear into your web page".
- You can comment a line in HTML by using ```<!-- Line Commented -->```

## Basic Elements
### General
- ```<title>``` is placed in the head element and refers to the title of the page that appears on the page tab and it also affects SEO.
- ```<meta>``` adds meta data to the html page. For example, ```<meta name="description" content="My Webpage Description">``` adds a descripton to the page to improve SEO for it.

### Text
- ```<h1>``` --> ```<h6>``` larger to smaller. h1 is the main header in your page. Manipulating them affect SEO of the page.
- ```<p>``` is a paragraph tag. Browser will automatically views it in a single line.
  > Warning: When the browser comes across two, more white spaces or even a line break, It only shows one space. That is known as "White space collapsing".
- ```<i>```, ```<em>``` to make the text italic.
- ```<b>```, ```<strong>``` to make the text bold.
- ```<ins>``` to underline "insert in semantics point of view".
- ```<del>``` to strike out "delete in semantics point of view".
- ```<small>``` to make the text small.
- ```<mark>``` to highlight the text.
- ```<sub>``` to sub-script the text.
- ```<sub>``` to super-script the text.

### Breaks
- ```<br>``` adding a line break inside a paragraph.
- ```<hr>``` creates a horizontal rule "line" to split the content.

### Lists
- you can create ordered list using ```<ol>``` or un-ordered list using ```<ul>```
  - ```<li>``` is used to represent add a list item.
  - A nested lists can be made by defining a new list within the ```<li>``` tag.
- ```<dl>``` is used to create a definition list that includes a series of terms and definitions.
  - ```<dt>``` : definition term.
  - ```<dd>``` : definition itself.

### Links
- A link is defined using ```<a>``` tags "anchor tags".
- ```<a>The text that the user clicks on</a>```
  - ```href="URL"```
  - ```target="_self"``` opens the link in the same tab or ```target="_blank"``` to open the link in another tab.
- URL types
  - Absolute URL is the url that you enters to get the web page directly. "http://google.com"
  - Relative URL is the url for a specific page relative to another page in your website, the root directory for example.
    - Within the same directory ```"bisho.html"```
    - Within a child directory ```"child_dir/bisho.html"```
    - Within a parent directory ```"../bisho.html"```
- To make a link to send an email directly we use ```href="mailto:example@gmail.com"```.

## Classes VS IDs
- Id attribute is used as unique identifier for it. The same id shouldb't be declared more than once in the same page. ```<element id="custom-id">Some Elements</element>```
- Class attribute is used to classify many tags for multiple selection. ```<element class="custom-class">Some Elements</element>```
- You can go to a specific section with a specific id in the same page by using a link with attribute ```href="#target-id"``` or to redirect to the page directly using url with ```#target-id``` at the end of it.

### Images
- ```<img>``` is used to add an image to your page.
  - ```src="url-for-the-image"```
  - ```alt="text for screen readers or if the image can't load"```
  - ```title="text appears when the user hovers over it"```
- Preparing Images
  - Use GIF or PNG for the photos that have flat colors "Logos or Illustrations".
  - Use JPEG for the photos that have varity of colors "Photographs".
  - Images created for the web should be saved at the resolution of 72 ppi. Making the images with higher resolution than 72 ppi will result in only a larger image not a higher quality image.
  - Vector images are resolution independent. It is created by placing points on a grid and drawing lines between those points. You can resize image as you want without affecting the quality of the image. Vectors are used in the web using SVG Format "Scalable Vector Graphics".
- You can use ```<figure>``` tags to add images with their caption.
  - ```<figcaption>``` tags can relate a caption with the image within ```<figure>``` tags.
  - For example
    ```html
    <figure>
      <img src="tea.jpg" alt="Tea cup with steam and pen on bed">
      <figcaption>Journaling with Tea</figcaption>
    </figure>
    ```

### Tables
- ```<table>``` tags are used to declare a table. The table is drawn row by row.
- ```<tr>``` declaring a table row. It indicates the start of each row.
- ```<td>``` declaring a table data "cell". It is usually put within table row.
- ```<th>``` declaring a table heading data. It makes the text bold to indicate it's a table heading data.
- Starting from HTML5, New tags to improve semantics are added.
  - These elements are used to help screen reader improvement, add more hooks to be used with css and to improve SEO for the page.
  - ```<thead>``` includes the heading of the table.
  - ```<tbody>``` includes the body of the table.
  - ```<tfoot>``` includes the footer of the table.

### Block-level VS Inline-level Elements
- Block-level elements always appears on a separate line. It can't have any tag with it on the same line. Like ```<p>``` or ```<h1>``` tags.
- Multiple inline-level elements can appear on the same line with other inline-level elements or within another block-level elements without requiring to be in a new line.
- ```Div``` VS. ```Span``` elements
  - They are just generic containers to group many elements. They have no benifits until using css on them.
  - ```<div>``` is a block-level element to select them with css once.
  - ```<span>``` is the inline-level equivalent of the ```<div>``` element.

### Forms
- HTML Form is a way to send user inputs to the server side.
- The form is sent to the server as key/value pairs.
  > You should never change the name of the form control in the page without making sure that the server knows the new value.
- ```<form>``` tag includes all the form controls.
  - ```action="URL"``` to specify the url of the page on the server to send the form data to.
  - ```method="method"``` the ```method``` can be ```get``` or ```post```
  - #### Get VS. Post
    | GET | Post |
    | --- | ---- |
    | parameters in the url | parameters in the request body |
    | used for fetching documents | used to update the server data |
    | has maximun length of 2048 byte | has maximun length of 8MB |
    | must haven't sensitive information | acceptable to have sensitive information |
    | can be cached or bookmarked | can't be cached or bookmarked |
    | used for fetching documents | used to update the server data |
    For more info, Check [Get VS. Post](https://goo.gl/J5nQP9).
- ```<input>``` tag is used to make a form control to get info from the user.
  - Any form control must have ```name``` attribute. It's the key to the value sent to the server.
  - Any form control can have ```value``` attribute to specify initial "default" value for it.
  - Text form controls can have ```placeholder``` attribute to make a temporary text before typing. It doesn't work when using ```value``` attribute.
  - ```maxlength``` attribute to control the max number of characters.
  - There are many types for the input for different type of values.
  - #### Input Types
    - ```<input type="text">``` used for plain text inputs.
    - ```<input type="password">``` used for passwords.
      > For full security, you should have SSL certification to make the request using https not http and encrypt the data before sending it to the server.
    - ```<textarea> Default Text </textarea>```
      - ```wrap="off"```  will make a horizontal scroll bar if the text is longer than the area.
      - ```wrap="soft"``` will make a new line automatically if the text was longer but the input is read without that newline (Default).
      - ```wrap="hard"``` will make a new line automatically if the text was longer and the input is read with those new lines.
    - ```<input type="radio">```
      - value="the value sent to the server if this button is checked"
      - checked. used to indicate which value should be selected by default.
        > The value of the name attribute must be the same for every radio button in the selection group.
    - ```<input type="checkbox">```
      - ```value=""``` indicates the value sent to the server if this button is checked.
      - ```checked``` indicates which value should be selected by default.
        > If many checkboxes are checked with the same name it will return the value of the last checked one
        If you want to return all the values of them type the name as an array and treat the input as an array.
        e.g. ```<input type="checkbox" name="time[]">```
    - ```<select>``` tags is used to make a select box.
      - ```multiple``` to use multiple selection.
      - ```size="#"```. The number of fields shown in the multiple mode.
        > When multiple selection is used , an array name must be used for the name attribute and it is treated like checkbox.
      - ```<option> Option Name </option>``` Used to create option within the ```<select>``` tags.
        - ```selected``` indicates which value should be selected by default.
        - ```value=""``` the valueto be sent to the server when selecting this option.
    - ```<input type="file">``` Create a browse button that selects a file from the client device.
      > You must make form attributes ```method="post"``` and ```enctype="multipart/form-data"``` to submit a file.
    - ```<input type="submit" name="submit_button_name">```. Standard submit button.
    - ```<input type="hidden">``` Used to sent additional hidden information to the server.
        > Never treat hidden inputs as secure.
    - ```<input type="date">``` makes a special select box to select a date.
    - ```<input type="email">``` The user must enter a valid email.
    - ```<input type="url">``` The user must enter a valid url.
    - ```<input type="search">``` Adds a cross beside the search box to clear the text.
    - ```<input type="color">``` Selects a color from the color palette.
- ```<fieldset>``` tags are used to group form controls together. It will render a border around the fieldset.
- ```<legend>``` tags are used to specify a caption for a group of the form controls. It's added at the top of ```<fieldset>``` tag.
- Label make input fields selectable when clicking on any text between label tags. Also improve screen readers. You can add a caption to the input tags with them. You can add them by using two methods.
    - ```<label>Label text <input type="text"></label>```
    - You can pair a label with id by using the syntax ```<label for="input-id">Caption</label>```
- Validation
  - Notify the users about the problems in the form before submitting it to the server.
  - ```required``` The user can't submit the form with this field empty.
- General Attributes
  - ```autocomplete``` By default it is "on" can be set to the entire form or a specific input element.
  - ```autofocus``` By default it is "off" selects the input element to directly write within it.
  - ```formaction```, ```formmethod```, ```formtarget``` >> override the form attributes for a specific submit button.
- ```<button>``` tags are used to style the submit buttons better than ```<input>``` tag, allows other elements to appear within it. Also It can submit forms.
  - ```type``` attribute can be ```button``` to stop form submittion behaviour.

### Iframe
- ```<iframe src="URL"></iframe>``` it's used to show another web page within the original page. It is an abbreviation for Inline Frame.

### Miscellenious
- ```<blockquote>``` is a semantic tag that tells the browser that is a quote. The text will be indented and it helps to catch the quotatins in your site by the search engines.
  - ```cite="who-said-the-quote"```
- ```<q>``` is used to make short inline quotation.
- ```<abbr>``` is used for abbriviations.
  - ```title="full-term"```
- ```<cite>``` is used when referencing a piece of work such as a book or a film. It is rendered as italic text.
- ```<dfn>``` is used when adding a new terminology "definition instance"
- ```<address>``` is used to contain the conatct info of the page author like physical address or email.

## HTML Entities
- Takes the form ```&code;``` eg. ```&copy;``` for copyright symbol.
  > Check the appearance of the symbol after inserting it as some fonts can't display some symbols.
- For the full list, Check [Html entities list](https://www.freeformatter.com/html-entities.html).

## More HTML5 elements
- ```<header>``` used for the header of the page.
- ```<footer>``` used for the footer of the page or an article.
- ```<nav>``` used for the navbar or the sidebar of the page "Navigation".
- ```<article>``` used as a container for a blog post or an article.
- ```<section>``` used as a container for splitting sections. eg. featured articles, recent articles and so on.
- ```<aside>``` used for creating secondery tags not so related with the current blog post.
- ```<time>``` used to wrap timestamps to give them semantic meaning