# Data Access

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

## Authentication

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

## Output Format

Our API can return data in JSON, [EDN](https://github.com/edn-format/edn) as well as
[Transit](https://github.com/cognitect/transit-format) format.

You can specify how you want to receive API responses by including the `Accept` header set to any one of:

* `application/json` (default)
* `application/edn`
* `application/transit+json`

The advantages of EDN and Transit are richer data types. With Transit you also get a more efficient over the wire format.

## Errors

GraphQL always returns a 200 HTTP response status code, so we have to rely on
the `errors` field of the response to check for errors.

Per the GraphQL specification, `errors` is an array of maps (dictionaries).  Each error map will have the following keys `message`, `category`, `kind` and `data`.  `data` is any valid `JSON` or `EDN` value and the other fields are all strings.  There are five (5) broad categories of errors `authentication`, `authorization`, `validation`, `application` and `unexpected`.  Within each category, `kind` explicitly identifies the actual error.

For example, an authentication errors look like:
```json
{
  "category": "authentication",
  "kind":     "auth.error/not-authenticated",
  "message":  "The operation requires you to be authenticated.",
  "data":     {}
}
```

## Websocket

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

If the input is CSV, we expect the first column contains the identifier, and the
second column contains a concatenation of an individual's written text as a single string. The CSV file should *not* have header.

If the input is JSON, we expect an array of objects, where
each object has two fields: `id` and `text`. `text` will be a concatenation of
an individual's written text into a single string, and `id` be any string that
is unique among the input rows/objects.

The output is streamed back in CSV format, where the first row is the header with the names of the traits. The values of the traits are percentage.

Juji does not retain the uploaded files, as they are immediately discarded after
the output is returned.
