# Juji API 

Two types of Juji API are provided - Juji Core API and Juji Application API. The [core API](meta.md) is independent of the Juji Application, it can be used in many applications beyond chatbots. On the other hand, the [application API](chat.md) provides a way to programmtically access the Juji Platform and its conversations.

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

## Domain Nouns

To effectively leverage Juji API, it is useful to understand the data schema of Juji platform. Juji data is organized with the following domain nouns.

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

Each release is associated with a corresponding script in [REP Language](../reference/). The script is identified by a unique namespace. The namespace has a format `<brand-name>.<engX>.<rep-name>`, where `X` is the sequence number of the engagement, e.g. `mycorp.eng3.kaya`

### Question

REP often asks questions in a chat. Each question is associated with the namespace in
which it resides, as well as a question id that is unique in that namespace.

### Participation

A participation represents one instance of a conversation by an end user with a REP.
A participation is always associated with a release.

### Answer

Each end users answer to REP's question is recorded, along with the participation
in which the question is answered.
