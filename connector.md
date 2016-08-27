---
title: The GitHub connector
code: https://github.com/apollostack/GitHunt-API/blob/8549f50246b29e7f999a96ec15406c0a82713321/api/github/connector.js
---

This is the definition of the GitHub connector. Basically, the idea is that it should abstract everything about calling the GitHub API in a secure and performant way. It does a few things:

  * Caches requests to the API using dataloader
  * Maintains a cache that keeps track of GitHub's eTags, which let us avoid going over GitHub's API limit
  * Keeps track of the GitHub API keys and makes sure to pass them with every request

<a href="https://github.com/apollostack/GitHunt-API/blob/8549f50246b29e7f999a96ec15406c0a82713321/api/github/connector.js#L20-L26" id="dataloader"><h3>Caching with DataLoader</h3></a>

This is the part where we use Facebook's dataloader library to cache requests. Basically, if we have several items in our feed posted by the same user, we don't want to send multiple requests to GitHub for the same user object, since those use up server resources and count against our API limit. DataLoader automatically de-duplicates the API URLs, and makes sure they are only fetched once per GraphQL query.

<a href="https://github.com/apollostack/GitHunt-API/blob/8549f50246b29e7f999a96ec15406c0a82713321/api/github/connector.js#L45-L49" id="etags"><h3>Working with GitHub eTags</h3></a>

Here, we check if we have already fetched this data from GitHub before, and make sure to send along the eTag we got from GitHub. This lets GitHub send back a 304 response if the data hasn't changed, which means we save the bandwidth of loading the data again and also save on our API rate limit.

<a href="https://github.com/apollostack/GitHunt-API/blob/8549f50246b29e7f999a96ec15406c0a82713321/api/github/connector.js#L10-L12" id="api-keys"><h3>API keys</h3></a>

Lastly, we pass in the GitHub API keys into the constructor. This lets the connector automatically pass those through, so we don't have to do it anywhere else in our code.

None of this code is GraphQL-specific - in fact, you might want a similar GitHub wrapper even if you're building a REST API. But GraphQL helps us organize our code so that we decouple the API layer and schema from the data fetching logic.
