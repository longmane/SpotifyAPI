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

# Main Concepts
There are a few broad security topics that are particularly important when it comes to APIs.
These topics work to protect both the server side of the application and the developer using the API in their application.
When used in combination **Authentication**, **Scopes**, and **Encryption** can make a world of difference in the level of security.

# Working with the Spotify API
The Spotify API requires that the user first sets up OAuth.
