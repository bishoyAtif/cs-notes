# Responsive Images
- It's all about loading different image sizes or resolutions to fit the context and the device used without using much bandwidth "specially for mobile devices".
- In the ```<head>``` of the document you'll find the line ```<meta name="viewport" content="width=device-width">``` this forces mobile browsers to adopt their real viewport width for loading web pages (some mobile browsers lie about their viewport width, and instead load pages at a larger viewport width then shrink the loaded page down, which is not very helpful for responsive images or design.

## Switching Resolutions and sizes
- if you want to display identical image content, just larger or smaller depending on the device.
  ```html
  <img srcset="elva-fairy-320w.jpg 320w,
              elva-fairy-480w.jpg 480w,
              elva-fairy-800w.jpg 800w"
      sizes="(max-width: 320px) 280px,
              (max-width: 480px) 440px,
              800px"
      src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
  ```

## Switching Resolutions with the same size
- If you're supporting multiple display resolutions, but everyone sees your image at the same real-world size on the screen, you can allow the browser to choose an appropriate resolution image by using srcset with x-descriptors.
  ```html
  <img srcset="elva-fairy-320w.jpg,
               elva-fairy-480w.jpg 1.5x,
               elva-fairy-640w.jpg 2x"
       src="elva-fairy-640w.jpg" alt="Elva dressed as a fairy">
  ```
  ```css
  img {
    width: 320px;
  }
  ```
- The css used is to restrict the width of the images.
- In this case, sizes is not needed — the browser simply works out what resolution the display is that it is being shown on, and serves the most appropriate image referenced in the srcset. So if the device accessing the page has a standard/low resolution display, with one device pixel representing each CSS pixel, the elva-fairy-320w.jpg image will be loaded (the 1x is implied, so you don't need to include it.) If the device has a high resolution of two device pixels per CSS pixel or more, the elva-fairy-640w.jpg image will be loaded.
  > CSS pixel doesn't always equal to Hardware pixel "actual device width" [why?](http://bit.ly/2FJTWd0)

## Art direction
- Explicitly tell the browser which picture to serve on different screen sizes.
  ```html
  <picture>
    <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
    <source media="(min-width: 800px)" srcset="elva-800w.jpg">
    <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
  </picture>
  ```
## Responsive images with srcset vs. picture
- As a web designer or developer, you have no way of knowing how much bandwidth the user currently has or if they’ve declared some sort of preference for the density of images they want. If we provide browsers with information via ```srcset``` and ```sizes``` then browsers can make smarter decisions about the appropriate image source.
- But none of that is possible when you use the ```<picture>``` element and its ```media``` attributes.
- When you specify the media queries for sources, you are providing rules to the browser that it must follow. The browser has no discretion to make smart decisions about what to download based on user preference, network, etc.
- ```<picture>``` tag is used when solving art direction problem while ```<img>``` tag with ```srcset``` attribute should be used with resolution switching problems.
- For more info read this [article](http://bit.ly/2FK3vsC).