---
title: Defining a model
code: https://github.com/apollostack/GitHunt-API/blob/8549f50246b29e7f999a96ec15406c0a82713321/api/github/models.js
---

Here, we'll look at the GitHub models, because they are much simpler than the SQL ones: https://github.com/apollostack/GitHunt-API/blob/8549f50246b29e7f999a96ec15406c0a82713321/api/sql/models.js

We want to focus on the structure of the code, rather than learning about how to write SQL queries in JavaScript.

You can see that the model is just a class with a set of methods that represent different ways of getting data of that type. This saves our resolvers from needing to worry about the URLs of the GitHub API.

You can see that the constructor of the model takes in something called a *connector*. This isn't a GraphQL-specific context, but it's a useful way of abstracting data fetching logic. In this case, the models deal with fetching a specific type of information, but the connector is the thing that abstracts away the semantics of fetching from the GitHub API. Turns out, there's a lot you can do to make fetching from the GitHub API better than a simple HTTP request, and we'll see that when we look at the connector next.
