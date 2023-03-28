# Programmatic Chatbots Creation and Deployment

<p align="center"><img src="../img/convert-chatflow.png" alt="Convert existing chatflow to Juji config-doc" width="650px"/></p>

This guide is for users who enjoy Juji chatbot's powerful dialog management, but prefer using their own interfaces to create chatflow. For example, one can take an existing chat flow created in another platform, convert it to [Juji's chatflow format](config-doc.md). Then use Juji APIs to create and deploy the chatbot on Juji. In other words, it is possible to programmatically create and deploy chatbots on the Juji platform. You just need to follow three simple steps:

1. [Log in to your Juji account](#create-a-juji-account-and-login)
2. [Create a chatbot and customize](#create-a-chatbot-and-customize-it)
3. [Launch your chatbot](#launch-your-chatbot)

## Create a Juji Account and Login

A valid Juji account is necessary for using most of the APIs. It is also the only step you have to complete using the Juji website. Simply go to [Juji Signup page](https://juji.ai/signup) to create an account if you haven't yet done so.

Once you have an account, you can use the `authenticate` [GraphQL](api.md#graphql) mutation to log into your account and start a session.
```javascript
mutation Authenticate($input: AuthenticateInput!){
	authenticate(input: $input) {
    	token
  	}
}
```
Store the value of the token. It will be used for [authentication](api.md#authentication) in other API calls.

You may also need your account's [brand id](nouns.md#brand), you can use the following GraphQL query to access it.
```javascript
query GetBrands{
	getBrands{
    	name
	}
}
```

## Create a Chatbot and Customize It

A chatbot lives in an [engagement](nouns.md#engagement). In order to customize a chatbot, you either creates an engagement or uses an existing engagement.

```javascript
// To create engagement with default blank template
mutation CreateEngagement($input: CreateEngagementInput!){
	createEngagement(input: $input) {
		engagement{
			name 
			id 
			order 
			status
		}
	}
}

// To list existing engagements
query Engagements($brandName: String!) {
	getEngagementsByBrand(brandName: $brandName) {
    	name
    	id
    	order
    	status
	}
}
```

Then you can 1) update your chatflow by uploading a [customized config-doc](config-doc.md) and/or 2) update your Q&As by uploading a [customized Q&A csv file](design.md#customize-qa-and-fallback).

```javascript
// Set isJson to true if the the config-doc is in JSON format,
// otherwise, Clojure EDN format is expected.
mutation UpdateChatConfig($input: UpdateChatConfigInput!){
    updateChatConfig(input: $input) {
        message
        success
    }
}
```

To update your Q&As, you will need to send a POST request. Below is a cURL snippet generated from Postman.
```bash
# overwrite is optional, remove it if you want to add the Q&As onto existing ones
curl --location --request POST 'https://juji.ai/api/faq-upload/<brand-id>/<engagement-order>' \
--header 'authorization: Bearer <token>' \
--form 'overwrite=1' \
--form 'file-content=ID,Question,Answer,Comment,Multi-turn Q&A,# of asking
help,Help,Here comes help!,,,
help,Can you help me?,,,,'
```

## Launch Your Chatbot

Once the chatbot is ready, you can deploy it by creating a [web release](release.md#deploy-to-web).

```javascript
mutation CreateRelease($input: CreateReleaseInput!){
	createRelease(input: $input) {
		id 
		order 
		type
	}
}
```

The web release can be accessed at `https://juji.ai/pre-chat/<engagement-id>` using a browser or API calls. Please refer to the [Juji chat API](cognitive-ai-chatbot-api.md) for details on how to use API calls to build conversational AI applications.

You can continue to improve your chatbot after you have made a release - simply update your config-doc and/or Q&As and then make a new release. The pre-chat URL above will always point to the latest web release.

## References

* Please read about Juji API [introduction](api.md) first for important API concepts to help you better understand this guide. Additional API documentation, such as [data model](nouns.md) and [Juji Cognitive Core API](psychographic-api.md)
* [Juji's GraphiQL](https://juji.ai/graphiql/graphiql.html) can be used to explore existing GraphQL APIs and their parameters.
* [Juji client github page](https://github.com/juji-io/cli-client#creating-a-new-chat-using-only-api-an-example) contains concrete examples written in JavaScript for all the API calls in this guide, please refer to it for detail.
