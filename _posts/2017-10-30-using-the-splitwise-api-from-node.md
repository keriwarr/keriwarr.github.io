---
layout:    post
title:     "Using the Splitwise API from Node"
date:      2017-10-30
tags:      coding
---

# *WORK IN PROGRESS*

# Using the Splitwise API from Node

**tl;dr** There is a full, usable code example at the [bottom](#all-together).

This past weekend I was tinkering around with an idea that involved querying the [Splitwise API](http://dev.splitwise.com/). Talking to their API requires authorizing using OAuth. Unfortunately, OAuth was (and still is) completely opaque to me. So if you're like me and just want to use the darn API, here are a couple striaghtforward examples of how you can do that!

## Set-up

I will be using `node v8.4.0` and the npm package [`oauth@0.9.15`](https://www.npmjs.com/package/oauth).

If you would like to follow along, I recommend that you install node using [`nvm`](https://github.com/creationix/nvm), and then you can install oauth with: `npm i --save oauth@0.9.15`.

## Step 0: Register your Splitwise application

In order to talk to Splitwise, you will need keys issued by Splitwise. You can get them [Here](https://secure.splitwise.com/oauth_clients)!

## Step 1: Initialize OAuth

We will talk to the Splitwise API using an instance of the OAuth class, created by passing in the client keys given to you by Splitwise.

```javascript
const SPLITWISE_CONSUMER_KEY = 'your key here';
const SPLITWISE_CONSUMER_SECRET = 'your secret here';
const { OAuth2 } = require('oauth');
const oauth2 = new OAuth2(
  SPLITWISE_CONSUMER_KEY,
  SPLITWISE_CONSUMER_SECRET,
  'https://secure.splitwise.com/',
  null,
  'oauth/token',
  null,
);
```

## Step 2: Get your access token

The keys you provided above are not actually used to make reads and writes to Splitwise. Rather, they're used to get a token which is itself used to make reads and writes.

```javascript
oauth2.getOAuthAccessToken('',
  { grant_type: 'client_credentials' },
  (_, token) => console.log(token),
);
```

## Step 3: Make a call to the API!

`get_current_user` is one of many available endpoints.

```javascript
const API_URL = 'https://secure.splitwise.com/api/v3.0/';
oauth2.get(`${API_URL}get_current_user/`,
  token,
  (_, data) => {
    const user = JSON.parse(data).user;
    console.log(user);
  },
);
```

Remember that you can only make this call using the `token` from step two.

## All together

```javascript
const { OAuth2 } = require('oauth');

const SPLITWISE_CONSUMER_KEY = 'your key here';
const SPLITWISE_CONSUMER_SECRET = 'your secret here';
const API_URL = 'https://secure.splitwise.com/api/v3.0/';

const oauth2 = new OAuth2(
  SPLITWISE_CONSUMER_KEY,
  SPLITWISE_CONSUMER_SECRET,
  'https://secure.splitwise.com/',
  null,
  'oauth/token',
  null,
);

oauth2.getOAuthAccessToken('',
  { grant_type: 'client_credentials' },
  (_, token) => {
    oauth2.get(`${API_URL}get_current_user/`,
      token,
      (_, data) => {
        const user = JSON.parse(data).user;
        console.log(user);
      },
    );
  },
);
```

This works just fine, but the nested callback pattern is not very nice. If we needed to make more API calls using the result of `get_current_user` it would get even more messy.

## Using Promises instead of callbacks

As an alternative to the callback pattern, we can use Promises instead! I think that the are much nicer to look at, and to reason about. Node gives us a utility method which allows us to convert standard callback consuming methods into promise returning methods. This is possible because the oauth methods that we're using behave in the way that `util.promisify` expects: they consume the callback as the last argument.

```javascript
const { OAuth2 } = require('oauth');
const { promisify } = require('util');

const SPLITWISE_CONSUMER_KEY = 'your key here';
const SPLITWISE_CONSUMER_SECRET = 'your secret here';
const API_URL = 'https://secure.splitwise.com/api/v3.0/';

const oauth2 = new OAuth2(
  SPLITWISE_CONSUMER_KEY,
  SPLITWISE_CONSUMER_SECRET,
  'https://secure.splitwise.com/',
  null,
  'oauth/token',
  null,
);

const getOAuthAccessToken = promisify(
  oauth2.getOAuthAccessToken.bind(
    oauth2, '', { grant_type: 'client_credentials' }
  ),
);
const getCurrentUser = promisify(
  oauth2.get.bind(oauth2, `${API_URL}get_current_user/`),
);

getOAuthAccessToken()
  .then(getCurrentUser)
  .then(JSON.parse)
  .then(data => console.log(data.user));
```

## Notes

The Splitwise API has some serious usability issues. I'm currently working on a little wrapper library to make it a bit more useable. Stay tuned!

Thanks for reading!

## TO-DO
 - how to do this with just `curl`
 - how to do this without imported packages
 - how to make a POST
