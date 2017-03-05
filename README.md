# API Basics
Many applications these days have Application Programming Interfaces, or APIs. These allow a user with some basic web programming knowledge to use some of the app's functions and libraries and create custom features to suit their needs.
They utilize URIs to communicate after authenticating, allowing the custom code to make calls to the API functions.
This is incredibly useful for developers of third party applications need to pull data from or access the functionality of the application with the API.

# Security in APIs
APIs are incredibly widely used and people of all technical skill levels implement them.
No matter that skill level though, one aspect that often seems to be forgotten is security.
Both the application supplying the API and the users integrating it into whatever they are building need to be aware of the security risks and standards that should be followed.
Unfortunately, it's rare for security concerns to be addressed in the documentation, leaving a lot of people vulnerable without realizing it.
This guide aims to rectify that by providing basic concepts of secure coding practices, using the Spotify API as an example.

![locky you](https://static1.squarespace.com/static/556460c9e4b0e65363ecdd12/t/583d40fe440243877a0c3ffa/1480409346401/)

## Main Concepts
There are a few broad security topics that are particularly important when it comes to APIs.
These topics work to protect both the server side of the application and the developer using the API in their application.
When used in combination **Authentication**, **Scopes**, and **Encryption** can make a world of difference in the level of security.

### Authentication
It's most common to find authentication on the web implemented with a dialog that prompts for username and password. 
Sites with a higher level of security often use software certificates, hardware keys, and external devices for two-factor. 
APIs commonly to use some kind of access token, either obtained through an external process, often when signing up for the API, or through a separate mechanism like OAuth. 
The token is passed with each request to an API and is validated by the API before processing the request.
Once the user is authenticated, the system decides which resources or data to allow access to.

The image below illustrates the flow of Spotify's authentication process.
![go with the flow](https://developer.spotify.com/wp-content/uploads/2014/04/Authorization-Code-Flow-Diagram.png)

### Scopes

### Encryption

# Working with the Spotify API
The Spotify API requires that the user first sets up OAuth.
