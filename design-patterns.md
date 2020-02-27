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
- So instead of making the module completely responsible for logging data to multiple endpoints, we can transfer the responsibility straight to the external environment.
- One Example for this principle is using observers. there’s a highly-decoupled subject "Observable" focused on doing just a few narrow tasks while one or more external observers are responsible for implementing the logic required for handling the events triggered by the subject. How to handle the events, and even processing new ones, is entirely a responsibility of the observers rather than the subject.
- For more info, check this [link](http://bit.ly/IOC-SP).

## SOLID Principles

## Structural Design Patterns

### Dependency Injection

- "Dependency injection is a software design pattern that allows the removal of hard-coded dependencies and makes it possible to change them, whether at run-time or compile-time". Simply, Dependency Injection is providing a component with its dependencies either through constructor injection, method calls or the setting of properties. It is that simple.
- In other words, we are giving the a class its dependency rather than creating it itself.
- For more info, check this [link](bit.ly/di-dpp).

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