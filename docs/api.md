# API Reference

Juji exposes the same API that powers our Web application to our users.

## Introduction

The Juji API is based on [GraphQL](https://graphql.org). We support
cross-origin resource sharing (CORS) so you can interact with Juji from any
client-side application thats support GraphQL. The API endpoint is https://juji.io/api/graphql

Juji API is explorable and executable through
[GraphiQL](https://juji.io/graphiql/graphiql.html) in-browser IDE.  Once you've
logged in to Juji platform, you can access the [GraphiQL
](https://juji.io/graphiql/graphiql.html) IDE.  This API reference covers only
important concepts of using Juji API. Please use the interactive
[GraphiQL](https://juji.io/graphiql/graphiql.html) to read the detailed documentation of all Juji GraphQL API calls.

<p align="center"><img src="../img/graphiql.png" alt="GraphiQL" width="650"/></p>

## Sample Application

To demonstrate the use of our API, we also maintain a command line based Juji client
written in node.js. You can play with the client to see what the API offers:

```
npm install juji-client
```

The MIT licensed source code of the client is at https://github.com/juji-io/cli-client

## Domain Nouns

To effectively leverage the API, it is useful to understand the data schema of Juji platform. Juji data is organized with the following domain nouns.

### Brand

A brand is synonymous to an organization.

### Engagement

An engagement is a chatbot project created under a brand.

### REP

REP is abbreviation for Responsible Empathetic Persona. It is the identity of
a chatbot, with a name and a personality. Each engagement has a REP.

### Release

A release represents a versioned deployment of one engagement.
Thus an engagement may have multiple releases. This allows you to refine your
bot without impacting your production release.

### Script

Each release is associated with a corresponding script in [REP Language](/reference/). The script is identified by a unique namespace. The namespace has a format `<brand-name>.<engX>.<rep-name>`, where `X` is the sequence number of the engagement, e.g. `mycorp.eng3.kaya`

### Question

REP often asks questions in a chat. Each question is associated with the namespace in
which it resides, as well as a question id that is unique in that namespace.

### Participation

A participation represents one instance of a conversation by an end user with a REP.
A participation is always associated with a release.

### Answer

Each end users answer to REP's question is recorded, along with the participation
in which the question is answered.

## Chat

Juji's chat experience is built on top of [WebSocket](https://en.wikipedia.org/wiki/WebSocket) to push data to the client. This requires using [GraphQL subscription](https://facebook.github.io/graphql/June2018/#sec-Subscription-Operation-Definitions) to enable the server to push data to your client. Invoking a GraphQL subscription must be done over WebSocket because data will be streamed in and the connection must be kept open.

The following steps are required to initiate a chat session via the API:

### Create participation

First, note the [Web release URL of the REP](/#create-your-first-chatbot), e.g.
`https://juji.io/pre-chat/mycorp/2`. Make a HTTP `POST` request to that URL
with the following form data:

Field Name | Required?
---|---
`firstName` | Yes
`lastName` | No
`email` | No

Only first name is required, so that the bot can address the user.

A successful `POST` request returns a JSON object looks like this:

```json
{
  "participationId": "5c3bcc2a-9ce5-40a7-b1da-80c065e283b0",
  "websocketUrl": "wss://juji.io/api/v1/ws"
}
```

The returned JSON object contains two pieces of information needed to initiate a WebSocket connection to start the chat: `participationId` and `websocketUrl`.

Failed `POST` request returns a JSON object with an `error` field with an error message string.

### Establish WebSocket connection

A WebSocket connection with the server can now be established by doing a HTTP `GET`
on the returned `websocketUrl` value above.

A successful `GET` request will upgrade the connection to the WebSocket protocol, or an
error message will be returned.

### Receive chat messages via GraphQL subscription

A listener should be registered to watch the status of the Websocket connection,
e.g. using browser JavaScript's `WebSocket.onopen` event listener.  When the connection
is open, the listener should send a chat subscription GraphQL query to the server
over the WebSocket connection. The subscription query looks like this:

```graphql
subscription {
    chat(input: {
        participationId: "5c3bcc2a-9ce5-40a7-b1da-80c065e283b0"
    }) {
        type
        role
        text
    }
}
```
A successful subscription will result in the server sending two messages
announcing that the user and the REP have joined the chat:
```json
{
  "data": {
    "chat": {
      "type": "user-joined",
      "role": "user",
      "text": null
    }
  }
}

{
  "data": {
    "chat": {
      "type": "user-joined",
      "role": "rep",
      "text": null
    }
  }
}
```

Followed by REP's chat messages if this REP is configued to speak first, e.g.

```json
{
  "data": {
    "chat": {
      "type": "normal",
      "role": "rep",
      "text": "Hello, John! I am Juji, your virtual interviewer."
    }
  }
}
```
where the "normal" type is for normal chat messages.

### Send chat messages

The client should send the chat messages over WebSocket connection. The message
is encoded in a `saveChatMessage` GraphQL mutation, which looks like this:

```graphql
mutation {
    saveChatMessage(input: {
        type: "normal"
        pid: "5c3bcc2a-9ce5-40a7-b1da-80c065e283b0"
        text: "Hello, nice to meet you."
    }) {
        success
    }
}

```
where the `pid` field should has the same value as the `participationId` received.

If successful, the client will receive a status message:
```json
{
  "data": {
    "saveChatMessage": {
      "success": true
    }
  }
}
```

## Data Access

You can access meta data as well as results about your chat engagements over the
GraphQL API at https://juji.io/api/graphql

An example GraphQL query to list all engagements of a brand:

```graphql
query
  engagements($brandName: String!) {
    getEngagementsByBrand(brandName: $brandName) {
        name
        order
        status
    }
  }
```

with the variable `brandName` specified in an JSON object:
```json
{
  brandName: "mycorp"
}
```

Consult the documentation of your GraphQL client library on the details of submitting
GraphQL queries.

### Authentication

Juji API data access operations require authentication.  The authentication is
based on [JSON Web Token (JWT)](https://en.wikipedia.org/wiki/JSON_Web_Token).

Once you have created an account at https://juji.io/signup, to authenticate to
the API, supply your email and password to the `authenticate` GraphQL mutation
and request the `token` field in the response, e.g.

```graphql
mutation
  authenticate($input: AuthenticateInput!) {
    authenticate(input: $input) {
      token
    }
  }
```
where the variable input should be a JSON object with `email` and `password` fields.

If successful, a JSON object is returned with a token, e.g.
```json
{
  data: {
    authenticate: {
      token: "a very long random looking string"
    }
  }
}
```

For all subsequent API calls, add the returned token in the
`Authorization` header of the request with the string `Bearer ` prefixed to the
token. For example, if the returned token was `abc` then the `Authorization`
header would be `Bearer abc`.

Note that all API calls must be made over HTTPS and that as of now, the returned token is valid for up to 10 hours.

### Output Format

Our API can return data in JSON, [EDN](https://github.com/edn-format/edn) as well as
[Transit](https://github.com/cognitect/transit-format) format.

You can specify how you want to receive API responses by including the `Accept` header set to any one of:

* `application/json` (default)
* `application/edn`
* `application/transit+json`

The advantages of EDN and Transit are richer data types. With Transit you also get a more efficient over the wire format.

### Errors

GraphQL always returns a 200 HTTP response status code, so we have to rely on
the `errors` field of the response to check for errors.

Per the GraphQL specification, `errors` is an array of maps (dictionaries).  Each error map will have the following keys `message`, `category`, `kind` and `data`.  `data` is any valid `JSON` or `EDN` value and the other fields are all strings.  There are four (4) broad categories of errors `authentication`, `authorization`, `validation` and `unexpected`.  Within each category, `kind` explicitly identifies the actual error.

For example, an authentication errors look like:
```json
{
  "category": "authentication",
  "kind":     "auth.error/not-authenticated",
  "message":  "The operation requires you to be authenticated.",
  "data":     {}
}
```

### Websocket

Some computational intensive API requests are handled with Websockt, so the results
can stream in when they become available. Since WebSocket requests cannot set custom headers, the JWT token should be sent as a query parameter `auth-token`.

## Upload Data for Analysis

It is possible to access Juji's analytics capabilities without using the chat platform. However, the same authentication requirement for data access described above is necessary.

Currently, we offer individual traits analysis, where our models infer an
individual's personality and other individual traits using text that he or she has
written.

The data analysis endpoint is https://juji.io/api/analyze

The input file is expected to be `POST` as a `file` field in `multipart/form-data`.

The input file can be either a JSON or CSV file with corresponding file suffix.
If the input is CSV, we expect the first column is named `id`, and the second
`text`.  If the input is JSON, we similarly expect an array of objects, where
each object has two fields: `id` and `text`. `text` will be a concatenation of
an individual's written text into a single string, and `id` be any string that
is unique among the input rows/objects.

The output is streamed back in CSV format, where the first row is the header with the names of the traits. The values of the traits are percentage.

Juji does not retain the uploaded files, as they are immediately discarded after
the output is returned.
