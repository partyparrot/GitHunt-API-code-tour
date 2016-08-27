---
title: Setting context
code: https://github.com/apollostack/GitHunt-API/blob/8549f50246b29e7f999a96ec15406c0a82713321/api/index.js#L67-L104
---

Here you can see where we attach our GraphQL schema to our Express web server using the apolloExpress middleware. Let's not worry about all of it yet.

<a href="https://github.com/apollostack/GitHunt-API/blob/8549f50246b29e7f999a96ec15406c0a82713321/api/index.js#L94-L103" id="feed-resolver"><h3>Middleware options</h3></a>

This is where we return the options for the middleware. You can read the full docs: http://docs.apollostack.com/apollo-server/setup.html#apolloExpress

One of the options is *context*, which, like we said before, is just an object passed into all of the resolvers. Here you can see we create the context object by adding the user field that represents the current user, and models for Repositories, Users, Entries, and Comments. Then we reference those models in our resolvers to fetch data.

So, we know how to add a model to the context. But how do we define one?
