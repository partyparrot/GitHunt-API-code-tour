---
title: Resolvers
code: https://github.com/apollostack/GitHunt-API/blob/8549f50246b29e7f999a96ec15406c0a82713321/api/schema.js#L49-L61
---

The schema is just the first part of the puzzle. Now that we have described the available data, we need to tell our GraphQL server how to actually retrieve that data from the backend. That's where the resolvers come in! If you're familiar with REST API frameworks like Rails, you can think of the resolvers as little controller methods.

Resolvers are defined for each type in your schema, and here we're looking at the resolvers for the root Query type.

<a href="https://github.com/apollostack/GitHunt-API/blob/8549f50246b29e7f999a96ec15406c0a82713321/api/schema.js#L50-L54" id="feed-resolver"><h3>An example resolver</h3></a>

Here you can see the resolver for the feed field - it takes type, offset, and limit fields. The types have already been validated by GraphQL, but we still need to do a bit more validation to ensure the limit is not too large.

Then, we call the Entries model on the execution context. You can think of this as a *model* - the part of our code that knows how to deal with a specific type of backend. We don't want our GraphQL API layer and resolvers to worry about the specific details of querying SQL or fetching from GitHub, so we abstract that into a model object and put that onto the GraphQL execution *context*. The context doesn't have anything special about it-it's just an object that's passed to every resolver during GraphQL execution, and we can attach anything we want there.

Now, let's take a look at how we create the model objects and put them on the context.
