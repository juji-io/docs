# Juji API 

Juji exposes the same API that powers our Web application to our users.

## GraphQL

The Juji API is based on [GraphQL](https://graphql.org). We support
cross-origin resource sharing (CORS) so you can interact with Juji from any
client-side application thats support GraphQL. The API endpoint is `https://juji.ai/api/graphql`

Juji API is explorable and executable through
[GraphiQL](https://juji.ai/graphiql/graphiql.html) in-browser IDE.  Once you've
logged in to Juji platform, you can access the [GraphiQL
](https://juji.ai/graphiql/graphiql.html) IDE.  This API reference covers only
important concepts of using Juji API. Please use the interactive
[GraphiQL](https://juji.ai/graphiql/graphiql.html) to read the detailed documentation of all Juji GraphQL API calls.

<p align="center"><img src="../img/graphiql.png" alt="GraphiQL" width="650"/></p>

## Sample Application

To demonstrate the use of our API, we also maintain a command line based Juji client
written in node.js. You can play with the client to see what the API offers:

```
npm install juji-client
```

The MIT licensed source code of the client is at https://github.com/juji-io/cli-client
As you can see, it took less than 200 lines of JavaScript code to have a client
that chats with a Juji bot.

## What's Next

* [Juji Data Model](../nouns)
* [Chat API](../chat)
* [Data API](../meta)

