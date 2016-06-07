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
library makes securing data easy for developers.  This library makes your
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

> To authenticate, you need include your API key when instantiating a new `abc.Context`:

```javascript
var ctx = new abc.Context('YOUR_API_KEY');
```

> Once you have the context object, you can begin securing your data.

# Accounts

## Create Account

```javascript
ctx.accountCreate('username', 'password', function(err, result) {
    if (err) {
        alert("Registration Failed: " + err);
    } else {
        var account = result;
    }
});
```

> If successful the above `accountCreate` function returns an `Account` object in the results field. It looks like this:

```json
{
    "authId": "UbeR8lwlogYSAk2h2arplNzXXKoQbd10Y9IlwY+oDUc=",
    "authKey": "...",
    "ctx": Context,
    "dataKey": "..."
    "rootKey": "..."
    "syncKey": "..."
    "username": "airbitz-js-user"
}
```

## PIN setup

If a PIN is setup for an account, a user can quickly login without needing to
type in their entire password. In order to take advantage of this
functionality, the user must already be logged in so `pinSetup` can be called
on the `account` object.

```javascript
account.pinSetup('pin', function(err, result) {
    if (err) {
        alert("Registration Failed: " + err);
    } else {
        alert("PIN setup");
    }
});
```

## Password Login

Password logins are the most typical way for a user to authenticate themselves.
If a user is able to login, you'll be returned an `Account` object.

```javascript
ctx.passwordLogin('username', 'password', function(err, result) {
    if (err) {
        alert("Registration Failed: " + err);
    } else {
        var account = result;
    }
});
```

> If successful, the response is the same as `accountCreate` function. An `Account` object is returned in the the results field.

```json
{
    "authId": "UbeR8lwlogYSAk2h2arplNzXXKoQbd10Y9IlwY+oDUc=",
    "authKey": "...",
    "ctx": Context,
    "dataKey": "..."
    "rootKey": "..."
    "syncKey": "..."
    "username": "airbitz-js-user"
}
```

## PIN Login

```javascript
ctx.pinLogin('username', 'pin', function(err, result) {
    if (err) {
        alert("Registration Failed: " + err);
    } else {
        var account = result;
    }
});
```

> If successful, the response is the same as `accountCreate` function. An `Account` object is returned in the the results field.

```json
{
    "authId": "UbeR8lwlogYSAk2h2arplNzXXKoQbd10Y9IlwY+oDUc=",
    "authKey": "...",
    "ctx": Context,
    "dataKey": "..."
    "rootKey": "..."
    "syncKey": "..."
    "username": "airbitz-js-user"
}
```

# Errors

All errors in the API are Javascript error objects. The message will either be
the error that occurred, or javascript object with a server response.

```json
{
    "authId": "UbeR8lwlogYSAk2h2arplNzXXKoQbd10Y9IlwY+oDUc=",
    "authKey": "...",
    "ctx": Context,
    "dataKey": "..."
    "rootKey": "..."
    "syncKey": "..."
    "username": "airbitz-js-user"
}
```


