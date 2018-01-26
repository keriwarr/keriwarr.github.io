---
layout: post
title:  "Using the Splitwise API from Node"
date:   2017-10-30
tags:   coding, splitwise, javascript, node
---

# Using the Splitwise API from Node

**tl;dr** There is a full, usable code example [below](#all-together).
Note: All code examples are [MIT licensed](https://gist.github.com/keriwarr/a0075615e5335476a6838ec472794dd8#file-license-txt).

[Splitwise](https://www.splitwise.com/) is a really cool tool for splitting expenses with your friends. This past weekend I was tinkering around with an idea that involved querying the [Splitwise API](http://dev.splitwise.com/), but unfortunately there are a couple hurdles involved with using it, and I couldn't find any example code in JavaScript. So, if you're like me and just want to use the darn API, here are a couple straightforward examples of how you can do that!

## Set-up

The below code should work on all versions of [Node.js](https://nodejs.org/en/), starting with version 6. We will also use the npm package [`oauth@0.9.15`](https://www.npmjs.com/package/oauth).

If you would like to follow along, I recommend that you install node using [`nvm`](https://github.com/creationix/nvm), and then you can install oauth with: `npm i --save oauth@0.9.15`.

## Step 0: Register your Splitwise application

In order to interact with Splitwise, you will need keys issued by Splitwise. You can get them [Here](https://secure.splitwise.com/oauth_clients)!

## Step 1: Initialize OAuth

<script src="https://gist.github.com/keriwarr/a0075615e5335476a6838ec472794dd8.js?file=step-1.js"></script>

## Step 2: Get your access token

The keys you provided above are not actually used to make reads and writes to Splitwise. Rather, they're used to get a token which is itself used to make reads and writes.

<script src="https://gist.github.com/keriwarr/a0075615e5335476a6838ec472794dd8.js?file=step-2.js"></script>

## Step 3: Make a call to the API!


<script src="https://gist.github.com/keriwarr/a0075615e5335476a6838ec472794dd8.js?file=step-3.js"></script>

## All together

<script src="https://gist.github.com/keriwarr/a0075615e5335476a6838ec472794dd8.js?file=all-together.js"></script>

Note that `util.promisify` is only available starting with Node version 8. With older versions, you could use a package such as [promisify-node](https://www.npmjs.com/package/promisify-node).

<script src="https://gist.github.com/keriwarr/a0075615e5335476a6838ec472794dd8.js?file=promises.js"></script>

## Writing data to the API with a POST

A number of the Splitwise endpoints require that a POST request be made, but `oauth` doesn't natively support making POSTs. Here's a workaround:

<script src="https://gist.github.com/keriwarr/a0075615e5335476a6838ec472794dd8.js?file=posting.js"></script>

## Notes

The Splitwise API has some serious usability issues. I'm currently working on a little JavaScript wrapper library to make it a bit more usable. Stay tuned!

Thanks for reading! Please [let me know](mailto:keri@warr.ca) if you have any feedback.
