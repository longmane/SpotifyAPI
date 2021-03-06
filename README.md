# API Basics
Many applications these days have Application Programming Interfaces, or APIs. These allow a user with some basic web programming knowledge to use some of the app's functions and libraries and create custom features to suit their needs.
They utilize URIs to communicate after authenticating, allowing the custom code to make calls to the API functions.
This is incredibly useful for developers of third party applications need to pull data from or access the functionality of the application with the API.

![locky you](https://static1.squarespace.com/static/556460c9e4b0e65363ecdd12/t/583d40fe440243877a0c3ffa/1480409346401/)

# Security in APIs
APIs are incredibly widely used and people of all technical skill levels implement them.
No matter that skill level though, one aspect that often seems to be forgotten is security.
Both the application supplying the API and the users integrating it into whatever they are building need to be aware of the security risks and standards that should be followed.
Unfortunately, it's rare for security concerns to be addressed in the documentation, leaving a lot of people vulnerable without realizing it.
This guide aims to rectify that by providing basic concepts of secure coding practices, using the Spotify API as an example.

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

Authentication is a crucial aspect in using any functions of an API that pull data not publicly available, meaning the user must have an account of some sort. 
This process is realatively simple to implement but can be tough to understand conceptually. 
As long as the basic concepts make sense though, one can get it working in no time.
OAuth, the mechanism stated above is the method of authentication that Spotify uses, and is run by Google.
The code snippet below shows how to easily do this with a node.js script.

```javascript
var request = require('request'); 

var client_id = 'CLIENT_ID'; // Your client id
var client_secret = 'CLIENT_SECRET'; // Your secret

// your application requests authorization
var authOptions = {
  url: 'https://accounts.spotify.com/api/token',
  headers: {
    'Authorization': 'Basic ' + (new Buffer(client_id + ':' + client_secret).toString('base64'))
  },
  form: {
    grant_type: 'client_credentials'
  },
  json: true
};

request.post(authOptions, function(error, response, body) {
  if (!error && response.statusCode === 200) {

    // use the access token to access the Spotify Web API
    var token = body.access_token;
    var options = {
      url: 'https://api.spotify.com/v1/users/longmane',
      headers: {
        'Authorization': 'Bearer ' + token
      },
      json: true
    };
    request.get(options, function(error, response, body) {
      console.log(body);
    });
  }
});
```


### Scopes
Scopes let you specify exactly what type of data access your application needs. The generated access token will contain permissions for the scopes that the user has already granted for that client_id, if any. When not specifying any scopes the access token will allow access to certain publicly available information by default. The code snippet below shows how this would be basically implemented.

```javascript
app.get('/login', function(req, res) {
var scopes = 'user-read-private user-read-email';
res.redirect('https://accounts.spotify.com/authorize' + 
  '?response_type=code' +
  '&client_id=' + my_client_id +
  (scopes ? '&scope=' + encodeURIComponent(scopes) : '') +
  '&redirect_uri=' + encodeURIComponent(redirect_uri));
});
```

### Encryption
Encryption is generally used to hide information from those not authorized to view it. On the Internet, often SSL is used to encrypt HTTP messages, sent and received either by web browsers or API clients. However SSL is limited in that it only applies to the transport layer, leaving a need for added security.

Encryption and Signatures are often used in conjunction; the signature could be encrypted to only allow certain parties to validate if a signature is valid - or the encrypted data could be signed to further ensure that data is neither seen or modified by unwanted parties.
Signatures are used to ensure that API requests or response have not been tampered with while in transit. The message itself might be unencrypted, but must be protected against modification and arrive intact.

# Working with the Spotify API
The Spotify API requires that the user first sets up OAuth.
