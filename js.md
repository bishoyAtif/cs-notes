## General
- JS is weakly "loosly" typed variables. Variables change their type by using it in another context.

## Variables and Types

- ```null``` is treated as ```0``` when using it with arithmatic operators.
- ```undefined``` is the value for variables that are declared without assigning a value to it. It will became ```NaN``` special value when using it with arithmatic operators.
- Every value is evaluated to true except the falsy values.
- Falsy values are ```0```, ```-0```, ```NaN```, ```null```, ```undefined```, ```false```.
- Strings are immutable. You can't change individual chars within it. You can't use ```str[0] = 'a';``` but the whole variable can be overwritten.
- ```str.length``` will return the length of the string.

  ### Values Casting 'Coercion'

  ```javascript
    Number('5'); // 5
    String(5); // '5'
  ```

## Variables

- String variables can be interpolated using ``` ` This variable has value ${variableName}` ```.

### Declaring variables

- ```new``` operator is used to create new objects. There are default classes in js like ```Object()```, ```Array()```, ```Function()```, ```Date()```, ```RegExp()```, ```Error()```. Note that ```Number()```, ```String()``` and ```Boolean()``` are used for values coercion and don't use ```new``` keyword.
  ```javascript
    var date = Date('March 6, 2019');
    date.toUTCString();
  ```
### Colsure

- Closure is a function that remembers the variables outside of it even if you pass the function elsewhere.

## Arrays

- use ```var arr = ['Element1', 'Element2'];``` to declare an array.
- Arrays are just objects with a special functions and attributes binded to them.
- Array have order while objects don't.
  ```javascript
    var x = [];
    x[0] = "test value";
    x['key'] = "value";
    x.length // 1
    x[5] = "another value";
    x.length // 6
  ```
- ```array.length``` It's calculated by getting the latest numeric index and add one to it - as it's zero indexed -.
- ```array.push(newElement)``` Adds an element to the array.
- array.sort();
- array.reverse();
- You can loop through an array using ```.forEach(callback)``` on an array.
  ```javascript
    arr.forEach(function(number) {
      console.log(number);
    });
  ```

### Array Destructuring

- Array destructuring is used to multi assign values from array to some variables.
  ```javascript
    var [firstVariable, secondVariable] = [1, 2];
    firstProperty; // 1
    secondProperty; // 2
  ```
- It can be used for swapping variables without using temporary variable. For example,
  ```javascript
    var a = 1, b = 2;
    [a, b] = [b, a];
    a; // 2
    b; // 1
  ```
- When destructuring arrays, the left side will be mapped to the right side variables.
  ```javascript
    var [a, , b] = [1, 2, [3, 4]];
    a; // 1
    b; // [3, 4]
  ```
## Loops

### For Loop

- Using to repeat a block of code for a specific number of times or traversing a datastructure with a numeric index.
  ```javascript
    for (let i = 0; i < arr.length; i++) {
      console.log(arr[i]);
    }
  ```

### For .. in

- Used to traverse an iterable datastructure like an object or an array.
  ```javascript
    for (let i in obj) {
        console.log(obj[i]);
    }
  ```

# DOM
- You can access title "for example" by using document.title
- document.getElementById('id'); //Getting the html element by its id.
- You can access the text between element tags using Element.InnerHTML
- getElementsByClass('class_name') //Getting all elements that have the class name.
- getElementsByTagName('tag_name')
- document.links //Getting all the links in the DOM.
- You can access element attributes as you access js objects by using "element.attribute"
- history //A global array have the history of your browsing in the current tab but you can't read or write from it.
- history.length //Gets the history length.
- history.go(-1) //Returns back to the previous page.
- Element.addEventListener("Event", function_to_be_excecuted)
- 'this' keyword references the element that the event happened to it.
- You can add a class to the class list by using element.classList.add("class_name")
- You can remove a class from the class list by using element.classList.remove("class_name")


- You can declare object by using
  var object = {
    name: 'bisho',
    age: 19,
  }

- You must parse the response get using JOSN.parse(request.responseText);

--------------------------------------General

//null VS undefined
- undefined is a variable declared but not have a value.
- null is explicit removal of the variable value.
- Example: When you check for the variable in your program you will check if the program flow has put the value null to the variable you want, not if the variable has a value or not.
