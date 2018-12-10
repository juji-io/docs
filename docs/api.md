# API Reference

Juji exposes the same API that powers our Web application to our users.

## Introduction

The Juji API is based on [GraphQL](https://graphql.org). We support
cross-origin resource sharing (CORS) so you can interact with Juji from any
client-side application thats support GraphQL. The API endpoint is https://juji.io/api/graphql

Like many GraphQL APIs, Juji API is explorable and executable through
[GraphiQL](https://github.com/graphql/graphiql) in-browser IDE.  Once you've
logged in to Juji platform, you can access [the GraphiQL endpoint](https://juji.io/graphiql/graphiql.html).

## Authentication

Almost all Juji API operations require authentication.  The authentication is
based on [JSON Web Token (JWT)](https://en.wikipedia.org/wiki/JSON_Web_Token).

Once you have created an
account at https://juji.io/signup, to authenticate to the API, supply
your email and password to the `authenticate` mutation and request the `token`
field in the response.

For all subsequent API calls, add the returned token in the
`Authorization` header of the request with the string `Bearer ` prefixed to the
token. For example, if the returned token was `abc` then the `Authorization`
header would be `Bearer abc`.

Note that all API calls must be made over HTTPS and that as of now, the returned token is valid for up to 10 hours.

## Errors

GraphQL always returns a 200 HTTP response status code, so we have to rely on
the `errors` field of the response to check for errors.

Per the GraphQL specification, `errors` is an array of maps (dictionaries).  Each error map will have the following keys `message`, `category`, `kind` and `data`.  `data` is any valid `JSON` or `EDN` value and the other fields are all strings.  There are four (4) broad categories of errors `authentication`, `authorization`, `validation` and `unexpected`.  Within each category, `kind` explicitly identifies the actual error.

For example, an authentication errors look like:
```json
"category": "authentication",
"kind":     "auth.error/not-authenticated",
"message":  "The operation requires you to be authenticated.",
"data":     {}
```


## JSON, EDN and Transit

Our API can return data in JSON, [EDN](https://github.com/edn-format/edn) as well as
[Transit](https://github.com/cognitect/transit-format) format.

You can specify how you want to receive API responses by including the `Accept` header set to any one of:

* `application/json` (default)
* `application/edn`
* `application/transit+json`

The advantages of EDN and Transit are richer data types. With Transit you also get a more efficient over the wire format.

## Chat

Juji's chat experience is built on top of
[WebSocket](https://en.wikipedia.org/wiki/WebSocket) to push data to the client.

This requires using [GraphQL subscriptions](https://facebook.github.io/graphql/June2018/#sec-Subscription-Operation-Definitions) to enable the server to push data to your client.

The WebSocket is initiated by doing a HTTP `GET` on
`https://juji.io/api/v1/chsk`. Since WebSocket requests cannot set custom
headers, the JWT token should be sent as a query parameter `auth-token`.

Invoking a GraphQL subscription must be done over WebSocket because data will be streamed in and the connection must be kept open.

## Domain Nouns

### Brand
A brand is synonymous to an organization.

### Engagement
An engagement is a chatbot project created under a brand.

### Release
A release represents a versioned deployment of one engagement (chatbot project).
Thus an engagement may have multiple releases. This allows you to refine your
bot without impacting your production release.

### Participation
A participation represents one instance of a conversation by a user with a bot.
A participation is always associated with a release.