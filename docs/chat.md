
# Chat API

It is easy to write a chat client that talks with a Juji chatbot via Juji Chat API. For example, it takes less than 200 line of Javascript code to write a client that chats with a Juji bot, see [sample code written in node.js on github](https://github.com/juji-io/cli-client). 

Juji's chat experience is built on top of [WebSocket](https://en.wikipedia.org/wiki/WebSocket) to push data to the client. This requires using [GraphQL subscription](https://facebook.github.io/graphql/June2018/#sec-Subscription-Operation-Definitions) to enable the server to push data to your client. Invoking a GraphQL subscription must be done over WebSocket because data will be streamed in and the connection must be kept open. Clients can be written in any programming language that supports Websocket and GraphQL subscriptions.

The following steps are required to initiate a chat session via the API:

## Create participation

First, note the [Web release URL of the REP](/#create-your-first-chatbot), e.g.
`https://juji.ai/pre-chat/mycorp/2`. Make a HTTP `POST` request to that URL
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
  "websocketUrl": "wss://juji.ai/api/v1/ws"
}
```

The returned JSON object contains two pieces of information needed to initiate a WebSocket connection to start the chat: `participationId` and `websocketUrl`.

Failed `POST` request returns a JSON object with an `error` field with an error message string.

## Establish WebSocket connection

A WebSocket connection with the server can now be established by doing a HTTP `GET`
on the returned `websocketUrl` value above.

A successful `GET` request will upgrade the connection to the WebSocket protocol, or an
error message will be returned.

## Receive chat messages via GraphQL subscription

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

`type` is a required field of Juji chat message. Currently, chat message could be one of the following types:

Type | Sender | Description
---|---|---
`user-joined` | server | REP or user have joined the chat, the start of a participation
`normal` | both | Normal chat messages
`user-left` | server | REP ends the participation
`typing` | client | User is typing
`keep-alive` | both | Server sends during idle to keep connection alive, client can send too
`connection-closed` | server | Server detected that the WebSocket connection to client is lost
`debug` | server | Debug information from the server

For all the possible fields of the chat subscription, please consult GraphiQL, and
look under "subscriptionRoot" - "chat" - "ChatMessage".

For example, if you want the REP to ask choice questions in your chat, you need
to add the fields "display" (for displying the choice question) and "move" (for sending user moves that respond to the choice questions) in the subscription.

```graphql
subscription {
    chat(input: {
        participationId: "5c3bcc2a-9ce5-40a7-b1da-80c065e283b0"
    }) {
        type
        role
        text
        display {
          type
          data {
            type
            gid
            questions {
              kind
              wording
              heading
              qid
              choices {
                text
                value
                other
              }
            }
          }
        }
        move {
          value
          text
          question
          gid
        }
    }
}
```

## Send chat messages

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

If you are sending response to a choice question, the input should include a "move"
field.
