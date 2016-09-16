# Google-OAuth2

is a library designed to make working with Google's Oauth2 API's more bearable.<br/>
taken from [treygriffith](https://github.com/treygriffith/google-oauth2)

As of now, it only supports one API, contacts, out of the box, but adding additional API's, either on the fly or permanently, is quite easy.

USAGE
------
```javascript
var oauth2 = new google_oauth2(MY_CLIENT_ID [, options]);

oauth2.authenticate(); //sends the user to the Google authorization endpoint

oauth2.authResponse(function(error, access_token) { //extract the access token
	if(access_token) {
		//execute some code here
	} else if(error) {
		//a response was attempted, but an error occurred
	} else {
		//there was nothing in the url fragment, in all likelihood, this was not a response to authentication
	}
});

oauth2.query(api [, options], function(error, results) {
	// execute some code on the returned values
});
```


---
# google-oauther
[clalimarmo](https://github.com/clalimarmo/google-oauther)

Simple Google OAuth2 module, for use in single page, client-side only
applications.  It opens a popup window to request permission, and stores the
auth token returned by Google.

## Usage

    var authenticator = require('google-oauther');

    authenticator.onAuthenticate(function(auth) {
      //stuff to do once the authenticator has authenticated user's profile info
      //(The auth parameter passed to the callback the authenticator, itself)
    });

    authenticator.run({
      scope: ['https://www.googleapis.com/auth/devstorage.read_write'],
      clientID: 'your-google-oauth2-client-id',
      tokenExpirationBuffer: 60000
    });

## Configuration

Required:

  * *scope* - the permissions to request from google
  * *clientID* - your google oauth2 client id

Optional:

  * *tokenExpirationBuffer* - number of milliseconds before the token actually expires,
    after which the authenticator will consider the token expired. Useful for getting a
    token, or preventing users from attempting unauthenticated requests, before the
    token expires.

## Methods

### onAuthenticate

Specify behavior that should occur once the user grants the requested
permissions. Do this before you call `run`

### run

Requests authentication from the user, and whatever permissions you specify
with the `scope` parameter.

### user

Returns the user profile information gleaned from an authenticated request to
https://www.googleapis.com/plus/v1/people/me

### token

Returns the auth token. Useful for subsequent requests to other Google APIs.

### reauthenticate

Does the same thing as run.

### tokenIsExpired

Indicates whether the token is expired or not.

## Notes

The authenticator always requests the 'profile' OAuth2 scope, in addition to
whatever scopes are specified in the call to `run`.

For the popup window to send the auth token returned by google back to the main
window, a global callback function is attached to the main window, called
`authenticatedWith`. Including the `google-oauther` module will attach this
callback function automatically; overwriting this function will break the
authenticator.
