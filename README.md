# Passport-BaseCRM

[![Build Status](https://secure.travis-ci.org/reydelleon/passport-basecrm.png)](https://travis-ci.org/reydelleon/passport-basecrm)

[Passport](http://passportjs.org/) strategy for authenticating with [BaseCRM](https://getbase.com/)
using the OAuth 2.0 API. Visit [Base Developers](https://dev.futuresimple.com/docs/rest/articles/introduction)
to get familiar with their API. You need to register your application with Base to be able to 
access their API.

This module lets you authenticate using BaseCRM in your Node.js applications.
By plugging into Passport, BaseCRM authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-basecrm

## Usage

#### Configure Strategy

The BaseCRM authentication strategy authenticates users using a BaseCRM account
and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts
these credentials and calls `done` providing a user, as well as `options`
specifying a client ID, client secret, and callback URL.

    passport.use(new BaseCRMStrategy({
        clientID: BaseCRM_CLIENT_ID,
        clientSecret: BaseCRM_CLIENT_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/basecrm/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ basecrmId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'basecrm'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/basecrm',
      passport.authenticate('basecrm'));

    app.get('/auth/basecrm/callback', 
      passport.authenticate('basecrm', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Examples

For a complete, working example, refer to the [login example](https://github.com/reydelleon/passport-basecrm/tree/master/examples/login).

## Tests

    $ npm install --dev
    $ make test

## Credits

  - [Jared Hanson](http://github.com/jaredhanson)

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2015 Reydel Leon <[http://jaredhanson.net/](http://jaredhanson.net/)>

