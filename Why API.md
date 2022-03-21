---
title: Why API ?
created: '2020-07-25T21:55:59.514Z'
modified: '2020-07-25T22:02:58.614Z'
---

Why API ?

- Application Programming Interface : An interface for a specific application to get information that another application want in a standard format "JSON for example".

- It's just a servant between two applications .. It gets the requset from one of them in a specific format and go to the another app and serve it then returns with the response to the second app in a specific format.

Example :
Without API:
An app finds the current weather in London by opening http://www.weather.com/ and reading the webpage like a human does, interpreting the content.

With API:
An app finds the current weather in London by sending a message to the weather.com API (in a structured format like JSON). The weather.com API then replies with a structured response.


## Why encoded slashes are disabled by default in most web servers?
- For security reasons. This is mostly to avoid issues you'd normally get with non-encoded content. This behavior is often associated with Remote Code Execution, Local File Access and Directory Traversal.<br>
- An example to this will be ```include 'languages/'.$_GET['lang'];```. A hacker may pass ```../``` to move around.

## OAuth 2

### Delegated Authorization

- OAuth is basically used for delegated authorization.
- For example, If you need to access your drive files from a third party application.
  - You can add google credentials to the third party and it will login for you and get your data. This is extremely unsafe.
  - You can use OAuth. It authenticates you with google server and gives the third party an access token with limited scopes "drive-files" for the previous example.
### Authentication using OAuth
