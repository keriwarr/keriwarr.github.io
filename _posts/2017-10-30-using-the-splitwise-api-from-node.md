---
layout:    post
title:     "Using the Splitwise API from Node"
date:      2017-10-30
tags:      coding
---

# *WORK IN PROGRESS*

# Using the Splitwise API from Node

This past weekend I was tinkering around with an idea that involved querying the [Splitwise API](http://dev.splitwise.com/). Talking to their API requires authorizing using OAuth. Unfortunately, OAuth was (and still is) completely opaque to me. So if you're like me and just want to use the darn API, here are a couple striaghtforward examples of how you can do that!

## Set-up

I will use the npm package `oauth`. You can install it with: `npm i --save oauth`.

There are three steps to using the API:

## Step one

Create an OAuth object using the credentials provided to you by Splitwise:

```
const oauth2 = new OAuth2(
  process.env.SPLITWISE_CONSUMER_KEY,
  process.env.SPLITWISE_CONSUMER_SECRET,
  'https://secure.splitwise.com/',
  null,
  'oauth/token',
  null,
);
```

## Step two

Get your temporary access token:

```
let accessToken = null;
oauth2.getOAuthAccessToken('',
    { grant_type: 'client_credentials' },
    token => {
        accessToken = token;
    }
)
```

## Step three

Make a call!

```
const APIURL = 'https://secure.splitwise.com/api/v3.0/';
oauth2.get(`${APIURL}get_current_user/`,
    accessToken,
    body => {
        const user = JSON.parse(body).user;

        // do stuff with `user`
    }
);
```

Remember that you can only make this call after `accessToken` is assigned in step two.

## All together

```
const { OAuth2 } = require('oauth');

const oauth2 = new OAuth2(
  process.env.SPLITWISE_CONSUMER_KEY,
  process.env.SPLITWISE_CONSUMER_SECRET,
  'https://secure.splitwise.com/',
  null,
  'oauth/token',
  null,
);

const APIURL = 'https://secure.splitwise.com/api/v3.0/';
let accessToken = null;

oauth2.getOAuthAccessToken('',
    { grant_type: 'client_credentials' },
    (_, token) => {
        accessToken = token;

        oauth2.get(`${APIURL}get_current_user/`,
            accessToken,
            (_, body) => {
                const user = JSON.parse(body).user;

                // do stuff with `user`
            }
        );
    }
)
```

This nested callback pattern doesn't look very nice though, so....

## Using Promises instead of callbacks

Promises are way better than callbacks. Check it out!
{link to further learning}
brief description of the fact that we can use util.promisify becuase these methods adhere to Node callback standard

### Alternatively, we can pass in lambdas to promisify to make our promise-returning methods even simpler to use...:

## Example without importing any packages?

## Using cURL

These are the exact bare network requests you need to make:

## Notes

Their API sucks. I'm currently working on a little wrapper library to make it more useable. Stay tuned!

Thanks for reading!
