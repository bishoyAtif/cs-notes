# OOP Design

## Design Principles

- Separate the code that changes a lot from the not changing one.
- Program to an interface not to an implementation.
- Favor composition over inheritance.

Why Encapsulation ?

1- It protects the information you want to keep out from another classes not from hackers
   It makes constraints on the variables that you don't need to modify it by external classes.
2- It keeps the organization of the classes structure .. It provides brief info about the internal variables of each class "doesn't depend on any class" and the external variables that depends on other classes.

Example : Suppose, you are a developer and your client is a bank that wants you to develop a library that involves classes related to bank accounts.

Now suppose you have a class "Account" that has attributes like account number, account balance etc. Your class can connect to the banks data base to access these details. You compile these classes and create a library. .  Now, if you just make these variables public then any other class (which is not part of your library) but includes your library in their code, is now able to to read it as well as write to it.

For example I develop a website to dispaly bank account by using your library. Now I do not access the bank database directly but I just use your classes to fetch the details. Now, as you made the variables public I got power of replacing the account balance variable although I should not have that permission but developers mistake gave me that permission!

But if you give just read only access to certain fields like account balance then my website can just access bank data through your library with read only permission. So now it can just display the account balance for example but not change it.

So protecting your variables has nothing to do with hackers. It has to do with other classes that use your class.

This is like giving key to your home to neighbours whom you want to access your home, still you want your locker room to be locked and not grant access to it. So think variables as safe box which you want to be private and not with public access.

## General Principles

### IOC "Inversion Of Control"

- ***Hollywood Principle***: Don't call us, we'll call you "Making actions that aren't implemented within the same module by calling the action from another module".
- Inversion of Control is as it says, “inverting the control” of a system by keeping organizational control entirely separate from our objects.
- Traditionally, application components have been designed to operate on and control the execution environment. For instance, a logging module could be implemented to log data to a file, and how and when to log the data would be a entirely under control of the module. But let’s say we need to extend the module’s functionality add logging data to a database, or eventually even via email. Upgrading the module to expose the extra functionality will make it grow in complexity, becoming more bloated as the logic required to attend to these additional duties is packaged behind the same API.
- So instead of making the module completely responsible for logging data to multiple endpoints, we can transfer the responsibility straight to the external environment, for example a whole new module.
- This principle helps to prevent dependency rot. Dependency rot happens when each component depends upon every other component. In other words, dependency rot is when dependency happens in each direction (upward, sideways, downward). The Hollywood Principle allows us to only make dependency in one direction.
- One Example for this principle is using observers. there’s a highly-decoupled subject "Observable" focused on doing just a few narrow tasks while one or more external observers are responsible for implementing the logic required for handling the events triggered by the subject. How to handle the events, and even processing new ones, is entirely a responsibility of the observers rather than the subject.
- For more info, check this [link](http://bit.ly/IOC-SP).

## SOLID Principles

### Single Responsibility

- “A class should have one, and only one, reason to change”.
- The problem: 
  - Maintainability: If you used a component that have many responsibilities. You may need to use one of those components in another place. In this case, you will need to copy it. But If you refactored it in another component and used it directly, you will change it in only one place.
  - Testability: If you need to test a class and you need to mock one of its components. It will be impossible to mock it if it is implemented within the same class.
  - Side Effects: Changing a class with single responsibility has less side effects than changing a class with multiple responsibilities.
  - Readability and Ease to understand: Classes, software components and microservices that have only one responsibility are much easier to explain, understand and implement than the ones that provide a solution for everything.
- The solution: Break any complicated class to classes each of them having one responsibility, Injecting related services together as needed.
- Example: If you have a controller that fetches the data from the tables, manipulates it and render it to a web view. And you need to make an api that outputs json. You will duplicate the whole code for fetching and manipulating the records. But if you have two separate classes one for fetching and manipulating the data and one for outputting it. You will have the manipulation process encapsulated in one place.
- Check this [github link](https://bit.ly/laracasts-srp) and this [article](https://bit.ly/srp-toptal) from toptal for example code.

### Open Closed Principle

- “Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification”.
Problem: Changing code in different places is hard to be maintained and causes a lot of bugs.
Solution: Try hard to separate the code that can be changed under a separate interface. So you just implement your login against the interface and be sure that the implemented classes have the functionality introduced in the interface.
- Check this [github link](https://bit.ly/laracasts-ocp) for example code.

### Liskov Substitution Principle

- “If S is a subtype of T, then objects of type T may be replaced with objets of type S”. Simply, Derived classes must be substitutable for their base classes.
- It extends the Open Closed principle and enables you to replace objects of a parent class with objects of a subclass without breaking the application.
- Problem: When using Open Closed Principle, you will extend the behaviour by substituting classes by new classes instead of changing the old class. So If the new class that inherits from the base class or implements the interface introduced behaves differently "throws an exception that wasn't expected when using the old class", This will cause a problem in one class of the substitutions or at least we will need to handle that exception differently according to the class type.
- Solution:
  - Don’t implement any stricter validation rules on input parameters than implemented by the parent class.
  - No new exeption should be throwed in the extended classes that weren't introduced in the base class.
  - The type of the returned values from the methods should be exactly as the base class's implementations.
- Check this [github link](https://bit.ly/laracasts-lsp) and this [article](https://bit.ly/stackify-lsp) from stackify for example code.

### Interface Segeration

- “Clients should not be forced to depend upon interfaces that they do not use“.
- Problem: When a class implements an interface that have much responsibility, It may not need all the functions contracted with the interface. So you may need to define functions just for the sake of implementing the contract and ```return null``` or so from those functions.
- Solution: Splitting the large interface to smaller interfaces. and use the smaller interfaces within the scope needed.
- Example: If you need to send an email to a user, you may have a function that accepts a User. But that scope it too large as if you needed to use this function to send emails to an email list you will need that to implement all functions of User in the email list. Instead, you should use an interface called ```Emailable``` within the ```sendEmail``` function and make the User implement it. So when you use an email list as a receiver, you need only to implement the functionality that enables the function to send to those emails.
- Check this [github link](https://bit.ly/2TIjgnN) for example code.

### Dependency Inversion

- “High level modules should not depend on low level modules but they both should depend on abstractions“. “Depend on abstractions not on implementations“.
- Dependency Injection is not equal to Dependency Inversion. But it is a method to adhere to the Dependency Inversion Principle.
- Problem: High coupling between components. Highly coupled components are difficult to be changed.
- Solution: Instead of using the implementation of the class "low level class" directly within another class "high level class" and calls methods from the class directly, You should code to an interface that are already implemented by another class and call the methods agreed on in the interface. This approach enables you to decouple the low level code from the high level one. In other words, you can change the underlying implementation of the low level class without changing the interface used, and that will have no effect on the high level code.
- Check this [github link](https://larcasts-dip) and this [article](https://bit.ly/stackify-lsp) from stackify for example code.

### More Resources

- This [article](https://bit.ly/jokiruiz-solid) has a brief introduction to SOLID Principles with example for each of them.
- This [series](https://bit.ly/tutsplus-solid) is a great explanation for SOLID Principles either.
- This [article](https://bit.ly/dzone-solid-grasp) is also great. It talks about SOLID, GRASP and many different oop desing principles.

## Structural Design Patterns

### Dependency Injection

- Dependency injection is a software design pattern that allows the removal of hard-coded dependencies and makes it possible to change them, whether at run-time or compile-time. Simply, Dependency Injection is providing a component with its dependencies either through constructor injection, method calls or the setting of properties. It is that simple.
- In other words, we are giving the a class its dependency rather than creating it itself.
- We can use the database object in the user class constructor to add the create user function using the query function in the database class.
- For more info, check this [link](bit.ly/di-dpp).

### Service Locator

Many developers out there don’t see the difference between the dependency injection and the service locator design patterns. Yes, both of them are trying to solve the same problem — increase decoupling. We all know what benefits this give us when it comes to scaling, testing or simply reading the code.
However, how do I know when to use dependency injection and when to use service locator? I would say we should use both of them when appropriate.
If I was asked to choose a single verb that best describes the dependency injection pattern I would choose “to give”. If you think about it, that’s exactly what we achieve with dependency injection after all. We simply give objects to an object.
$window = new Window();
$door = new Door();
$house = new House($window, $door);
In this case, we give the window object and the door object to the house object.
On the other hand, if I was asked to describe the service locator pattern with a single verb I would say “to take”. Just think about it. That’s what we do when we use a service locator. We take objects from an object.
$house = $serviceLocator->get(House::class); 
As you can see, we take the house object from the service locator.
In many cases, the dependency injection and the service locator work as a single unit. We might not see it when the things are injected automagically but behind the scene the implementations of dependency injection rely on service locators in order to retrieve actual dependencies.
This is how it might look like somewhere in the code:
foreach ($dependencies as $dependency) {
    $instances[] = $this->container->get($dependency);
}
return $this->resolve($class, $instances);
A service locator is pretty easy to implement. All you need is to have ability to get a requested instance by name or id and ability to check whether the requested instance actually exists. Worth to note that a service locator is often called a container. Both things are the same. Both of them are meant to provide instances or services however you prefer to call them. Of course, there’s a difference between a service and an instance when speaking about terms and purposes, but from the technical point of view they are all instances of certain classes.
Here’s a primitive version of a service locator (aka container):
class ServiceLocator {

    private $services = [];

    public function get(string $id) : ?object {
        return $this->services[$id] ?? null;
    }


    public function has(string $id) : bool {
        return isset($this->services[$id]);
    }

    public function register(string $id, object $service) : void {
        $this->services[$id] = $service;
    }
}
$serviceLocator = new ServiceLocator();
$serviceLocator->register('house', new House());
// somewhere else

if ($serviceLocator->has('house')){
    $house = $serviceLocator->get('house');
}
Additionally, I have provided the way to register services.
The implementations of dependency injection usually inject dependencies into objects automatically. All you need is to provide a bit of configuration and that’s all. That’s pretty convenient in many cases, but there are cases when you have to use service locator to avoid the deadlock. This could happen when two instances are depended on each other via constructor. Here’s an example:
class A {
    
    public function __construct(B $b)
    {
        //
    }
}

class B {
    public function __construct(A $a)
    {
        //
    }
}
$a = new A(...); // We need B!
$b = new B(...); // We need A!
As you can see, we cannot resolve any of the services because they are depended on each other. We cannot resolve the service A because it requires the service B, and we cannot resolve the service B because it requires the service A. To solve this, we need to retrieve one of the services in lazy-loading way. Meaning that, we should take one of the services from the service locator at the point when the service is actually needed and not in the constructor.
All in all
Hope this article cleared some things up for you and you enjoyed reading it. If not, then you must be already smartest programer out there ;-)

## Database Design Patterns

### Active Records

- Active Records maps an object to a database table row. <img src="https://www.infinitypp.com/wp-content/uploads/2011/03/active-record.jpg" alt="Active Records" width="40%" align="right" style="margin: 15px">
- The interface of an object conforming to this pattern would include functions such as Insert, Update, and Delete, plus properties that correspond more or less directly to the columns in the underlying database table.
- This pattern is commonly used by object persistence tools and in object-relational mapping (ORM).
  ```php
    $user = new User;  
    $user->username = ‘philipbrown’;  
    $user->save();  
  ```
- Advantages:
  - Esay to get up and running with small or medium size projects.
- DisAdvantages:
  - Less SQL means queries may be more numerous and less performant. Bottlenecks might occur when the users of the system grows as it can't use pure SQL.
  - Your domain is not your database. You think about the app in terms of entities so it isolates the develoeper from the database.

### Data Mappers

- The data mapper is meant to be a layer between the actual business domain of your application and the database that persists its data. It completely separates your domain from the persistence layer. <img src="https://www.infinitypp.com/wp-content/uploads/2011/03/datamapper.png" alt="Active Records" width="40%" align="right" style="margin: 15px">
```php
  $user = new User;  
  $user->username = ‘philipbrown’;  
  EntityManager::persist($user);    // EntityManager can be an injected service that is responsible for the persistance.
```
- Advantages:
  - Greater flexibility between domain and database.
  - Data Mappers "Doctrine2, for example" can be much more performant.
- DisAdvantages:
  - It's not too easy like active records "where you design your database along with your Models". It requires you to configure the mapper layer independently.
- For more info, check this [link](https://culttt.com/2014/07/07/doctrine-2-different-eloquent/)