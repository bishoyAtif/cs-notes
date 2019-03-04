# Basic Terms

## Charsets and Character Encoding

- Character set is a defined list of characters recognized by the computer hardware and software. **Each character is represented by a number**. For example, ASCII and Unicode.
- [ASCII Charset](https://www.commfront.com/pages/ascii-chart) represents one character in a byte. For example, Character 'A' in ASCII is represented with 01000001 "65".
- Since there are character sets with more than 256 characters in the character set one cannot in general simply say that each character is a byte.
- Another charset is Unicode. Every platonic letter in every alphabet is assigned a magic number by the Unicode consortium which is written like this: U+0639. This magic number is called a **code point**. The U+ means “Unicode” and the numbers are hexadecimal. There is no real limit on the number of letters that Unicode can define and in fact they have gone beyond 65,536 **so not every unicode letter can really be squeezed into two bytes**. Unicode just presents the characters into numbers and it says nothing about how these numbers should be implemented in a computer memory.
- Character encoding is how to encode characters included in the charsets into sequences of bytes "actual bytes in the memory".  For example, UTF-8 or windows-1252.
- ASCII was encoded in early days in one byte "the number represented by the charset" so it can be considered also an encoding "just in the range of 0-127".
- UTF-8 uses 1 byte when encoding an ASCII character, giving the same output as any other ASCII encoding. But for other characters, it will use the first bit to indicate that a 2nd byte will follow.
- When you encode your data, you use an encoding, but when you decode data, you will need to know what encoding was used, and use that same encoding to decode it. So **It does not make sense to have a string without knowing what encoding it uses**.
- Mojibake problem happens when you encode the string in a specific encoding and decode it with a different one. It can interpret a char encoded in two-byte-encoding as two chars in one-byte-encoding.
- For more info, check [What is character encoding and why should I bother with it](https://stackoverflow.com/a/31760986/6273509) and [The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and Character Sets](http://bit.ly/2RdHVC8)

## Mime Type

- A MIME type is a label used to identify a type of data. It is used so software can know how to handle the data. It serves the same purpose on the Internet that file extensions do on Microsoft Windows.
- So if a server says "This is text/html" the client can go "Ah, this is an HTML document, I can render that internally", while if the server says "This is application/pdf" the client can go "Ah, I need to launch the Foxit PDF Reader plugin that the user has installed and that has registered itself as the application/pdf handler."
- You'll most commonly find them in the headers of HTTP messages (to describe the content that an HTTP server is responding with or the formatting of the data that is being POSTed in a request) and in email headers (to describe the message format and attachments).
- For more info check [Mime & Content-Type](https://youtu.be/FBkZ2TJZZUY)

## JWT

- A JSON Web Token (JWT) is a JSON object that is defined as a safe way to represent a set of information between two parties. The token is composed of a header, a payload, and a signature. Simply it is a string with the format ```header.payload.signature```
- The authentication server then creates the JWT and sends it to the user. When the user makes API calls to the application, the user passes the JWT along with the API call. In this setup, the application server would be configured to verify that the incoming JWT are created by the authentication server and not faked or temered with.<br>
<img src="https://i.ibb.co/0K3SxH8/1-SSXUQJ1d-Wji-Ur-Do-Kaai-GLA.png" style="float: right;width: 40%;">
- The header component of the JWT contains information about how the JWT signature should be computed. The value of the “typ” key specifies that the object is a JWT, and the value of the “alg” key specifies which hashing algorithm is being used to create the JWT signature component.

  ```json
  {
      "typ": "JWT",
      "alg": "HS256"
  }
  ```

- The payload component of the JWT is the data that‘s stored inside the JWT (this data is also referred to as the “claims” of the JWT). There are several different standard claims for the JWT payload, such as “iss” the issuer, “sub” the subject, “userId” to mark the user and “exp” the expiration time.
- What this algorithm does after that is base64url encoding the header and the payload created previously. The algorithm then joins the resulting encoded strings together with a period (.) in between them. Then the data string is hashed with the secret key using the hashing algorithm specified in the JWT header. The resulting hashed is then base64url encoded to produce the JWT signature. Then we simply need to combine the components, with periods (.) separating them.
- It is important to understand that the purpose of using JWT is **NOT to hide or obscure data in any way**. The reason why JWT are used is to **prove that the sent data was actually created by an authentic source**.

## CORS

### Origin

- Origin syntax is ```<scheme> "://" <hostname> [ ":" <port> ]```.
- An origin is composed of the scheme, the host name and the port. For example, ```http://www.example.com/dir/page2.html``` and ```http://www.example.com/dir2/other.html``` are from the same origin. ```http://www.example.com:81/dir/other.html``` and ```http://www.example.com/dir2/other.html``` are different.

### Same Origin Policy

- Browsers implement something called "Same-origin Policy" (SOP).<img src="https://cdn-images-1.medium.com/max/1600/1*g_ISMQPCQpjw-6w3JRFUKQ.png" style="float: right;width: 40%;">
- It pervents the browser from executing XMLHttpRequests and some other requests "mentioned below" from cross origins. As it can contain many vulnerabilities like csrf "Making blind requests to cross web site depending that there are registered cookies for those web sites".
- In other words, Two websites can load each others contents "Using Ajax Requests" only if they are both from the same origin "Same Origin Requests". But if the origins of the two sites differ, loading content from each other "Cross Origin Requests" is not permitted, unless we use CORS or another technique to poke little holes into the SOP.
- SOP is not to protect the resources requested on a server, that task is up to the server itself via other means. **The point is to protect the innocent user**.
- It isn't to stop people from accessing website content generally. if somebody wants to do that, they don't even need a browser. The point is to stop client scripts accessing content on another domain without the necessary access rights. The scenario is the following:
  - You go to website X.
  - The author of website X has written an evil script which gets sent to your browser.
  - That script running on your browser logs onto your bank website and use your stored cookies to do evil stuff and because it's running as you in your browser it has permission to do so.

#### Which corss-requests are blocked by SOP

- Invocations of the XMLHttpRequest or Fetch APIs in a cross-site manner.
- Web Fonts (for cross-domain font usage in @font-face within CSS).
- WebGL textures.
- Images/video frames drawn to a canvas using drawImage().

### Cross-Origin-Request-Sharing "CORS"

- It’s a way to relax security and make it less restrictive. SOP is implemented in almost all modern browsers and because of that, a website from one origin is not allowed to access resources from foreign origins. CORS is a mechanism to make exceptions to SOP by allowing servers to specify who can access its assets or resources.
- It basically discards response in non-destructive non-authorized requests "Simple Requests" and blocks totally distructive non-authorized requests "Pre-Flighted Requests.

#### Simple Cross-Origin Requests

- A simple request must meet those conditions
  - Uses a GET, HEAD, or POST method
  - Don’t have headers other than the small subset defined in the specification (any custom or authorization header breaks this condition)
  - The only allowed values for Content-Type header are application/x-www-form-urlencoded, multipart/form-data, text/plain (application/json breaks this condition).
- If cross-origin ajax request occurs, the browser send ```Origin``` header with the value of the current request source and then it checks the response from the server. If it has ```Access-Control-Allow-Origin``` value that matches the origin sent, the response will be allowed normally, else it simply discards the response to block any info exposure **The Request is sent to the server but it's the server's responsibility to stop any unneccessary or dangerous requests**.

#### Pre-Flighted

- Breaking any conditions mentioned above "for example, Authorization header" causes the request to be preflighted.
- A pre-flighted request makes the browser first send an additional preliminary OPTIONS request (“preflight request”) in order to make sure that the actual request "pre-flighted request" is safe to send as it may be destructive or can modify the server resources "for example, DELETE and PUT methods requests users pre-flighted requests".
- The browser first sends an OPTIONS request with three additional parameters ```Origin```, ```Access-Control-Request-Method``` the method requested and ```Access-Control-Request-Headers``` additional headers attached. Then the browser checks the server response and it should have ```Access-Control-Allow-Origin```, ```Access-Control-Allow-Methods```, ```Access-Control-Allow-Headers``` headers that match the request origin, method and headers. If it matches, the browser then sends the actual request, else it just discards the request totally.

## Web Server

- The primary function of a web server is to store, process and deliver web pages to clients. A user agent, commonly a web browser or web crawler, initiates communication by making a request for a specific resource using HTTP and the server responds with the content of that resource or an error message if unable to do so.
- Many generic web servers also support server-side scripting using Active Server Pages (ASP), PHP, or other scripting languages. This means that the behaviour of the web server can be scripted in separate files, while the actual server software remains unchanged. Usually, this function is used to generate HTML documents dynamically ("on-the-fly") as opposed to returning static documents. The former is primarily used for retrieving and/or modifying information from databases. The latter is typically much faster and more easily cached but cannot deliver dynamic content.
- Web servers are able to map the path component of a Uniform Resource Locator (URL) into:
  - A local file system resource (for static requests)
  - An internal or external program name (for dynamic requests)
- For a static request the URL path specified by the client is relative to the web server's root directory.
- Consider the following URL as it would be requested by a client ```http://www.example.com/path/file.html```. The client's user agent will translate it into a connection to ```www.example.com``` with the following HTTP 1.1 request:

``` http
  GET /path/file.html HTTP/1.1
  Host: www.example.com
```

- The web server on ```www.example.com``` will append the given path to the path of its root directory. On an Apache server, this is commonly ```/home/www``` (On Unix machines, usually ```/var/www```). The result is the local file system resource ```/home/www/path/file.html```.