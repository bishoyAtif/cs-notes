## General

- Local Host 127.0.0.1 >> "There is no place like 127.0.0.1"
- for pure PHP files, Omit the closing tag of php script ```?>```.
- String Concatanation $s .= 'Bisho';  ==>  $s = $s . 'Bisho'; 
- Getting variable type
  - gettype() >> to get only the type of a variable.
  - var_dump() >> to get the type and the contents of a variable in details
- Resource datatype >> A variable that calls an external file or database out of the PHP code. It becomes a 
  resource variable when the connection succeeds but it becomes a False-Boolean variable when the connection fails.
  Example : $conn = mysqli('localhost', 'root', 'password', 'Mydb');
            $fp   = fopen('bisho.txt', 'r');
- Defining a constant >> define("CONSTANT NAME" , constant value or variable);
  Constants are global and used in website config.
- __FILE__ >> constant contains current file name
  __DIR__ >>  constant contains the current directory name
  __METHOD__, __FUCTION__,__NAMESPACE__.
- $a ==  $b is the equal operator. It returns true if only the two values are equal
  $a === $b is the identity operator. It returns true if the two values and data types are equal
  Example : $a = 5; $b = '5'; 
            $a == $b >> true .... but $a === $b >> false
- die(string status) === exit(). It stops the excution of the current script, excutes the destructors and   
  shutdown functions and if there is a status between parentheses It will be displayed. 
- Error control operator '@'. It turns off the errors in php statement.
  $fp = @fopen('Bisho.txt', 'r') or die('There is no file')
  note : '=' is higher precedence than 'or' so the interpreter tries to evaluate fopen() first. If it returned true it will leave the statement otherwise it will turn off the error and excute the after-or statement.
  It may be used with include(), fopen() and database connection
- header('REFRESH:;URL=bisho.php'); >> redirects to bisho.php after seconds. 
- header('Location: bisho.php'); >> redirects to a new location
- Using _END : _END; must be on a new line with no indentation and without spaces after it.
  echo <<<_END Some text .....
    Another text
_END;
  Advantges of using it :
    - Makes it very clear when debugging your program
    - When you wish to insert a variable within HTML you type it directly without need to reopn php tags.
- empty($variable) >> returns true if variable doesn't have any value.
- ini_set('Property', 1); >> sets a value to ini file 'PHP Configuration'
- Adv. of Functions :
    - Less typing.
    - Less excution time.
    - reduce syntax and programming errors.
- function_exists('Function_name') >> Used to know if the fucntion exists in this version of PHP.
- Anonymous functions >> The functions which aren't assigned to a specific name but just added to a variable or inserted in another function 
  Example : $func = function(){// Function body}
- The call back is a property that used with anonymous functions 
  Example:  function split_str($string, $callback){
              $results = explode(' ', $string);
              if(is_callable($callback))
              {
                call_user_func($callback, $results);
              }
            }
            split_str('Bisho Atif Samy', function($results){
              echo $results[2]; 
            });
- uniqid([ $prefix = '', $more_entropy = FALSE ]) >> returns a random id with prefix.
  with 23 chars if $more_entropy = true of 13 if false.
- hmtlspecialchars($text) >> used when adding text to your html
- urlencode($text) >> used when adding text to your URL
- sleep($sec) >> stops the execution of the script for $sev seconds.
- usleep($sec) >> the same as sleep but in micro seconds.
- ceil($number) >> rounding the number up.
- floor($number) >> rounding the number down.
- func_get_args() >> used within a function to return the function arguments as an array.
- RegEx: The pattern in PHP is included within foroward slaches '/Pattern/' 

## Variables & Operators

- We can use variable functions. 
  Example : $x = 'hello'; $x(); >> This will trigger the function hello. It's like using hello();

- Super global variables     
    $GLOBALS >> An assocaiative array that has all variable names in the global scope of the scope as its keys and global values as its values
    $_SERVER >> An assocaiative array that has all server information needed
    $_GET, $_POST, $_FILES >> has all variable sent to script from these http headers
    More like $_ENV, $_SESSION, $_COOKIE and $_REQUEST

- Global variables can't be accessed directly in function scope. It can be only accessed with 
  $GLOBALS['variable_name'].

- $_SERVER['REQUEST_METHOD'] >> GET, POST, PUT and so on.
  $_SERVER['SERVER_ADDR']    >> server ip. like 127.0.0.1.
  $_SERVER['SERVER_NAME']    >> server name. like localhost.
  $_SERVER['PHP_SELF']       >> returns the path to the php script.
  $_SERVER['QUERY_STRING']   >> returns the query string attached to the link requested .. ?name=bisho&...

- $_GET >> Array contains all parameters sent from the form to the current php script. It is shown in the link.

- $_POST >> Array contains all parameters sent from the form to the current php script. It is not shown in the 
            link parameters and is encrypted.

- $_REQUEST >> Can act like $_GET or $_POST.

## Arrays

- You can define array as ```['element1', 'element2', ...]```
- We can add an element to the end of an indexed array using ```$array[] = value``` and to the end of associative array using ```$array[key] = value;```.
- We can overwrite a value of the array using ```$array[index] = newValue;```.
- floating point can't be assigned as keys in associative array. The array ignores the floating point part and deals with it as int.
- ```foreach($arrayName as $value){}``` loops through the values of the array and ```foreach($arrayName as $key => $value){}``` loops through the keys and values of the associative array.
- To loop through rows of a database, We can use a nested foreach loop
```php
  foreach($results as $key => $row) {
    echo $key . '<br>';
    foreach($row as $field => $value) {
      echo $field . '---->' . $value . '<br>';
    }
    echo '----------------------------------------<br>';
  }
```

### Common array related functions

- extract($array, $mode, $prefix) turns the key value pairs in the associative array to a variables and 
  values in the current script.
    * EXTR_OVERWRITE   >> If there is a collision, overwrite the existing variable. 
    * EXTR_SKIP        >> If there is a collision, don't overwrite the existing variable.
    * EXTR_PREFIX_ALL  >> Prefix all variable names with prefix.
    * EXTR_PREFIX_SAME >> If there is a collision, prefix the variable name with prefix.
- compact($array_of_strings = 'str1','str2'....); returns an associative array with pairs of keys from the 
  variable name from the string inputted and a value from the corresponding variable value.
  It is usually used for debugging a script
  Example : $arr = compact(explode(' ', 'var1 var2 var3'));
- count($array, $mode = 0) >> counts the elements of an array 
    * $mode = 0 or COUNT_NORMAL >> counts only the first  level of the array.
    * $mode = 1 or COUNT_RECURSIVE >> counts recursively all the elements of the arrays in the indexes of the main array
- array_reverse($array); >> returns a reversed array.
- Adding elements to the array 
    - array_push($array, $item1, ...) >> adding item to the end of the array.
    - array_unshift($array, $item1, ...); >> adding item to the top of the array.
- Removing elements from the array 
    - array_pop($array, $item1, ...) >> removing item from the end of the array.
    - array_shift($array, $item1, ...); >> removing item from the top of the array.
- sort($array, $sort_type) , rsort($array, $sort_type) "Reversed Sort" >> 
    * SORT_REGULAR - compare items normally >> doesn't change types of data (orders string fistly then int).
    * SORT_STRING - compare items as strings >> changes the whole array to strings then orders it.
- asort($array, $sort_type),rasort($array, $sort_type) >> sorts associative array values normally and reversed 
  ksort($array, $sort_type),rksort($array, $sort_type) >> sorts associative array keys normally and reversed
- Array searching methods: 
    - in_array($item, $array) >> returns true if the item is in the array, false if not.
    - array_search($item, $array) >> returns the index of the item in the array if exists, else returns false.
    - array_key_exists($key, $array) >> returns true if the key exists in the array, false if not.
- shuffle($array); >> shuffles the array inputted.
- array_fill($start, $number, $value); >> returns an array filled with the value repeated from the start 
  position and repeated $number times.
- array_sum($array); >> returns the sum of the values in the array "ignores strings".
- array_rand($array, $num = 1) >> returns an array of $number random keys from the main array. If $num = 1 it  
  will return only int not an array.
- array_unique($array); >> returns the main array without repeated elements.
- reset($array) >> returns the first element of that array.
  end($array)   >> returns the last element of that array.
============================================================================================================

                                    -----------------------------
                                    <<<<<<<    Strings    >>>>>>>
                                    -----------------------------

- explode($delimite, $array, [$limit]) >> it splits the string about the delimiter and returned it to an array
  * if limit > 0, it will split the string to maximum indecies of that limit.
  * if limit < 0, it will split the string ignoring the limit number inputted from the end of the array

- join() = implode($delimiter, $array) >> the opposite of explode .. It returns a string from concatanating 
  all the elements in the array seperated by the delimiter inputted.

- str_split($str, $length = 1); >> splits the string to chunks of length chars and put them in an array.

- chunk_split($str, $length, $delimiter = '\n'); >> returns the string with the $delimiter between every   
  $length characters of it.

- str_replace($replaced_string_array, $replace_with, $str, $count); works on strings and the values of an array
    - If $replaced was array and $replace_with was a string it will search for all the strings in the array 
      and replace it with the string.
    - If $replaced was array and $replace_with was an array it will replace each value of the first array with 
      the corresponding value in the second array "If the second array was smaller than the first, the values 
      that have no corresponding replaces will be replaced with empty strings" 
  Example : changing the '\n' to '<br>' in html forms to be viewd in the page as a new line.
            $str = str_replace('/n', '<br>', $str);

- str_repeat($str, $num) >> returns a string with value $str repeated $num times.
- str_shuffle($str) >> returns the string $str shuffled
- strlen($str) >> returns the string length
- strtolower(), strtoupper() >> returns the string in lower case or upper case
- ucfirst() >> upper case first, lcfirst() >> lower case first
- ucwords() >> returns the string with all its words upper case.
- addslashes($str) >> escape all quotes and slashes from the string.
- stripslashes($str); >> remove all slashes before charachters escaped in the string.
- strip_tags($str, $allowed_tags :: "<br><a><b> and so on");  >> remove all html and xml tags from the string.
- trim($str, $charlist = '\n\t \0'), ltrim(), rtrim() >> it returns the string with its beginning and end stripped with $charlist
  example : $str = trim($str, 'BASHIK') >> it will search in the two endings with this chars and remove them one by one.

- parse_str($str,[$array]); >> parses the link and returns all key value pairs in it as a variable or in an 
  array if inputted.
  Example : parse_str("name=Bisho&age=19&gender=male", $array) >> makes $array associative array that have 
  key : name with value Bisho .. ,etc

- nl2br($str, [XHTML = true]); >> returns a string with all new lines converted to breaks.

- str_word_count($str, [ $mode = 0, $charlist = '' ]) >> split the string to words
  - Mode:
    - mode = 0 >> returns only the numbers of the words in the string
    - mode = 1 >> returns the words of the string as a numeric array
    - mode = 2 >> returns the words of the string as an associative array with keys 'the position of each word'
  - Charlist: A string have all special characters that can be counted as words.

- strcmp($str1, $str2) 
  - returns 0  >> the two strings are the same.
  - returns +n >> the first string is more than the second string with n chars
  - returns -n >> the first string is less than the second string with n chars

- strncmp($str1, $str2, $length)
  - The same as strcmp() but is works with the first $length chars of each of the words.

- strrev($str) >> returns the string reversed.

============================================================================================================

                              --------------------------------------------
                              <<<<<<<    What 's the difference    >>>>>>>
                              --------------------------------------------

- Difference between echo and print   
    - They are both php constructs and doesn't need parentheses
    - print can have many arguments not like echo.
    - print have a return value so it's little slower than echo
    - echo can't used in more complex expressions like $b ? print 'TRUE' : print 'FALSE'

- Difference between require and include:
    - including file with require stops the whole script if the file doesn't exist, require_once includes the 
      file just once.
    - including file with include doesn't stop the script if the file doesn't exist and just shows a warning 
      that the file doesn't exist, include_once includes the file just once.

- Difference between single and double quoted strings 
    - Single quotes >> The interpreter doesn't try to evaluate the variables in it like 
      'Hi His is $Dollar' >>> Hi His is $Dollar
    - Double quotes >> The interpreter tries to evaluate the variables in it like 
      'Hi His is $Dollar' >>> No variable called $Dollar (Assuming that no variable $Dollar declared)

- Difference between 'and' and && 
    - and >> has lower precedence than equal operator '='
      example : $a = true and false >> ($a = true) and false .... so $a equals true and that is wrong.
    - &&  >> best practice to use it because it has higher precedence than equal operator. It doesn's cause 
      any problem with using assignment and logical operators.

- Difference between == (equality) and === (identity)
    - 'Bisho' == 'Bisho' >> true
    - 'Bisho' === 'Bisho' >> true
    - '2' (string) ==  2 (int) >> true
    - '2' (string) === 2 (int) >> false

============================================================================================================

- htmlentities() function that escapes all html dangerous characters that passed to it.

- Ternary operator ? is used like if statement with vaiable assignment
  Example : $x = $x > $new ? $x : $new; >> This checks for the condition ($x > $new) and assign variable $x based on this condition.

- rand(from, to) >> getting random value from the range inputted.

- phpversion() >> shows the php version of your current server.

- phpinfo() >> shows info about your server, php version, server configs and more. It 's usually disabled in 
  the production stage.      

- list() is used to assign a list of variables in one operation and it only works on numerical arrays.
  Example : list($drink, $color, $power) = ['coffe', 'brown', 'powerful'];
            echo "$drink is $color and $power makes it special.\n"; >> coffee is brown and caffeine makes it 
            special

============================================================================================================

                                      -------------------------------
                                      <<<<<<<    Debugging    >>>>>>>
                                      -------------------------------

- var_dump(A no-value-returning-function) >> NULL

- We musn't include any file twice or more, It will cause an error because we will declare the variables and 
  the functions in the main script more than one time. 

- Don't nest multi line comments

- print_r() >> prints any type of arrays in a human readable format. It is usually used within <pre></pre> to 
  be printed in the write way in html. 

=============================================================================================================

                                  ----------------------------------------
                                  <<<<<<<    Working with files    >>>>>>>
                                  ----------------------------------------

- $handle = fopen('file_name', 'mode'); >> opens this file in the mode required
  - mode :
    - 'r' Open for reading only; place the file pointer at the beginning of the file.
    
    - 'r+'  Open for reading and writing; place the file pointer at the beginning of the file.
    
    - 'w' Open for writing only; place the file pointer at the beginning of the file and truncate the file to zero 
      length. If the file does not exist, attempt to create it.
    
    - 'w+'  Open for reading and writing; place the file pointer at the beginning of the file and truncate the file to 
      zero length. If the file does not exist, attempt to create it.
    
    - 'a' Open for writing only; place the file pointer at the end of the file. If the file does not exist, attempt to 
      create it. In this mode, fseek() has no effect, writes are always appended.
    
    - 'a+'  Open for reading and writing; place the file pointer at the end of the file. If the file does not exist, 
      attempt to create it. In this mode, fseek() only affects the reading position, writes are always appended.
    
    - 'x' Create and open for writing only; place the file pointer at the beginning of the file. If the file already 
      exists, the fopen() call will fail by returning FALSE and generating an error of level E_WARNING. If the file 
      does not exist, attempt to create it.
    
    - 'x+'  Create and open for reading and writing; otherwise it has the same behavior as 'x'.

- Opening a file using FTP
  $handle = fopen('ftp://user:password@bisho.info/path_to_file', 'mode');

- $content = fread($handle, $length) 
  Example: $content = fread($handle, filesize($file_name));

- fwrite($handle, $string, [$length]) >> writes a string to a file 

- fseek($handle, $offset, $whence) >> moves the pointer to a specific position different from the default position.
  - whence:
    - SEEK_SET - Set position equal to offset bytes.
    - SEEK_CUR - Set position to current location plus offset.
    - SEEK_END - Set position to end-of-file plus offset.

- __DIR__ 's value is the current directory of the current script.
- __FILE__ 's value is the full file name of the current script.
- file_exists($file) >> reutrns true if the file exists, false if not.
- is_writable($file) >> reutrns true if the file is writable, false if not.
- filesize('bisho.txt') >> returns the file size of the inputted file
- mkdir($dir) >> making a directory named $dir.
- rmdir($dir) >> removing dir named $dir.
- is_dir($dir) >> returns true if the dir exists, false if not.
- dirname($path) >> returns the path of the directory your file are in. 
  Example : dirname(__FILE__) == __DIR__
            dirname(/opt/lampp/htdocs/first_task) == '/opt/lampp/htdocs'

- basename($path, $suffix) >> takes the path of the whole file and returns the file name only .. if extention 
  of the file was inputted it will remove the extention from the returned name.
  Example : basename(/opt/lampp/htdocs/first_task) == 'first_task'

- chmod($file, $permissions) >> modified the permisstions of the file as you changes it with linux command 
  line. 

- file_put_contents($file_path, $data, $mode) >> puts the $data in the file. If not existes it will be created.
  Mode :
    - FILE_APPEND >> don't remove the previous file contents.
    - LOCK_EX >> to prevent anyone else writing to the file at the same time.

- file_get_content($path/to/file, $include_path, context, offset, length) >> returns the contents of the file 
  as a string and can return a specific length from a specific offset.

- copy($original_file, $target_file);
- rename($original_file, $target_file); >> can be treated as move.
- pathinfo($path); >> returns an array contains dirname, basename, extentsion, filename.
- unlink($file_name); >> removes the file.
- rmdir($directory); >> removes the directory .. must be empty.
- scandir($path) >> returns the files and the folders in this path in an array.


=============================================================================================================
                                      -----------------------------
                                      <<<<<<<    Filters    >>>>>>>
                                      -----------------------------

- filter_list() >> returns an array have all filters possible in php.

- filter_var($input, Flags, Options); >> returns a sanitized string
    - Flags can be used to validate or sanitize inputs.
    - Options are passed as an array.

- filter_var($email, FILTER_VALIDATE_EMAIL) >> returns the email if the email is valid or false if not.

=============================================================================================================

                                      ----------------------------
                                      <<<<<<<    MySQLi    >>>>>>>
                                      ----------------------------

- $conn = new mysqli($hn, $un, $ps, $db);
  if($conn->connect_error) die($conn->connect_error);  >> Connecting to the DB.

- $results = $conn->query(); >> returns a result object based on this query.

- $results_array = $results->fetch_all(MODE); >> returns the results as an array
    - Mode can be MYSQLI_ASSOC >> returns associative array.
    - Mode can be MYSQLI_NUM >> reyurns numeric array.

- $conn->insert_id >> if you want to know the id of the row you have just inserted.
  ==> I think it differs from one php version to another ... maybe $result->insert_id

- $results->close(), $conn->close() >> closes the conn and the results object.

## Security

- register_globals >> functionality in PHP that takes the variables in $_POST and $_GET and put them directly 
                      in PHP variables ... Must be disables because any one can but GET attribute in the link 
                      to override your script variables if not initialized " website.com/?override=value "
- Using Placeholders >> The Most safe way
  - $statement = $conn->prepare("INSERT INTO books VALUES(?,?,?,?,?)");
    $statement->bind_param('isisi', $isbn, $name, $year, $author, $category) ;
    /// i --> integer, s --> string, d --> double, b --> blob :: This is added in the first parameter of bind
    $isdb = 123; $name = 'bisho' .......;
    $statement->excute(); // Finished Excuting statement.
- Protecting from XSS 'Cross Site Scripting' >> must be used when making user add things to your HTML code.
  - htmlentities($string);
  - strip_slashes($string);
  - strip_tags($string);
- SQL Injection >> hacker inputs some text in the form to complete a query in your database connection to 
                   access a forbidden data in your site.
                   >> name= admin , password = 'or 1=1 or ' .. makes an always true condition in password field
                   >> name= admin' -  ... comments the rest of the database query
- Protecting from SQL Injection : 
    - $conn->real_escape_string($string);
    - Use the protection of XSS also

## Exceptions

### ```try .. catch``` statement

- Exceptions in PHP are used to mark that there is an error then handle it later and give the feedback to the user.
- try .. catch statement is used to catch any exception that arises within try statement. If no try .. catch statement found and an exception occured, PHP fallbacks to the global exception handler to handle it.
  ```php
    try {
        // Run your code here
    }
    catch (Exception $e) {
        // Code to handle the exception
    }
    finally {
        // Optional code that always runs
    }
  ```
- You should ensure that you actually do something about the exception when catching it. In most cases, Just silenting the exception can cause bugs which are hard to diagnose.

### Exception Class

- It has a constructor that receives the message and the status for the error happened.
- It has some methods like
  - ```getMessage()```. Gets the Exception message.
  - ```getPrevious()```. Returns previous Exception.
  - ```getCode()```. Gets the Exception code.
- You can simply ```throw``` an ```Exception``` using ```throw new Exception('Message', exceptionCode)```. Standard ```Exception``` Class implements ```throwable``` interface so that it can be thrown.

### SubClassing Exception

- You can simply extends ```Exception``` and handle those special exception separately.
  ```php
    class AuthException extends Exception
    {
        // Other special functions related to the authentication process.
    }

    try {
        throw new AuthException();
    } catch (AuthException $e) {
        // Code to handle the special exception.
    } catch (Exception $e) {
        // Code to handle the general exception.
    }
  ```

## PDO

- PDO is not a specific database extention but it is database access layer that can access many of database 
  engines like mysql, sqlite, postgres.
- To know the database engines in your system use the static function PDO::getAvailableDrivers();
- To create a new PDO connection object with a specific db :
  $handler = new PDO('mysql:host=ip_address;dbname=database_name', 'user_name', 'Password');
- We can use try and catch exceptions using PDOException class
  ```php
    try
    {
      //Connect to the DB
    }
    catch($PDOException $e)
    {
      $e->getMessage(); //This returns the error happened
    }
  ```
- To set attributes to the pdo object >> $handler->setAttribute(PDO_Attribute, PDO_Constant);
- To get the available drivers in the current pdo version .. use $handler->getAvailableDrivers();
- $result = $handle->query('SELECT * FROM table');
  $result->fetch(PDO_BOTH, PDO_NUM, PDO_ASSOC, PDO_OBJ) >> fetches one row of the data with these specific preferences.
- $query = $handle->query($sql);
  $query->setFetchMode(PDO::FETCH_CLASS, 'Class_name');
  while($object_name = $query->fetch())
  {
    //Do something with $object_name;
  }
  class Test
  {
    function __construct ...
  }
- Preparing statements:
  $sql = "SELECT * FROM books where id = ?";
  $stm = $db->prepare($sql);
  $result = $stm->execute(["Value of placeholder #1", "Value of placeholder #2" ..... ]);
- Last Inserted ID:
  $handler->lastInsertId(); >> returns the value of the last insert query id.
- $results->rowCount(); >> returns the number of the rows returned from a query.

## Date & Time

- time() >> returns the current timestamp in unix format.
- data($format[ , $timestamp = time()]) >> formats the timestamp as the inputted format.

## Clean Code Tips

- Return expected objects last.
- At If statements, Check the negative values that can break your work flow first So you don't need to nest if 
  statements.                            

## Cookies & Sessions

- HTTP is a stateless protocol. There is no association between any two HTTP requests. Because the protocol does not provide any method that the client can use to identify itself, the server cannot distinguish between clients.
- Cookies are an extension of the HTTP protocol. More precisely, they consist of two HTTP headers: the Set-Cookie response header that adds a cookie key-value pair to the browser and the Cookie request header that sends the cookie values in the browser to the server.
- It is a small piece of data "4KB" stored in the browser for a specific website. Each cookie belongs to a specific domain and it can only be sent or received to its specific domain or the parent domain. A domain can't set or reveive cookies from its sub domains or its sibillings.
- If the cookie has no "expires" parameter, It's called "session cookie" and it expires when you close the browser. The "remember me" feature in the login forms sets the "expires" parameter in the cookies.
- The concept of session management builds upon the ability to maintain state by maintaining data associated with each unique client using cookies.
- You can use the superglobal array ```$_COOKIE``` to view the current cookie stored in the client side.
- You can add a new cookie to the browser using ```setcookie(<key>, <value>, <whenToExpire> "time() + 60 * 60 to denote an hour", <secure> "HTTPS", <httpOnly> "Available for scripts? or not")```
- To delete a cookie use ```setcookie(<key>, null, time() - 60 * 60)```. That will set the expire date of the cookie to a timestamp in the past. So it will be destroyed.
- Session is based on cookies and it saves info about the user and populates it in all of the pages for the same domain in the browser's session. For example, the shopping cart contents should be saved when I navigate the website. By default the session will be destroyed if I close the browser. You can explicitly save the session key to the cookie to resume the session in the next time you open the browser.
- By default the session file is saved in the server  within a storage or a database and the server finds the right session for the right user using ```phpsessid``` key in the ```$_COOKIE``` superglobal array.
- You should call ```session_start()``` to resume or initiate a session when using the sessions within your app.
- When you call ```session_start()```, PHP first determines whether a session identifier ```'phpsessid'``` is included in the current request within the request cookie. If it is, the session data for that particular session is read and provided to you in the ```$_SESSION``` superglobal array.
- The two most common causes of cookie disclosure are browser vulnerabilities and cross-site scripting.

## Composer

- Composer is a dependancy management tool that are used for autoloading also.

### Autoloading

- Required classes should be included before we use them.
- We can simple include all the classes, but with huge libraries we could import too much unused classes. Here comes the autoloading to solve this problem, It imports only the files with classes we gonna use
- In older days, SPL's autoloader was used. This function will trigger this functions and import any class using ```require``` when a class is used.
  ```php
    spl_autoload_register(function($class) {
      require "src/{$class}.php"; // The class name must be identical to the file name.
    });
  ```
- One way to use autoloading by making ```composer.json``` file and add this snippet .. It will load all the classes from the specified directory "Just add ```/vendor/autoload.php``` within your root file" **You have to run ```composer dumpautoload``` every time you add another class to add the new class in the classmap**
  ```json
  {
    "autoload": {
      "classmap": [
        "DirectoryToLoadFrom/"
      ]
    }
  }
  ```
- Another way is to use autoloading is to use ```psr-4``` key. You must have namespaces within your classes files to implement it and every time you add a new file, It gets autoloaded dynamically. An example to this approach is
  ```json
  {
    "autoload": {
      "psr-4": {
        "RootNameSpace\\" : "DirectoryToLoadFrom"
      }
    }
  }
  ```
