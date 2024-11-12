# Basic Terms

## Mime Type

- A MIME type "Content-Type Header in the response" is a label used to identify a type of data. It is used so software can know how to handle the data. It serves the same purpose on the Internet that file extensions do on Microsoft Windows.
- So if a server says in the http response "This is text/html" the client can go "Ah, this is an HTML document, I can render that internally", while if the server says "This is application/pdf" the client can go "Ah, I need to launch the Foxit PDF Reader plugin that the user has installed and that has registered itself as the application/pdf handler."
- You'll most commonly find them in the headers of HTTP messages to describe the content that an HTTP server is responding with or the formatting of the data that is being POSTed in a request "```enctype``` attribute in html" and in email headers (to describe the message format and attachments).
- For more info check [Mime & Content-Type](https://youtu.be/FBkZ2TJZZUY)
- ```enctype``` header within html form is the way you edit ```Content-Type``` header in the HTTP POST request. It can be one of two values:
  - ```application/x-www-form-urlencoded```: It's the default value. The body of the HTTP message sent to the server is essentially one giant query string name/value pairs are separated by the ampersand (&), and names are separated from values by the equals symbol (=). non-alphanumeric characters are replaced by `%HH', a percent sign and two hexadecimal digits representing the ASCII code of the character. So It turns any non-alphanumeric characters into 3 bytes and It wouldn't be efficient with large files.
  - ```multipart/form-data```: The type that allows file ```<input>``` element(s) to upload file "binary" data. It splits the payload into MIME messages each ended with a boundary separator that is assigned in the ```Content-Type``` header. This approach will not be efficient in the small "non binary" messages.
  - ```text/plain```: A type introduced in HTML5. It is intended to be human readable. They are not reliably interpretable by computer, So avoid using them.
  - For more info, check this [article](http://bit.ly/2Kz9wt3).

## JWT

- A JSON Web Token (JWT) is a JSON object that is defined as a safe way to represent a set of information between two parties. The token is composed of a header, a payload, and a signature. Simply it is a string with the format ```header.payload.signature```
<img src="https://i.ibb.co/0K3SxH8/1-SSXUQJ1d-Wji-Ur-Do-Kaai-GLA.png" alt="JWT Exchange Model" width="40%" align="right" style="margin: 15px">
- The authentication server then creates the JWT and sends it to the user. When the user makes API calls to the application, the user passes the JWT along with the API call. In this setup, the application server would be configured to verify that the incoming JWT are created by the authentication server and not faked or temered with.
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

- Browsers implement something called "Same-origin Policy" (SOP). ![CSRF Attack Model](https://cdn-images-1.medium.com/max/1600/1*g_ISMQPCQpjw-6w3JRFUKQ.png)
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

### JSONP "JSON With Padding"

- One way to overcome the restrictions of SOP is JsonP.
- There is one item that bypasses this limitation of SOP. It's ```<script>``` tag. When you use a script tag, the domain limitation is ignored, but under normal circumstances, you can't really do anything with the results, the script just gets evaluated.
- Here it the trick! When you make your request to a server that is JSONP enabled, you pass a special parameter that tells the server a little bit about your page. That way, the server is able to nicely wrap up its response in a way that your page can handle. For example ```http://www.example.net/sample.aspx?callback=mycallback```. Without jsonp, the normal response will be ```{ foo: 'bar' }``` but if the server has implemented jsonp, It will take the parameter ```mycallback``` and wrap it around the json returned. So It will become ```mycallback({ foo: 'bar' });```. As you can see, it will now invoke the method you specified. So, in your page, you define the callback function:
  ```javascript
  mycallback = function(data){
    alert(data.foo);
  };
  ```
- And now, when the script is loaded, it'll be evaluated, and your function will be executed.
- This technique is outdated. These days, CORS is the recommended approach vs. JSONRequest.

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

## Https
- Hyper Text Transfer Protocol Secure (HTTPS) is the secure version of HTTP, the protocol over which data is sent between your browser and the website that you are connected to. The 'S' at the end of HTTPS stands for 'Secure'. It means all communications between your browser and the website are encrypted. HTTPS is often used to protect highly confidential online transactions like online banking and online shopping order forms.
- HTTPS pages typically use one of two secure protocols to encrypt communications - SSL (Secure Sockets Layer) or TLS (Transport Layer Security). Both the TLS and SSL protocols use what is known as an 'asymmetric' Public Key Infrastructure (PKI) system.

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

### How does the server handle dynamic content

- First, the client sends http request to the server. The server handles it and passes it with ```CGI``` or ```FastCGI``` protocols to the gateway. The gateway is the process manager that actually spins up the processes that deal with and interpret the dynamic code "PHP", for example. 
- Some of gateways examples are
  - ```mod_php```: Module can be enabled within Apache and it's a php interpreter integrated within web server so the server doesn't need to make external calls.
  - ```php_fpm```: "PHP FastCGI Process Manager" It's a php interpreter that accepts the FastCGI request from the server, setting-up the environment and process the required files based on the request.

### Apache VS. NGINX

#### Handling the connections and traffic
- **Apache**: has many multi-processing modules "_MPMs_" that dictate how client requests are handled.
  - ```mpm_prefork```: This processing module spawns processes with a single thread each to handle request. Each child can handle a single connection at a time. Fast until the requests exceeds the number of proceses. The only way to make safe multi-threaded php apps "as some php functions are not safe for threading".
  - ```mpm_worker```: This module spawns processes that can each manage multiple threads. Each of these threads can handle a single connection. Threads are much more efficient than processes, which means that this MPM scales better than the prefork MPM.
  - ```mpm_event```: The event MPM handles keep alive connections by setting aside dedicated threads for handling keep alive connections and passing active requests off to other threads. This keeps the module from getting bogged down by keep-alive requests, allowing for faster execution. It's like the ```mpm_worker``` in most cases.
- ***NGINX***: Nginx was designed to use an asynchronous, non-blocking, event-driven connection handling algorithm. It spawns worker processes, each of which can handle thousands of connections. The server is single-threaded and processes are not spawned to handle each new connection, the memory and CPU usage tends to stay relatively consistent, even at times of heavy load.

#### Handling dynamic content
- **Apache**: Apache handles dynamic content by embedding a processor "as loadable module" of the language in question into each of its worker instances. This allows it to execute dynamic content within the web server itself without having to rely on external components. So the configuration of dynamic processing tends to be simpler. Communication does not need to be coordinated with an additional piece of software and modules.
- **NGINX**: Nginx does not have any ability to process dynamic content natively. To handle PHP and other requests for dynamic content, Nginx must pass to an external processor for execution and wait for the rendered content to be sent back. this means that communication must be configured between Nginx and the processor over one of the protocols Nginx knows how to speak (http, FastCGI, SCGI, uWSGI, memcache). However, this method has some advantages as well. Since the dynamic interpreter is not embedded in the worker process, its overhead will only be present for dynamic content. Static content can be served in a straight-forward manner and the interpreter will only be contacted when needed.

#### Specific directory configuration
- **Apache**: Apache includes an option to allow additional configuration on a per-directory basis using ```.htaccess``` files which is often used for implementing URL rewrites, access restrictions, authorization and authentication, even caching policies. It makes it flexible but slower.
- **NGINX**: Nginx does not interpret ```.htaccess``` files.  By not allowing directory overrides, Nginx can serve requests faster by doing a single directory lookup and file read for each request

## Terminal vs Console vs Shell

### Terminal

- Mainframes had terminal stations equipped with a display and keyboard scattered around the premise. They were endpoints where users could access the mainframe.
- Any external part that can interact with the system.
- text input/output environment.

### Console

- physical implementation of a terminal.
- The black screen that you interact with to make input/output commands.

### Shell

- A shell is a user interface for access to an operating system's services.
- It is a command language interpreter that executes commands read from the standard input device such as keyboard or from a file.
- The shell gets started when you log in or open a terminal.
- It is named a shell because it is the outermost layer around the operating system kernel.
- Examples of shells are BASH, CSH, and ZSH.
