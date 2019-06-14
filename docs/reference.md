# REP Language Reference

The REP Language is the main glue for supporting various capabilities of the
Juji platform. Instead of boring you with BNF or other formal grammars, this
reference attempts to illustrate the language with examples and give some
intuition behind the design.

## Design Goal

The REP language deign has evolved slowly overtime, mainly driven by the use cases.
However, there are a few design goals that we strive to achieve.

Expressive
: As a domain specific language (DSL), REP itself is not designed to be general purpose. However, the complexity of the domain, human conversation, requires that the language to be expressive enough to easily specify a large percentage of normal conversations, and to make the rest possible.

Simple
: The concepts and constructs of the language should not involve too much
incidental complexity. The basis of the language is a rule engine. A small core set of orthogonal and consistent rules should cover the vast majority of cases. A simple language is easier to learn and helps with adoption.

Concise
: The code should be easy to write and read, without too much noise or boilerplate. Writing a chatbot should be a fun process, not a chore. In addition to programmers, the target audience includes the line of business people who are used to writing scripts for applications such as Excel, the hard core gamers who are used to doing game modifications, or the technology hobbyists who like to tinker.

Composible
: In order to support a graphic user interface layer on top of the DSL, the code
should be easily generated and manipulated by programs. Smaller components
should be readily composed together to form larger components. Components should
be reusable. The most composible solution is to use pure data, and we will take
this approach.

Extensible
: To enable the functionalities beyond rules, the system is designed to be easily extensible by directly embedding user defined functions in the script. The goal is to have a system framework where advanced technology components such as natural language processing, machine learning and others could be plugged into.

## Data Structure

REP reuses the [Clojure](https://clojure.org) data structure for base syntax. On
that syntactical basis, REP codifies some specialized semantic rules. A
reference to  Clojure data structures is at [this page](https://clojure.org/reference/data_structures).

Here we summarize the basic syntactic elements used in our language. Content
after `;` is comment. We use the following data types:

### Scalar Value

These are primitive values that can be composed into collections.

#### Boolean

These are the Boolean logic values.

```Clojure
true  ; true value
false ; false value
nil   ; equivalent to false in the context of logic expression
```
Any other non-nil value is also considered equivalent to `true` in the context
of logic expression.

#### Number

We parse a number literal into long or double number based on whether there’s a dot in it.

```Clojure
42 ; a long number
20.0 ; a double number
```
#### String
A string literal is enclosed by double quotation marks.
```Clojure
"a piece of text" ; a string
```
Some characters have special meanings, e.g. “;” is to start a comment and should be quoted as a string if it is to be used as a piece of text.

#### Keyword
Keywords are symbolic identifiers that evaluate to themselves. They starts with a `:`.
```Clojure
:something ; a keyword, the name of the keyword is "something"
```
Keywords cannot be assigned values and cannot be used as variable names, because they evaluate to themselves.

#### Symbol

When used inside a pair of parentheses, symbols are identifiers that are used to refer to something else. They often return the value bond to them when evaluated.

```Clojure
something ; something is a symbol
```
When used inside a pair of brackets, e.g. as part of a sequence pattern, the name of symbol will be used to represent a token.

```Clojure
[love] ; the name of symbol love is "love", and it is a pattern to be matched or displayed
```

### Collection

These are composite data structures. The following collection types are used in REP extensively.

#### Vector
Vector collection literal starts with `[` and ends with `]`. It contains an ordered collection of elements. Each element of the vector can be anything: scalar values or other collections.

```Clojure
;; a vector containing three elements: a double, a long, and ends with a string
[1.0 2 "a-string"]
;; another vector, containg three elements: a string, followed by
;; another vector, and ends with a symbol
["a-string" [:a 1] something]
```

#### Map
These are hashes that map keys to values. A map is enclosed by `{` and `}`.
The key value pairs inside a map are not ordered.

```Clojure
;; a map with two key value pairs, first maps a keyword to a boolean,
;; second maps a keyword to a number
{:a true :b 1}
;; another map, first maps a keyword to a vector, then a keyword to a string
{:b [:x 3] :c "a-string"}
```

#### List

Lists starts with `(` and ends with `)`. They are also ordered collections, but
they often represent executable code and
the first element of the list tells us what the execution is about, e.g. a
control flow construct, a function, or a declaration, and so on.

```Clojure
(if condition this that) ; the "if" conditional control structure
(defn my-fn [] "OK") ; a function definition, the function name is my-fn.
(my-fn) ; call the above function, it takes zero argument, and returns "OK"
(+ 1 2 3) ; another function call, the function name is "+", this call return 6
;; another function call, is the same as (get a-map :something),
;; will return the value mapped by the key :something in "a-map"
(:something a-map)
;; declaring a REP topic (see below), and this topic instructs the system
;; to say "OK" proactively
(deftopic my-topic [] []["OK"])
```

## Token

Like most natural language processing software, REP breaks up an utterance into
a sequence of words, called tokens. In languages such as English, punctuation
such as spaces, periods, colons, and so on are the natural boundary between
tokens. In REP, the punctuation marks that are not blanks are also regarded as
tokens.

For example, the string `"Hello, world!"` is converted into a sequence of
four tokens: `"Hello"`, `","`, `"world"`, `"!"`.

The only exception is `-`, which is not considered a token of its own.
For instance, `"twenty-five-year-old"` is a single token.

In REP, a token could be represented with a symbol, a string, or a regex.

### Symbol token

Symbol tokens are first converted to the lower case, then into the canonical
form (lemma) of their names, so different forms of the same word are treated as
the same token. For example, `bike`, `Bikes` and `BIKES` are the same token.

!!! note "Symbol containing / is not a token"
    Because `/` is a token of its own, a symbol containing a `/` will be treated
    as a name spaced REP language programming construct, instead of a token.

### String token

String tokens are not lemmatized, and they are only case *insensitive*. For
example, `"bike"`, and `"Bike"` are the same token.

### Regex token

For maximal specificity, a token can be specified by a regular expression
(regex). A tag `#token/regex` is used to designate a string as a regex.
The string has the same syntax as [Java's regex pattern](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) .
See [Regex tag](#tag-pattern) below for more details.

!!! note "Token Conversion Precedence"
    Strings, symbols, and regex can be freely mixed in a pattern, as expected.
    ```Clojure
    [I "used to" work in #token/regex "^IBM$"];
    ```
    However, when the same input word matches more than one type of tokens, a
    precedence is used to determine which type of token this input word is
    converted to:
    **string > symbol > regex**.
    ```Clojure
    ;; for an input word "IBM", the string "ibm" is actually matched
    [:1 IBM "ibm" #token/regex "IBM"]
    ```

## Rule Pattern

REP in its core is a rule language. The patterns of the rules are
the basic abstraction of REP. A rule pattern can be used to infer the meaning of
user’s input, or to specify the bot's actions. A pattern used in the
former case is called a **trigger pattern**, used in the later, called an **action
pattern**.

Trigger patterns are similar in concept to regular expressions, but the focus
here is on capturing natural language patterns. Therefore, they take tokens
instead of characters as the basic units of pattern matches.

There are many types of rule patterns.  The following are the basic types of
patterns that can be composed together to form a complex pattern.

### Sequence Pattern

The simplest type of pattern is an ordered sequence of tokens separated by spaces, represented as a vector of symbols. The name of the symbol suggests the string to be matched. For example:

```Clojure
;; will match user input "I love pizza", "i will love pizza",
;; "I don't love pizza", and "I LOVE PIZZA"
[I love pizza]
```
As we can see, the match is not case sensitive. For the sake of conciseness, a sequence pattern consists of tokens are matched quite liberally. It basically scans the input sequentially for matched tokens, ignoring tokens that do not match (essentially, allowing wildcard between tokens). For example,

```Clojure
[I have two bicycle] ; can match "I had two bicycles".
```

Used as action pattern, the sequence pattern will be output as strings separated
by spaces.

### String Pattern

If we only want to match the literal form of the text, without lemmatization or skipping, we should make the pattern a string:

```Clojure
;; will match "I love pizza" or "i love pizza",
;; but not "I loved pizza", "i will love pizza"
["I love pizza"]
```
Used in response, the string pattern will become part of the output as it is.

!!! note
    String pattern is case **insensitive**.

### Alternative Pattern

Another common type of pattern is to specify multiple alternatives that are
equivalent for the match. However, there are several cases of matching
behaviours for alternatives. For example, should we match zero or more of the
alternatives `:*`, zero or one of them `:?`, one or more of them `:+`, only one
`:1`, one to three of them `:1-3`, all of them `:a`, or anything but them `:!`?
We use a keyword to indicate the desired case:

```Clojure
; match zero or more of the four tokens, in any order
[:* pizza bacon sausage hamburger]
; match zero or one of the four tokens
[:? pizza bacon sausage hamburger]
; match one or more of the four tokens, in any order
[:+ pizza bacon sausage hamburger]
; all three tokens must appear, in any order
[:a pizza I love]
; none of the three tokens can appear
[:! pizza hamburger bacon]
; match one of the four alternatives
[:1 pizza bacon sausage hamburger]
; match two of the four alternatives
[:2 pizza bacon sausage hamburger]
; match two to three of the four alternatives
[:2-3 pizza bacon sausage hamburger]
; match at least two of the four alternatives
[:2- pizza bacon sausage hamburger]
; match any one token except the two listed
[:0 pizza hamburger]
```

The case indicator keyword has to be the first element of the vector. The orders among the rest of the elements are ignored, since they are alternatives.

```Clojure
;; will match "I love bacon", "Pizza is what I like", "I hate pizza but love tofu"
[:a I [:1 like love adore] [:1 pizza bacon]]
```

When used in action patterns, the system will randomly pick the alternatives using the
compatible semantics as matches. For example, `:1` will randomly pick one alternative as output; `:?` will pick one or zero alternative at random chance; and so on. The one exception is the `:0` case, as it does not make sense in actions. The choices are made at runtime.

### Wildcard Pattern

Sometimes we do not know the alternatives and wish to match any words, and wildcard patterns are needed for these cases. Similar to regular expressions, we have four wildcard symbols:

```Clojure
;; can match "I love mushroom topped pizza", "I love hot pizza", or "I love bacon"
[I love * [:1 pizza bacon]]
;; can match "I love hot pizza", or "I love thick pizza"
[I love . pizza]
;; can match "I love spicy noodle" or "I love noodle"
[I love ? noodle]
;; can match "I love spicy noodle" or "I love hot and spicy noodle"
[I love + noodle]
```

Symbol `*` can match any number of any words, including zero word.

For convenience, in a sequence pattern, such as `[I love pizza]`, system automatically insert `*` between the regular tokens (i.e. symbols or strings), so that the pattern is the same as `[I * love * pizza]`. However, for other cases, such as between a regular token and a vector pattern, or between two vector patterns, the explicit use of `*` is required if so desired. For example, the pattern `[[:1 where [which place] [what place]] you [:1 born located]]` will not match input “where are you located” due to the extra token `are`, but `[[:1 where [which place] [what place]] * you [:1 born located]]` will match.

Symbol `.` matches any one word, `?` matches zero or any one word, and `+`
matches any one or more words.

!!! note
    If the four wildcard literals, `*`, `.`, `?`, and `+`, need to appear as a part of text, one needs to double quote them as strings.

If we want to specify concrete numbers of wildcard words or a range of numbers, we need to be explicit:

```Clojure
[I love :2. pizza] ; match exactly two words between love and pizza

; require two tokens in front of I
[:2. I love pizza]
; this is an alternative pattern, match two tokens out of the three
[:2 I love pizza]

[I love :2-4. pizza]  ; match two to four words between love and pizza
[I love :2-. pizza]  ; match two or up to 5 more words between love and pizza

[I love :0. pizza] ; pizza needs to immediately follow love, no token between them
```

Wildcard patterns do not make sense in actions, and thus are not allowed there.

### Refinement Pattern

At occasions when we need to refine a given pattern to impose further
restrictions, two refinement patterns can be used. These patterns start with a
refinement keyword, either `:=` or `-`. The first part of the pattern following
the refinement keyword is the main pattern to be matched, and the rest are the
refinement.

In addition to match the first (main) pattern, requirement pattern `:=` requires
the subsequent patterns to match as well; Conversely, exclusion pattern `:-`
exclude the subsequent patterns from matching.

```Clojure
;; will match if there are two words between "love" and "pizza",
;; and they must contain "veggie" or "vegan"
[love [:= :2. [:1 veggie vegan]] pizza]
;; will match if there are two words between "love" and "pizza",
;; as long as they do not contain "veggie" or "vegan"
[love [:- :2. veggie vegan] pizza]
```

Refinement patterns are not allowed in actions.

### Start/End Pattern

We sometimes require a pattern to be at the start or the end of the sentence to match. As can be extrapolated from the above, keyword `:0`. placed at the beginning (meaning there should be no more token in front) or at the end (meaning there should be no more token behind) of a pattern can be used to signal these.

```Clojure
;; match only if there's no other token in front of "I", and no token after "pizza".
[:0. I love pizza :0.]
[:0. "Great"] ; "Great" should be the first word in order to match

; this :0. has no effect, because it is not at the head position, same as [I love [pizza]]
[I love [:0. pizza]]

; this :0. requires I, if present, to be the first token
[:1 We [:0. I]]
; this :0. requires pizza, if present, to be the last token
[I love [:1 [pizza :0.] bacon]]

; this :0. requires either I or We to be the first token
[:0. [:1 We I] love pizza]

; this :0. requires either pizza or bacon to be the last token
[I love [:1 pizza bacon] :0.]
; this :0. is misplaced, only bacon will be the last token
[I love [:1 pizza bacon :0.]]
```

### Tag Pattern

For certain syntactic or semantic class of content, some pre-defined tags can also be used to annotate a pattern, requiring its content to fit the class. Tags are prefixed with `#`, and are placed in front of the pattern to be annotated.

```Clojure
;; For an input "The dog says he dogs the tree",
;; #pos/verb requires "dog" to be tagged as a verb for it to match
;; the first dog should not match, whereas the second should
[#pos/verb dog]
```
Most tags are backed by ML based NLP modules.

#### Parts of Speech tag

 Tag | Description | Examples
---|---|---
#pos/noun |Noun | desk, books, water
#pos/verb |Verb | go, enjoy, love
#pos/adj  |Adjective | superior, one-of-a-kind, the most
#pos/adv  |Adverb  | very, later, lovely
#pos/pronoun |Pronoun | she, her, you
#pos/preposition |Preposition | on, for, after
#pos/to |to |to
#pos/particle |Particle | so, up, let
#pos/number |Number token | two, third
#pos/ext-there |Existential theres | there
#pos/modal | Verbs don't take s ending in 3rd person | can, may, must
#pos/determiner | Determiner | a, no, the, any, each, that
#pos/conjunction | Conjunction | and, but, nor, or, plus, minus
#pos/interjection | Interjection | my, oh, please, see, uh, well, yes

#### Phrases tag

 Tag | Description | Examples
---|---|---
#phrase/NP | Noun phrase | the police officer's dog, a yellow house
#phrase/VP | Verb phrase | was walking, must go, let the fresh air in
#phrase/PP | Preposition phrase | in the storefront window, by the river
#phrase/ADJP | Adjective phrase | smarter than me, extremely delighted
#phrase/ADVP | Adverb phrase | in total silence, quite easily
#phrase/sub | subordinate clause | that, because, while
#phrase/other | not part of any chunk |

#### Entity tag
 Tag | Description | Examples
---|---|---
#entity/person  | person name | John, Mary
#entity/org | organization name | UN, IBM
#entity/location | location name | Canada, Main St.
#entity/time | time | tomorrow, around 10:30
#entity/duration | duration | 5 years, 3 hours

#### Regex tag

When a pattern requires sub-token variations, we can use character based regular
expressions. A regular expression is represented as a
string with a tag `#token/regex` in front. The syntax of the string follows
Java's regular expression.

```Clojure
;; match a token consists of one or more digits.
;; Note the double backsladh
#token/regex "\\d+"
;; match "favorite", "fav", "favarable", etc.
#token/regex "fav*"
```

!!! warning
    In REP, the regex tag pattern is restricted to represent a single token only. A regex representing multiple tokens will never match since the input to the pattern is always a single token.

When a token’s case-sensitivity is important, e.g. when matching acronyms, regex tag can be useful.

```Clojure
#token/regex "IBM" ; match "IBM" or "IBMer", but not "ibm"
#token/regex "^IBM$" ; match "IBM" only
```

Tag patterns are not allowed in actions.


### Class Pattern

With the exception of regex tag, the same set of tags
indicated above can be specified using namespaced keywords, which represent
placeholders for the specified class of content. For example,

```Clojure
;; :pos/verb matches a token whose parts of speech tag is a verb, e.g. "love", "hate", etc.
[he :pos/verb her]
```

Essentially, Class Pattern can be thought of as shorthand for a special case of Tag Pattern, where the tagged content are Wildcard Patterns.

```Clojure
;; These two are the same
[#pos/verb +]
[:pos/verb]
```

### Callable Pattern

Patterns can contain lists representing things that can be called to produce results. We evaluate lists recursively using Clojure’s `eval` after `macroexpand-all`.

There are two types of callable in REP.

#### Clojure Built-in Form

In order to support proper logic branching behavior in action patterns, we implemented special forms `let` and `if` ourselves to match Clojure’s semantics. This enables us to also support most of the Clojure’s branching macros: `and`, `or`, `when`, `when-not`, `when-let`, `if-not`, `if-let`, `cond`, `condp`. The only exception is `when-first` due to the way it was implemented in Clojure.


#### Function Call

Two types of function call can be included in the patterns.

##### Pattern Function

Functions with names starting with `_` allow the generation of dynamic patterns at runtime. Such function calls can appear anywhere in place of a token, as long as they return an appropriate data structure for a pattern. This applies to both trigger and action patterns.

```Clojure
;; result of function call (_query-favirate-food) is now part of the match pattern
[I love (_query-favirate-food)]
;; for example, if it returns [hot pizza], the pattern becomes
[I love [hot pizza]]
```

!!! note
    Because function calls are executed during live chat, the calls should not take too long to complete if a good response time is desired.

##### Regular Function

Regular functions do not generate patterns, but can be used for two purposes:

1. Producing side effects, such as displaying a visualization, processing user
actions, querying database, and so on;

2. Serving as an additional condition for the trigger pattern. That is to say, if
   the function return value is `false` or `nil`, the whole match fails. In
   other words, there’s an implicit `and` logic relation among the functions
   within a  trigger pattern.

What about `or`? Well, all rules are implicitly `or`ed together in a topic (see below).

!!! info
    One can still explicitly use Clojure logic forms such as `and`, `or`, `not` within the patterns.

Juji platform provide a set of built-in functions, see [System Functions](function.md) for details.

!!! note
    Juji system functions have special calling conventions:
    1. No namespace is necessary.
    2. The first argument should be omitted, for it refers to the chatbot itself.

To define a function, the `defn` form of Clojure can be used in the script. The
defined function resides in the namespace of the script (see below).


## Pattern Construct

In addition to plain compositions of rule patterns, we introduce some important constructs that are useful for writing more sophisticated scripts.

### Named Pattern

Often we want to reuse a pattern in different places, so we want to assign the
pattern a name to refer to it. Such named pattern is indicated by a symbol
starting with `_`.

The visibility of the name pattern depends on where it is defined. If the assignments are done with a top level `named-pattern` form, the named patterns defined therein are globally accessible. If defined inside a topic (see below), it is visible only within that topic.

```Clojure
(named-pattern ; bindings of named patterns are defined inside a vector
  [_negative    [:1 no not don't doesn't isn't ain't]
   _food        [:+ tofu pizza rice]
   _time-of-day [:1 morning afternoon evening]
   _greeting    [good _time-of-day]
   _hi          [Hi, (user-first-name)]])
```

The bindings of named patterns happen in the order they appear, so later
bindings can refer to previous named patterns. Topic specific named patterns can
refer to global named patterns. Topic specific named patterns can also override
the global named patterns with the same name.

!!! info
    We encourage the use of named patterns as they promote code reuse and lead to better organized and more readable scripts.

The substitution of a pattern name by the actual pattern it refers to happens at compile time. Named patterns can contain function calls (see below), but not captured content (see below).

```Clojure
[I _negative love pizza] ; match "I don't love pizza"
```

### Captured Content

We often want to name the content matched by a pattern. A form looks like `(?captured-content-name pattern)` can be used to do that, where a symbol starting with `?` will be assigned the content matched by the pattern.

```Clojure
;; capture any possible words between love and pizza
[I love (?kind *) pizza]
;; capture one of "thin" or "thick"
[I love (?kind [:1 thin thick]) pizza]
```

The captured content can then be referred to later by its name symbol, for example, `?kind`. The reference to captured content is visible within the containing rule, including the remaining parts of the trigger pattern, action pattern and anonymous followup topics.

```Clojure
;; The captured content ?food is passed into two functions:
;; foreign-food? and hot-food?
;; If the results of either of the two calls is false, the match fails
[I love ?food (foreign-food? ?food) (hot-food? ?food)]

;; the ?number must greater than 10 but smaller than 100
[I have ?number books (> ?number 10) (< ?number 100)]
;; same as above, only longer
[I have ?number books (and (>= ?number 10) (< ?number 100))]
;; this is actually the best, short and sweet, isn't S-expression great?
[I have ?number books (> 100 ?number 10)]
```

!!! info "Capturing Shorthand"
    For the most common case of capturing the `+` wildcard pattern, i.e. capturing any one or more tokens, we can use a shorthand, just `?captured-content-name` itself.

    ```Clojure
    ;; the following two are equivalent
    [I love ?kind pizza]
    [I love (?kind +) pizza]
    ```

Capturing content is not allowed in actions, but referring to the captured
content in action patterns is its intended use, where we gather user input.

A useful use case for class pattern is to combine it with capturing:

```Clojure
;; Capture what's after [I am] pattern and
;; only match if the captured is a adjective type part-of-speech
[I am (?sth :pos/adj)]
[?sth]
```

!!! note "?-starting Symbol Resolution Precedence"
    The resolution of a symbol started with `?` uses the following search precedence: First check if it is an argument of the containing topic, then check if it is a reference to captured content, followed by a check on whether it is inherited from parent topics if this is part of an anonymous followup topic (see below), if all above fails, it will then be treated as a shorthand for capturing `+`.

## Topic

In the [Conceptual Overview](concept.md), we have seen that topics are the
building blocks of REP script.

### Define and Use

The declaration of a topic is represented by a
list, with `deftopic ` as the first element, then a symbol as the name of the
topic, followed by a vector of parameters. A topic may take zero or more
parameters, e.g. useful for passing contextual values to followup topics. Each
parameter is represented by a symbol starting with `?`.

The body of the topic consists of an optional map and a number of rules. A rule
is a pair of a trigger and an action, optionally followed by zero or multiple
followup topic invocations. Schematically, the structure of a topic definition
is illustrated by the following example:

```Clojure
(deftopic a-topic [?para-1 ?para-2]
  {:option-key-1 option-value-1} ; option map, can omit when empty

  ;; rule-1 starts
  [trigger-1]
  [action-1]
  (followup-topic1-1 ?para-1)
  (followup-topic1-2 :something)
  ;; ... more followup topics
  ;; rule-1 ends

  ;; rule-2 starts
  [trigger-2]
  [action-2]
  (followup-topic2-1 ?para2)
  ;;... more followup topics
  ;; rule-2 ends

  ;;...more rules
  )
```

Followup topics `followup-topic1-1`, `followup-topic1-2`, and
`followup-topic2-1` must all be defined elsewhere already. Each of them happens
to take a single parameter.

As you can see, the invocation of a topic is simply represented by a list, with
the first element being the name of the topic, followed by a number of parameter
values that match the topic definition. For example, an invocation of the topic
`a-topic` defined above could look like this `(a-topic 2 5)`, where the
parameter `?para-1` is bound to value `2` and `?para-2` to value `5`.

### Rule

A topic can be seen as essentially a collection of rules. To generate a
response, rules in a topic are tried in the order that they are written.

Two types of rules can be defined, the simple rule and the branched rule.

#### Simple Rule

We have seen a few examples of simple rules, which consist of a trigger pattern, an
action pattern, and optionally a number of followup topic invocations.

```Clojure
[I love pizza]
"Me too, what's your favirate topping?" ; action here is a string
(topping)
```
The pair of trigger and action represents one turn of conversation. When user input
matches the trigger pattern, the corresponding action will be taken. If a rule
successfully generated a response, its attached followup topics will be tried
first for the next turn. In this example, the follow up turns of conversation
might be on the topic of pizza topping.

!!! note
    If a simple rule’s trigger pattern is `[]`, it means that this rule is a
    proactive rule and will fire regardless when the rule is tested.

#### Branched Rule

Branched rules allow further refinement for a trigger pattern, which will be
refined into a tree of more trigger patterns, with corresponding actions and followup topics. That is to say, instead of a single action, a trigger will be paired with a list of sub-rules, each can be a rule of its own. The list can optionally end with a default action (optionally with a list of followup topics), which will be returned when all the sub-rules fail to trigger.

```Clojure
[I [:1 love like] pizza]
([love]
 "Wow, I am a pizza head too"
 (pizza-head)

 [like]
 "Same here, I also like hot dog"

 "Cool")
```
Line 1 is the top/root trigger of the branched rule, if triggered, the branches
below will be tested.

Line 2 and 6 are two branch triggers. Only one of them can be triggered. Or none
of them matches. In that case, the default action in Line 9 will be generated as output.

Sub-rules inherit the captured content of the ancestor matches, allowing a path of matches to capture multiple pieces of information necessary for a complex action.

```Clojure
;; root match
[I [:1 love like] ?thing]
;; followed by a list of sub-rules

;; the first sub-rule
([love]
 ;; nested sub-rules
 ([(= ?thing ["pizza"])]
  "Wow, I am a pizza head too"
  (ask-for-more)

  [(= ?thing ["tofu"])]
  "Me too, I also love tofu"
  (_ [really] [Of course ?thing is my favirate]
     [no] "It's true")

  ;; default response for "[love]" sub-rule match
  "Loving something is great"
  (ask-for-more))

 ;; the second sub-rule
 [like]
 [Same here, I also like ?thing]
 (ask-for-more)

 ;; the default response for root match
 "Cool"
 (ask-for-more))
```
As can be seen, branched rules can be nested arbitrarily in depth. It can be
seen as a decision tree that provides many decision points before a single action is chosen.

### Option Map

A topic may optionally include an option map to control its behavior.  The options
take default values if not specified in the option map. These are the options:

```Clojure
{;; This topic will first segment input into sentences, then each rule will be
 ;; tried on each sentence.
 ;; If any sentence matched the rule, the input is considered a match
 ;; default is false.
 ;; When used in a branch rule, when matched, all sentences in the input will be
 ;; considered by the next level rule
 :segment-sentence? true

 ;; these local named patterns can be used inside this topic
 :named-pattern [_negative [:1 not don't doesn't]
                 _food [:+ tofu pizza pork]]

 ;; Specify a pre-condition for the topic, its value is a match pattern. If
 ;; present, the topic will be tried if the match pattern return true
 :pre-condition [hello]

 ;; some function calls before the rules are tried, useful for initialization
 :pre-action [(<- init-var 0)]

 ;; some function calls after the rules are tried, useful for cleanup
 :post-action [(cleanup-1) (cleanup-2)]

 ;; These rules are only tried after neither the topic's main rule set nor the ad-lib
 ;; topics fire; it may also have an option map with :include-before and :include-after
 :default-rules ({:include-before [(my-default)]}
                 [(> (input-length) 3)]
                 [:1 "Thank you for the input" "Got it, thank you"]

                 [thank]
                 "You are welcome.")

 ;; This response will be generated if the following fail to generate a
 ;; response: main rule set of the topic, ad-lib topics and default rules of the topic
 ;; failed-reponse does not consume user input.
 :failed-response ["ok"]

 ;; Include other topics as part of this topic, as if rules in the included
 ;; topics are copied into this topic. This is how topics compose in REP.
 ;; These topic invocations will be tried before rules of this topic is tried.
 :include-before [(common-topic-a ?q) (common-topic-b)]

 ;; These topic invocations will be tried after rules of this topic is tried.
 :include-after [(common-topic-c) (common-topic-d)]

 ;; a map containing some meta information about the topic, key-value could be
 ;; anything user defined
 :note {:some-key some-value :other-key :other-value}}
```

### Topic Composition

Together with `:default-rules`, a topic may be thought
of as a composition of two sets of rules that are tried in order, with an
intermission of ad-lib topics:

* rules in the main body of the topic
* rules in `:default-rules`, which only apply after none of the above fires and
none of the ad-lib topics fires.

Both sets of rules may include rules of other topics. `:include-before` and
`:include-after` options enable the rules of a topic to become parts of another
topic, allowing topics to become composible. Rules in the topics of
`:include-before` are tried before the main body of rules, `:include-after` are
tried after the main body of rules.

Taken together, the order of trying rules of a topic is the following:

1. include-before of the topic
2. main body of the topic
3. include-after of the topic
4. ad-lib topics
5. include-before of the default rules
6. main body of the default rules
7. include-after of the default rules

Sometimes it is necessary to use the set of rules in the main body only. These
rules can be referred to with a special topic name, an earmuff enclosed
topic name and a `-main` suffix. For example, for a topic named
`my.ns/handle-favorite-things`, the system automatically creates a corresponding
`my.ns/*handle-favorite-things-main*` topic to refer to the rules in the main body of
the topic. Similarly, `my.ns/*handle-favorite-things-default*` refers to the set
of rules in the default-rules of the topic.

### Topic Recursion

Since the followup topics of a topic can contain any topic, including the parent
topic itself, REP supports arbitrary recursion among topics. This mechanism can
be used for repeating, looping and any other purposes that require to go back
to a prior topic.

In addition to using the topic name as the recursion target, REP provides a
special followup topic, `(*recur*)`, which always recurs back to the
current topic. This is specially useful when a topic is included in another
topic, so that the followup topic of the included topic can
go back to the including topic, which is usually the intended behavior.

### Anonymous Topic

 Any named topic can be a followup topic of another topic. However, sometimes we
 do not want to come up with names for some one-shot followup topics. In these
 cases, we can define anonymous followup topic and use it in place.

```Clojure
[I love pizza]
"Me too, what's your favourite topping?"
(_ [:+ mushroom veggie]
   "Cool, it's healthy"
   (healthy-food)

   [:+ beef pepperoni]
   "Wow, I like meat, yummy!"
   (meat-food))
```
 Anonymous followup topics use `_` as the topic name,  they do not take parameters and do not have their own option maps. Instead they inherit the parameters and option map of the ancestor topics, as well as the captured contents of the ancestor rules.

## Variable

Variables are symbols that can be used to track information or store results during system run. Variables are scoped within a running REP instance and are available only during the run-time.

!!! note
    Syntactically, variables should always appear inside a pair of parentheses.

### Local Variable

Sometimes it is necessary to track some information local to a topic. Local
variables can be set using function `(set-var name value)`, where name could be
any symbol and value any Clojure data. This function always returns `nil`, so it
should only be used in actions. `<-` is a shorthand function name.

In trigger patterns, use `(set-var-ret name value)` instead, because it returns
the value itself and will not short-circuit the match. Shorthanded name for this
function  is `-<-`.

Local variables of a topic are inherited by its followup topics. The local variable of a followup topic takes precedence over that of the parent topic with the same name.

### Global Variables

It is often useful to use some global variables to track conversational state that span across multiple conversation topics. We can set a global variable value with `(set-global-var name value)` or `(set-global-var-ret name value)` system function calls, and their short-hands are `<-|` and `-<-|` respectively. Global variables are accessible by all topics and live until the end of the conversation.

Local variable has precedence over global variable when the two names collide.

## Namespace

REP reuses [Clojure namespace](https://clojure.org/reference/namespaces)
constructs. Each script has a unique namespace, and may require other namespaces.

```Clojure
(ns juji.eng1.ava
  (:require [my.other :as other]
            [juji.questions :as jq]))
```
Symbol with a prefix in front of `/` is considered as namespaced, e.g.
`abc/xyz`, where `abc` is the namespace prefix. Namespaced symbols can be used
to refer to things defined in other namespaces,

```Clojure
[other/_greetings]
[(ask-question jq/what-q)]
```

Clojure core functions or macros of Clojure, such as `>=`, `and`, `or`,`if`, as
well as Juji system functions can be called without namespace prefix.

## Question

In order to support conducting surveys and have good results reporting, REP treat questions specially. Questions need to be defined before being asked in the topics. Similar to named patterns, a top level `(question ...)` form is used to define named questions with a binding form.

```Clojure
(question [likert1-5    [{:value 1 :text "Strongly disagree"}
                         {:value 2 :text "Slightly disagree"}
                         {:value 3 :text "Neutral"}
                         {:value 4 :text "Slightly agree"}
                         {:value 5 :text "Strongly agree"}]
           yes-no       [{:value 1 :text "Yes"}
                         {:value 0 :text "No"}]
           apple-q      {:kind    :single-choice
                         :heading "I own an apple product"
                         :choices yes-no}
           pizza-q      {:kind    :single-choice
                         :heading "I love pizza"
                         :choices likert1-5}
           election-q    {:kind   :single-choice
                          :heading "Who did you vote for?"
                          :choices [{:value 0 :text "Trump"}
                                    {:value 1 :text "Clinton"}
                                    {:value 2 :text "Johnson"}
                                    {:value 3 :text "Stein"}]}
           what-q       {:kind :open-ended
                         :heading "What color do you like?"
                         :wording "Could you please tell me the color you like?"}
           why-q        {:kind    :open-ended
                         :heading "Why do you like that color?"
                         :wording "May I ask you why you like that color?"}])
```
Some types of questions are normally presented in a GUI form. `:single-choice`
questions are radio buttons; `:multiple-choice` questions are check boxes.

The value of `:choices` attribute may be given a name, defined before hand, so that they are reusable, e.g. `likert1-5` and `yes-on`, or it could be included inline, e.g. the choices in `election-q`.

`:open-ended` question are normally presented as sentences in a conversational turn. They may optionally have a `:wording` attribute that is an action pattern.


Questions, once defined, can be used in special functions to be displayed to the
users. `:open-ended` questions are displayed using function `(ask-question
question-name)`. `:single-choice` and `:multiple-choice` questions are displayed with `(ask-qui-question question-name)` function.

To record user’s answer, use function `(record-answer question-name content)`, where content should be a captured content of user input or user choices.


## GUI

REP can present information and accept user input via GUI displays. Displays are specified in a top level form `gui`, which binds some GUI elements to the corresponding symbols.

```Clojure
(gui [fun-form     {:type        :form
                    :instruction "Please fill out the form"
                    :questions   [{:kind :single-choice
                                   :heading  "I love pizza"
                                   :choices  likert1-5}
                                  apple-q]}])
```
System function `(display-gui display)` can be called to display a GUI element. Normally this should happen on the action pattern of some rules.

## Config

REP is designed as a declarative language. Developers do not control the
execution flow directly, as the conversation may progress in a non-deterministic
fashion due to user's responses. Developers only write down the rules, and code
execution is handled by the system.

Users can influence the system behaviours by specifying some control directives.
In addition to topic specific directives in option map, some global directives for the bot can be declared in a global map called `config`.

```Clojure
(config {
  :release-action []
  :pre-action []
  :post-action []
  :agenda [start-topic [:a (topic-1 "arg1") topic-2 (topic-3 "arg3")] end-topic]
  :exception [error-topic1 error-topic2]
  :ad-lib [ad-lib1 ad-lib2]
  :background [notify-topic1]
  :session-duration-max 30 ; in minutes
  :min-response-time 2000 ; after user hit Enter key, the minimal system wait time before responding, in milliseconds
  :between-response-delay ; when REP have multiple sentences to say in one turn, the deblay between the sentences
  :turn-pace 5 ; when there is no user input, the interval between system's proactive attempts to say something, in seconds
  :typing-allowance 10 ; when user is typing, how long the system allows the user to pause before trying to respond to previous user input, in seconds })
```
`:release-action` allows a vector of function calls to run
 right after compilation, so some setup for the release can be done, e.g.
 to prepare some read-only data resources.

`:pre-action` allows a vector of function calls to run before a chat session begins.
This allows some session specific setup, e.g. to initialize some global variables.

`:post-action` allows a vector of function calls after a chat session ends.

`:agenda` vector specifies desired conversation progression in term of topics. It uses a similar format as that of action patterns, only that the basic unit is topic invocation instead of tokens. It supports sequence pattern, alternative pattern, wildcard pattern, exclusion pattern, start and end pattern. Also, parameters for top level topics are given here.

REP may also use some topics as conversational fillers, e.g. to initiate small
talks unrelated to the agenda, or to quickly dispatch user digression. These
topics are declared in `:ad-lib` vector.

REP may also actively check some topics in the background, where some external conditions are the
triggers. When the conditions are met, the REP may notify the users about the
external events. These topics are in `:background` vector.

User may also give unexpected input to REP. These exceptional user input are
handled by topics declared in `:exception` vector.

The declaration of `:agenda`, `:ad-lib`, `background` and `:exception` uses the same format.
