---
title: Airbitz Core Javascript API Reference

language_tabs:
  - Code

toc_footers:
  - <a href='https://developer.airbitz.co'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction

Welcome to the Airbitz Core Javascript API!  The Airbitz Core Javascript
API makes securing data easy for developers.  This library makes your
user's data secure and 100% private so that only end-users can access it.

This functionality is particularly well-suited for blockchain applications that
need to secure and backup private keys, but it can also be used to augment
existing applications, making them more private and more secure.

# Getting Started

You'll need to build `abc.js` to include into your own application.

`$ git clone https://github.com/airbitz/airbitz-core-js`

`$ cd airbitz-core-js`

`$ npm install`

`$ npm run webpack`

Now you can copy `abc.js` into your project.

# Authentication

The first step in using `abc.js` is to instantiate an `abc.Context` object.
You'll need a developer API key in order to do so.  You can register for an API
key at our [developer portal](https://developer.airbitz.co).

You'll be required to login with BitId, another technology that `abc.js` is
able to easily support.

> Example code

```javascript
var context = new abc.Context('YOUR_API_KEY');
```

# Classes

## Context Class

The context class is required to interact with the Airbitz Core API. From this
class you can create accounts, login and query the Airbitz servers.

```javascript
Context({
    usernameAvailable: function() {},
    accountCreate: function() {},
    passwordLogin: function() {},
    pinExists: function() {},
    pinLogin: function() {}
})
```

## Account Class

The account object provides access to the secured data and provides various
operations on the account for example [`logout`](#logout) and [`pinSetup`](#pin-setup).

```javascript
Account({
    pinSetup: function() { },
    logout: function() { },
    dataKey: "...",
    syncKey: "...",
    rootKey: "..."
})
```

# Functions and Methods

## Username Available

This method allows you to check if a particular username is available.

Parameter | Description
--------- | -----------
username  | the new user's username
callback  | callback with either an error code or an account object

> Example code

```javascript
context.accountCreate('username', 'password', function(err, result) {
    if (err) {
        console.log(err);
    } else {
        console.log(result);
    }
});
```

## Create Account

This method allows you to create new accounts for the user.

Parameter | Description
--------- | -----------
username  | the new user's username
password  | the new user's password
callback  | callback with either an error code or an account object

> Example code

```javascript
context.accountCreate('username', 'password', function(err, result) {
    if (err) {
        alert("Registration Failed: " + err);
    } else {
        var account = result;
    }
});
```


## Password Login

Password logins are the most typical way for a user to authenticate themselves.
If a user successfully logs in, you'll be returned an `Account` object. At the
moment, the account contains the `pinSetup` method and holds keys and private
data for the account.

Parameter | Description
--------- | -----------
username  | the new user's username
password  | the new user's password
callback  | callback with either an error code or an account object

> Example code

```javascript
context.passwordLogin('username', 'password', function(err, result) {
    if (err) {
        alert("Registration Failed: " + err);
    } else {
        var account = result;
    }
});
```

## PIN Setup

If a PIN is setup for an account, a user can quickly login without needing to
type in their entire password. In order to take advantage of this
functionality, the user must already be logged in so `pinSetup` can be called
on the `account` object.

Parameter | Description
--------- | -----------
pin | the pin to login with on the current device

> Example code

```javascript
account.pinSetup('pin', function(err, result) {
    if (err) {
        alert("Registration Failed: " + err);
    } else {
        alert("PIN setup");
    }
});
```

## PIN Login

PIN login can only be used on an account that has previously logged in with
`passwordLogin` and that has `pinSetup` called as well.

Parameter | Description
--------- | -----------
pin       | the login pin specified in `pinSetup`
callback  | callback with either an error code or an account object

> Example code

```javascript
context.pinLogin('username', 'pin', function(err, result) {
    if (err) {
        alert("Registration Failed: " + err);
    } else {
        var account = result;
    }
});
```

## Logout

Logout clears the account object, nulling out the keys. Since there is no
"session" in the typical sense, if the keys in the account are null, the user
is effectively logged out. In order to regain access to the keys again, the
user will have to login again.

> Example code

```javascript
// Not much to see here, just log out
account.logout();
```

# Errors

All errors in the API are Javascript error objects. The message will either be
the error that occurred, or javascript object with a server response.

