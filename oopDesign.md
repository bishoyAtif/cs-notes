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