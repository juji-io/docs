# Concepts of Juji Platform

Juji leverages the fruits of half century of artificial
intelligence (AI) research, mainly in "Symbolic AI" to build a practical and
easy-to-use conversational agent authoring platform which makes sophisticated conversational
AI available to everyone.

The core of the Juji platform is a hybrid AI system
which marries Symbolic AI (characterized by a high-confidence solidity) and the latest deep learning
intelligence (AI) research to build a practical and easy-to-use conversational
agent authoring platform. The core of the Juji platform is a hybrid AI system
that marries the so called "traditional" or "Symbolic AI" and the state of art deep learning
(DL) and machine learning (ML) technologies in natural language processing (NLP).

To meet business requirements which demand flexibility, accountability and
explainability of AI systems, Juji developed a declarative production rule
language to glue together its advanced NLP
capabilities. Called **REP** (Responsible Empathetic Persona), the language compiler
and provides run-time **automatic dialog management**, which alleviates most of the time-consuming confusions,
burdens and pains often associated with developing anything but the most rudimentary conversational agent.
In other words our hybrid AI is baked in.  This is one of the central advantages of the Juji Platform.

So let's briefly go over the main concepts of REP language. If you need more detail take a look at [Language
Reference](reference.md).

## Topic

Topics are the primary building blocks of a REP driven conversation, which break
up the chat into some groups of turns according to semantic affinity. The
simplest topic may represent only one turn of the conversation, but many topics go
deeper and branch into nested followup topics.

Here is the definition of our first topic:

```clojure
(deftopic hello-world
  []
  []
  ["Hello world!"])
```

_Line 1_ declares the name of a new topic (deftopic) defined in this case as `hello-world`.

*Line 2* lists the parameters for the topic. In this case, there are none.

*Line 3* is a 'trigger'. Often this is a Boolean expression. As there is no trigger defined, the response always returns 'true'.
meaning that it always returns true.

*Line 4* is an action that the bot will take as a result of the action in the two lines above. Here it says "Hello world!"

### Rule

The pairing of a trigger with an action is known as a rule. When the conditions
of the trigger are met and the action is taken by the bot, we say that the rule is 'fired'.

### Followup Topic

When a rule is fired, its associated followup topics are 'primed', and automatically loaded as the first topics to be considered as the bot's suitable response.

```clojure
(deftopic hello-world
  []
  []
  ["Hello world!"]
  (_ [hello]
     ["Nice to meet you!"]))

```
*Line 5* starts with an anonymous topic definition, `_` , for a name or label if one doesn't come to mind. No paremeters are accepted. The line ends with a trigger pattern, which is the word 'hello'. If the word "hello" is contained in the user's response to the bot's initial "Hello world!", the action is triggered,

*Line 6* is the triggered action, In this case, a text response by the bot to reply "Nice to meet you!" to the user.

This time, instead of a default topic definition, let's go ahead and give our topic a proper definition instead. Let's call it "greeting".

```clojure
(deftopic greeting
  []
  [hello]
  ["Nice to meet you!"])

```

Now the `greeting` topic can be used as an followup topic in `hello-world` to
achieve the same thing.

```clojure
(deftopic hello-world
  []
  []
  ["Hello world!"]
  (greeting))

```

To extend the power of the topic as a building block, there can be multiple rules in a topic. And each rule may itself be
associated with zero or multiple embedded followup topics.

```clojure
(deftopic greeting
  []

  [:1 hello howdy hi]
  [(user-first-name) ", nice to meet you!"]

  [(> (max-similarity-score ["what's up"]) 0.9)]
  ["Nothing much, you?"]
  (handle-whats-up)

  [[:1 你 您]好]
  ["我很好，你好么?"]
  (continue-greeting-in-chinese)
  (ask-about-chinese-stock-market))

```
Line 4 is a _trigger_ pattern that requires user input to contain any one of "hello",
"howdy" or "hi". (No comma seperating keywords, and no multi-word keywords) to fire the rule. For details of the many patterns REP supports, see [Rule Patterns](reference.md#rule-pattern)

Line 5 is an _action_ that includes a [built-in system function](function.md) call
that returns the user's first name. In addition to producing text output,
functions can do arbitrary things. You can also write your own [user defined function](udf.md).

Line 7 is a trigger that contains a built-in function call that checks whether
the user input is very similar to the short question  "What's up?". This is a classic example of the Juji hybrid AI in action. The "0.9" equates to a 90% match proabaility, which can be ascertained by utilizing the advanced DL and ML technologies baked in to the Juji codesbase.

Line 11 demonstrates that our pattern language seamlessly handles foreign languages within the same rule.

Line 9, 13, 14 contains reference to topics that must be defined elsewhere
already, and pulled into the conversation from external sources.

## Automatic Dialog Management

In Juji's REP protocal, the dialog flow is managed automatically by the Juji system. The system
which takes care of both system initiated (proactive) and user initiated (reactive)
conversation turns. The conversation may jump around, but the bot always brings
the conversation back to the rules and topics as defined by the chatbot creator.
This unique combination of supported flow management and mission (or dialogue through-line)
focus is made easier by computational recognition of three key topic types.

## Topic Types

### Agenda Topics (User Generated)

These are often the user's chosen topics as constructed in the [Design View](../juji-studio/design). Once built they are lined up into anan agenda queue on the Juji engine's run-time system. Users can control and vary the order of, and trigger randomization within their agenda topics, as they see fit. The bot always attempts to prioritize the user's chosen agenda topics, and will only fundamentally diverge from the user's plan if the user consistently fails to follow the agenda topic path laid out by the chatbot creator.

### Ad-lib Topics (Small Talk)

If an agenda topic fails to produce a bot response, ad-lib topics can be triggered. Juji has many of these built in topics
that cover all kinds ofcontingencies, such as user digression, user misbehavior, missing information, courtesy fillers, troll responses, small talk and and so on. Users may write their own ad-lib topics, which can then added to the Juji database for use by others. Ad-lib topics are a critical bridge to completing an agenda, and once again, are built in.

### Exception Topics  (Fallbacks)

These are the last resort topics, known often as fallbacks, which handle cases where the bot through line breaks down and it cannot discern a pathway forward. But in order that the conversation may continue beyond system errors, REP scripting mistakes, and so on, these topics are created to engender teamwork with the user to fix the problem proactively, rather than delivering apologies. As with the Ad-Lib Topics above, Juji has already built an extensive list of these exception topics, but of course, users are encouraged to write their own to match their use cases more directly.

### Topic Categories

The function of a topic in any topic type above is not fixed. For example, an ad-lib topic may become an agenda topic if it is placed in the agenda topic queue in the `Config` form in the IDE. For more details on this flexibility check out [Config](reference.md#config).

## Other Features

In addition to topics and functions, REP language includes some convenient scripting
features, such as

[Variables](reference.md#variable),
[Named Patterns](reference.md#named-pattern),
[Name Spaces](reference.md#namespace).

To enable users to build interviews and surveys, REP has tailor-made scripting features for use cases involving questions (eg, job interviews) and surveys (GUI).

[Questions](reference.md#question)
[GUI](reference.md#gui).

Further features will be rolled out over time.
