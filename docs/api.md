# Juji API 

Juji exposes the same API that powers our Web application to our users.

## GraphQL

The Juji API is based on [GraphQL](https://graphql.org). We support
cross-origin resource sharing (CORS) so you can interact with Juji from any
client-side application that supports GraphQL. 

Once you've logged in to Juji platform, you can access the in-browser [GraphiQL](https://juji.ai/graphiql/graphiql.html) IDE to explore Juji API and execute queries.  

<p align="center"><img src="../img/graphiql.png" alt="GraphiQL" width="650"/></p>

This API reference covers only
important concepts of using Juji API. Please use the interactive
[GraphiQL](https://juji.ai/graphiql/graphiql.html) IDE to read the detailed documentation of all Juji GraphQL API calls.

For your code to access the API, put this GraphQL API endpoint `https://juji.ai/api/graphql` in your code. Please note: this URL is for your code to access, not a destination for human to visit in browser, you will get `{"error": "Unknown server resource."}` if you open it with a browser.

## Authentication

Most Juji API endpoints requires authentication. Two types of authentication are supported.

### JSON Web Token (JWT) Authentication

This authentication is based on JWT (https://en.wikipedia.org/wiki/JSON_Web_Token).

Once you have created an account at https://juji.ai/signup, to authenticate to the API, supply your email and password to the `authenticate` GraphQL mutation and request the `token` field in the response, e.g.

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

For all subsequent API calls, add the returned token in the `Authorization` header of the request with the string `Bearer ` prefixed to the token. For example, if the returned token was `abc` then the `Authorization` header would be `Bearer abc`.

Note that all API calls must be made over HTTPS and that as of now, the returned token is valid for up to 10 hours.

### API KEY Authentication

API key can be used as a long lasting token for autentication. Once you obtained the key, you can used it for years. So it is useful if you want to build some integration with Juji on your product. 

To obtain the API key, you will need to do the following:

1. Log in to your Juji account on juji.io
2. In the dashboard, click the top right button and select Account
  <p align="center"><img src="../img/visit-account-page.png" alt="Visit Account Page" width="650px"/></p>
3. In the Account page, select "APIKEY" then select "Generate New API Key" to get one
  <p align="center"><img src="../img/generate-new-api-key.png" alt="Generate New API Key" width="650px"/></p>
4. Copy the generated API key somewhere secure and don't tell anyone :) Note that you will only see the API key on Juji website once. If you lost it, you will need to generate a new one.
  <p align="center"><img src="../img/generated-api-key-example.png" alt="Generated API Key Example" width="650px"/></p>

Once you have the API key, you can use the basic auth method to authenticate your API calls. Use "apikey" as the username and your API key as the password. Below is an example in Postman:
<p align="center"><img src="../img/postman-api-key-example.png" alt="Postman API Key Example" width="650px"/></p>
In cURL you can use `-u` or `--header`:
```
-u 'apikey:cd177690b1e3484b8c3d3e0e27bce4a2'

--header 'Authorization: Basic YXBpa2V5OmNkMTc3NjkwYjFlMzQ4NGI4YzNkM2UwZTI3YmNlNGEy'
```

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

