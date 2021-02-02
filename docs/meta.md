# Data Access

You can access meta data as well as results about your chat engagements over the
GraphQL API at https://juji.ai/api/graphql

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

Once you have created an account at https://juji.ai/signup, to authenticate to
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

The data analysis endpoint is https://juji.ai/api/analyze

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

## Download Chat Report with Personality Scores

This can be done with a GET request.

```shell
curl --location --request GET \
'https://juji.ai/api/reports?report-key=big5&auth-token=<token-value>&engagement-id=<engagement-id>&include-test-data=false'
```
As shown in the example above, send a GET request to `https://juji.ai/api/reports` and in the query string, set the `report-key` to "big5", then fill in the authentication token and engagement-id. 

The response will be a string of data in csv format. The data includes conversation responses and personality scores (if applicable) of each participatants of the given engagement. An exameple is shown below.
```shell
First Name,Last Name,Email,User Agent,Completion Code,Location,Start,Finish,Duration (minutes),Channel,Gather demographics: gender,Asked FAQs,Openness,Imagination,Artistic_Interest,Feelings,Adventurousness,Intellectual_Curiosity,Liberalism,Conscientiousness,Self_Efficacy,Orderliness,Dutifulness,Achievement_Striving,Self_Discipline,Cautiousness,Extroversion,Friendliness,Gregariousness,Assertiveness,Activity_Level,Excitement_Seeking,Cheerfulness,Agreeableness,Trust,Straightforwardness,Altruism,Cooperation,Modesty,Sympathy,Neuroticism,Anxiety,Anger,Depression,Self_Consciousness,Impulsiveness,Vulnerability
t1,,juji-user-548327dc-aa1f-4054-8ab4-a37e203e0c26@juji-inc.com,"Mozilla/5.0 (Macintosh; Intel Mac OS X 11_0_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36",,"{:timezone ""America/Los_Angeles"", :ip ""75.31.74.180"", :area-code 0, :dma-code 0, :city ""Sunnyvale"", :country-code ""US"", :metro-code 0, :longitude -122.0177, :postal-code ""94085"", :region ""California"", :org ""AS7018 AT&T Services, Inc."", :latitude 37.388596, :country-name ""United States""}",2021-01-20 23:24:06,,1,web,,,36.13541798365461,13.290581805094925,69.90396487992511,77.15953217560208,14.352478113721617,21.452611092889672,20.653339834694272,44.28527848667517,54.561037503275145,82.38387886673544,91.3233545692471,10.616104982056406,19.55675956043462,7.270535438302267,75.0045233539362,84.47620138247996,80.35717998131344,66.9274661801379,54.78618912035408,82.03414681082974,81.44595664850205,82.06446262912935,90.87886328546921,85.49197212672262,83.83877023080315,75.70710344618357,88.70960654682591,67.76046013877169,78.67947741962988,67.04116468437702,86.20177231934017,78.76662084022674,69.74154161142214,99.68790702532878,70.6378580370844
```