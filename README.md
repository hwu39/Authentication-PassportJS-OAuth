# passportjs-google-oauth20

[Passport](http://passportjs.org/) strategies for authenticating with [Google](http://www.google.com/)
using OAuth 2.0.

This is a module that uses [passport-google-oauth20](http://www.passportjs.org/packages/passport-google-oauth20/).
with Google APIs for web application development with Node.js. 

# Description
This module allows users to sign up manually with an email address and password or a Google account with the use of a Google API. 
Users can add any secret messages to the MongoDB and all of them will be displayed anonymously once logged in. The subject of 
this module is to get familiarized with the modern passwordless login tools such as OAuth2.0. In addition to that, proper salting and
hashing techniques are implemented to improve password protection.

---


## Install

    $ npm install passport-google-oauth20
    
## Configure Strategy
The Google authentication strategy authenticates users using a Google account and OAuth 2.0 tokens. The client ID and secret obtained when creating an application are supplied as options when creating the strategy. The strategy also requires a verify callback, which receives the access token and optional refresh token, as well as profile which contains the authenticated user's Google profile. The verify callback must call cb providing a user to complete authentication.

```javascript
var GoogleStrategy = require('passport-google-oauth20').Strategy;

passport.use(new GoogleStrategy({
    clientID: GOOGLE_CLIENT_ID,
    clientSecret: GOOGLE_CLIENT_SECRET,
    callbackURL: "http://www.example.com/auth/google/callback"
  },
  function(accessToken, refreshToken, profile, cb) {
    User.findOrCreate({ googleId: profile.id }, function (err, user) {
      return cb(err, user);
    });
  }
));
```

## Authenticate Requests

Use passport.authenticate(), specifying the 'google' strategy, to authenticate requests.

For example, as route middleware in an Express application:

```javascript
<span>app.get('/auth/google',
    passport.authenticate('google', { scope: ['profile'] }));

app.get('/auth/google/callback', 
  passport.authenticate('google', { failureRedirect: '/login' }),
  function(req, res) {
    // Successful authentication, redirect home.
    res.redirect('/');
  });
```
