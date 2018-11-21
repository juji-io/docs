# API Reference

## Introduction

The Juji API is based on [GraphQL](https://graphql.org). Our API can return data in JSON, EDN as well as Transit.  We support cross-origin resource sharing (CORS) so you can interact with Juji from any client-side web application.  Further, the API is explorable and executable through [GraphiQL](https://juji.io/graphiql/graphiql.html) once you've logged in.

## Authentication

Almost all Juji API operations require authentication.  To authenticate, supply the email and password to the `authenticate` mutation and request the `token` field in the response.  For all subsequent API calls, add the token in the `Authorization` header of the request with the string `Bearer ` prefixed to the token. If the returned token was `abc` then the `Authorization` header would be `Bearer abc`.  Note that all API calls must be made over HTTPS and that as of now, the returned token is valid for up to 10 hours.


## Errors

GraphQL always returns a 200 HTTP response status code, so we have to rely on the `errors` field of the response to check for errors. Per the GraphQL spec, `errors` is an array of maps (dictionaries).  Each error map will have the following keys `message`, `category`, `kind` and `data`.  `data` is any valid `JSON` or `EDN` value and the other fields are all strings.  There are four (4) broad categories of errors `authentication`, `authorization`, `validation` and `unexpected`.  Within each category, `kind` explicitly identifies the actual error.

For example, an authentication errors look like:
```json
"category": "authentication",
"kind":     "auth.error/not-authenticated",
"message":  "The operation requires you to be authenticated.",
"data":     {}
```


## JSON, EDN and Transit

You can specify how you want to receive API responses by including the `Accept` header set to any one of
* `application/json` (default)
* `application/edn`
* `application/transit+json`

The advantages of EDN and Transit are richer data types. With Transit you also get a more efficient over the wire format.

## Chat

Juji's chat experience is built on top of WebSockets to push data to the client. This requires using GraphQL subscriptions
to enable the server to push data to your client.

## Domain Nouns

### Brand
A brand is synonymous to an organization.

### Engagement
An engagement is a collection of chat bot projects under a brand.

### Release
A release represents a versioned deployment of your chat bot.  This allows you to refine your bot without impacting your production release.  Thus an engagement may have multiple releases.

### Participation
A participation represents one instance of a conversation with a bot and is associated with a release.
