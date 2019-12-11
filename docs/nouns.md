
# Domain Nouns

To effectively leverage Juji API, it is useful to understand the data schema of Juji platform. Juji data is organized with the following domain nouns.

## Brand

A brand is synonymous to an organization.

## Engagement

An engagement is a chatbot project created under a brand.

## REP

REP is abbreviation for Responsible Empathetic Persona. It is the identity of
a chatbot, with a name and a personality. Each engagement has a REP.

## Release

A release represents a versioned deployment of one engagement.
Thus an engagement may have multiple releases. This allows you to refine your
bot without impacting your production release.

## Script

Each release is associated with a corresponding script in [REP Language](/reference/). The script is identified by a unique namespace. The namespace has a format `<brand-name>.<engX>.<rep-name>`, where `X` is the sequence number of the engagement, e.g. `mycorp.eng3.kaya`

## Question

REP often asks questions in a chat. Each question is associated with the namespace in
which it resides, as well as a question id that is unique in that namespace.

## Participation

A participation represents one instance of a conversation by an end user with a REP.
A participation is always associated with a release.

## Answer

Each end users answer to REP's question is recorded, along with the participation
in which the question is answered.

