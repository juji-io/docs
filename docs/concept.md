# Concepts of Juji Platform

Juji leverages the fruits of half century of artificial
intelligence (AI) research to build a practical and easy-to-use conversational
agent authoring platform. The core of the Juji platform is a hybrid AI system
that marries the so called "traditional AI" and the state of art deep learning
(DL) and machine learning (ML) technologies in natural language processing (NLP).

To meet industrial requirements that demand flexibility, accountability and
explainability of AI systems, Juji developed a declarative production rule
language to glue together the state of art NLP
capabilities. Called **REP** (Responsible Empathetic Persona), the language compiler
and run-time provide **automatic dialog management**, which alleviates most of the
burdens and pains associated with developing a conversational agent.

We now briefly go over the main concepts of REP language. Please refer to [Language
Reference](reference.md) for more details.

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

Line 1 declares the name of a new topic to be defined: `hello-world`.

Line 2 lists the parameters to the topic, if any. There is none here.

Line 3 is a trigger. You can think of it as a Boolean expression. Here it is empty,
meaning that it always returns true.

Line 4 is an action that the bot will take. Here it says "Hello world!"

### Rule

A pair of a trigger and an action is together called a rule. When the conditions
of the trigger are met and the action is taken by the bot, we say that the rule is fired.

### Followup Topic

When a rule is fired, its associated followup topics are primed, meaning that
these followup topics will be first considered in the bot's quest to come up
with something to say.

```clojure
(deftopic hello-world
  []
  []
  ["Hello world!"]
  (_ [hello]
     ["Nice to meet you!"]))

```
Line 5 starts an anonymous topic definition, for we are too lazy to come up with
a name so we use a `_` as the name, nor do we allow room for parameters. The line
ends with a trigger pattern. Basically, this pattern is matched if the word
"hello" is contained in the user's response to our "Hello world!".

Line 6 is the action, if triggered, the bot will say "Nice to meet you!"

Of course, we could be not so lazy and give the followup topic a proper
definition instead. Say, let's call it "greeting".

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

As you can imagine, there could be multiple rules in a topic. Each rule may be
associated with zero or multiple followup topics.

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
Line 4 is a trigger pattern that requires user input to contain any one of "hello",
"howdy" or "hi". For details of the many patterns REP supports, see [Rule Patterns](reference.md#rule-pattern)

Line 5 is an action that includes a system built-in function call that returns the user's
first name. In addition to producing text output, functions can do arbitrary
things.

Line 7 is a trigger that contains a built-in function call that checks whether
the user input is very similar to the sentence "what's up", i.e. the similarity
of user's response to the sentence has to be over 0.9. Obviously, this is an
instance where DL and ML technologies make a big play.

Line 11 shows that our pattern language handles foreign languages as well.

Line 9, 13, 14 contains reference to topics that must be defined elsewhere
already.

## Dialog Management

In REP, the dialog flow is managed automatically by the system. The system
properly handles both user initiated (reactive) and system initiated (proactive)
conversation turns. The conversation may jump around, but the bot always brings
the conversation back. This unique combination of flow flexibility and mission
focus is achieved with the help of categorizing topics into three types.

### Agenda Topic

These are often the topics you define in the [Design View](design.md). They
are placed in the agenda queue of the run-time system. You may also control the
ordering and its randomization. In general, the bot tries to ensure all the
agenda topics are covered, unless the user is stubbornly uncooperative.

### Ad-lib Topic

If an agenda topic fails to produce a bot response, ad-lib topics are tested.
They are mainly Juji's built-in topics that cover all kinds of
contingencies, such as user misbehavior, missing information, courtesy fillers,
and so on. You may write your own ad-lib topics.

### Exception Topic

These topics are tried last, and they handle cases where the bot has failed to
cope with a situation, so that the conversation may still go on. These include
system errors, REP scripting mistakes, and so on. These topics again normally are
written by Juji, but you can write your own as well.

Any topic can be treated as any topic category by being placed in one of the
three topic queues in the `config` form. Details description is in [Config](reference.md#config)

## Other Features

In addition to topics and functions, REP language includes some convenient scripting
features, such as [Variables](reference.md#variable), [Named
Patterns](reference.md#named-pattern), [Name Spaces](reference.md#namespace), and so on.

To facilitate the use cases of conducting interviews and surveys, REP has
special handling of
[Questions](reference.md#question) and [GUI](reference.md#gui).
