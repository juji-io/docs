# REP Language Reference

The REP Language is the main glue for various capabilities of Juji platform.

## Design Goal

The language deign has evolved slowly overtime, mainly driven by the use cases.
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

REP reuses the Clojure data structure for base syntax. On that syntactical
basis, REP codifies some specialized semantic rules. A reference to Clojure data
structures is at [this page](https://clojure.org/reference/data_structures).

Here we summarize the basic syntactic elements used in our language. Content
after `;` is comment. We use the following data types:

### Scalar Value

These are primitive values that can be composed into collections.

#### Boolean

```Clojure
true ; true value
false ; false value
```
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

## Rule Pattern

The basis of REP is a rule language. The patterns of the rules are
the basic abstraction of REP. A rule pattern can be used to infer the meaning of
user’s input, or to specify the bot's actions. A pattern used in the
former case is called a **trigger pattern**, used in the later, called an **action
pattern**.

Trigger patterns are similar in concept to regular expressions, but the focus
here is on capturing natural language patterns. Therefore, they take words
(called tokens) instead of characters as the basic units of pattern matches.

There are many types of rule patterns.  The following are the basic types of
patterns that can be composed together to form a complex pattern.

### Sequence Pattern

The simplest type of pattern is an ordered sequence of tokens separated by spaces, represented as a vector of symbols. The name of the symbol suggests the string to be matched. For example:

```Clojure
;; will match user input "I love pizza", "i will love pizza",
;; "I don't love pizza", and "I LOVE PIZZA"
[I love pizza]
```
As we can see, the match is not case sensitive. For the sake of conciseness, a sequence pattern consists of symbols are matched quite liberally. It basically scans the input sequentially for matched tokens, ignoring tokens that do not match (essentially, allowing wildcard between tokens). In addition, each symbol is converted to the canonical form (lemma) of its name, so different forms of the same word are treated as the same. For example,

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
    String pattern is case insensitive.

### Regex Pattern

When a pattern requires sub-token variations, we can use regular
expressions, which are character based. A regular expression is represented as a
string with a `#` in front. The syntax follows Clojure's.

```Clojure
#"\d+"  ; match a token consists of one or more digits.
#"fav*" ; match "favorite", "fav", "favarable", etc.
```

!!! warning
    In REP, the regex pattern is restricted to represent a single token only. A regex representing multiple tokens will never match since the input to the regex is always a single token.

Similar to string pattern, when a token’s case-sensitivity is important, e.g. when matching acronyms, regex patterns can be useful.

```Clojure
#"IBM" ; match "IBM" or "IBMer", but not "ibm"
#"^IBM$" ; match "IBM" only
```

Regex patterns are not allowed in actions.

### Alternative Pattern

Another common type of pattern is to specify multiple alternatives that are
equivalent for the match. However, there are several cases of matching
behaviours for alternatives. For example, should we match zero or more of the alternatives, zero or one of them, one or more of them, only one, all of them or anything but them? We can use a keyword to indicate the desired case:

```Clojure
; match zero or more of the four tokens, in any order
[:* pizza bacon sausage hamburger]
; match zero or one of the four tokens
[:? pizza bacon sausage hamburger]
; match one or more of the four tokens, in any order
[:+ pizza bacon sausage hamburger]
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
; match all three tokens in any order
[:a pizza I love]
```

The case indicator keyword has to be the first element of the vector. The orders among the rest of the elements are ignored, since they are alternatives.

```Clojure
;; will match "I love bacon", "Pizza is what I like", "I hate pizza but love tofu"
[:a I [:1 like love adore] [:1 pizza bacon]]
```

When used in action patterns, the system will randomly pick the alternatives using the
compatible semantics as matches. For example, `:1` will randomly pick one alternative as output; `:?` will pick one or zero alternative at random chance; and so on. The one exception is the `:0` case, as it does not make sense in actions. The choices are made at runtime.

!!! note "Token Conversion Precedence"
    Strings, symbols, and regex can be freely mixed in a pattern, as expected.
    ```Clojure
    [I "used to" work in #"^IBM$"];
    ```
    However, when the same input word matches more than one type of tokens, a
    precedence is used to determine which type of token this input word is
    converted to:
    **string > symbol > regex**.
    ```Clojure
    ;; for an input word "IBM", the string "ibm" is actually matched
    [:1 IBM "ibm" #"IBM"]
    ```

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

### Exclusion Pattern

At occasions when we need to exclude some special cases from a given pattern, the exclusion can be made by a preceding - symbol before the excluded pattern.

```Clojure
;; will match two words between "love" and "pizza", as long as they do not contain "veggie" or "vegan"
[I love [:2. -[* [:1 veggie vegan] *] pizza]
```

A sub-pattern (as delimited by a pair of `[` and `]`) may contain at most one
exclusion, and the exclusion must be the last element of the vector.

!!! note
    The excluded pattern should indicate special cases of the main pattern, otherwise the results are not well defined.

Exclusions are not allowed in actions.

### Tag Pattern

For certain syntactic or semantic class of content, some pre-defined tags can also be used to annotate a pattern, requiring its content to fit the class. Tags are prefixed with `#`, and are placed in front of the pattern to be annotated.

```Clojure
;; For an input "The dog says he dogs the tree",
;; #pos/verb requires "dog" to be tagged as a verb for it to match
;; the first dog should not match, whereas the second should
[#pos/verb dog]
```
These tags are backed by machine learning based natural language processing modules, e.g. parts of speech tagging.

### Class Pattern

The placeholders for the same set of classes indicated above can be specified using namespaced keywords. For example,

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

!!! info "Capturing Shorthand"
    For the most common case of capturing the `+` wildcard pattern, i.e. capturing any one or more tokens, we can use a shorthand, just `?captured-content-name` itself.

    ```Clojure
    ;; the following two are equivalent
    [I love ?kind pizza]
    [I love (?kind +) pizza]
    ```

Capturing content is not allowed in actions, but referring to the captured
content in action patterns is its intended use, where we gather user input.

Another example, a useful use case for class pattern is to combine it with capturing:

```Clojure
;; Capture what's after [I am] pattern and
;; only match if the captured is a adjective type part-of-speech
[I am (?sth :pos/adj)]
[?sth]
```

!!! note "?-starting Symbol Resolution Precedence"
    The resolution of a symbol started with `?` uses the following search precedence: First check if it is an argument of the containing topic, then check if it is a reference to captured content, followed by a check on whether it is inherited from parent topics if this is part of an anonymous followup topic (see below), if all above fails, it will then be treated as a shorthand for capturing `+`.

### Callable

Lists represent things that can be called to produce results. We evaluate lists
recursively using Clojure’s `eval` after `macroexpand-all`.

There are two types of callable in REP.

#### Clojure Built-in Form

In order to support proper logic branching behavior, we implemented special forms `let` and `if` ourselves to match Clojure’s semantics. This enables us to also support most of the Clojure’s branching macros: `and`, `or`, `when`, `when-not`, `when-let`, `if-not`, `if-let`, `cond`, `condp`. The only exception is `when-first` due to the way it was implemented in Clojure.


#### Function Call

Two types of functions can be included in the patterns. Functions with names starting with _ allow the generation of dynamic patterns at runtime. Such function calls can appear anywhere in place of a token, as long as they return an appropriate data structure for a pattern. This applies to both match and response patterns.

;; result of function call (_query-favirate-food) is now part of the match pattern
[I love (_query-favirate-food)]
;; for example, if it returns [hot pizza], the pattern becomes
[I love [hot pizza]]

Regular functions do not generate patterns, but can be used for two purposes: a. Producing side effects, such as displaying a visualization, processing user actions, querying database, and so on; b. Serving as an additional condition for the match pattern. That is to say, if the function return value is false, the match fails. In other words, there’s an implicit and logic relation among the functions within a match pattern. What about or? Well, all production rules are implicitly ored together in a topic (see below). Of course, one can still explicitly use Clojure logic forms such as and, or, not within the match patterns.

;; The captured content ?food is passed into two functions: foreign-food? and hot-food?
;; If the results of either of the two calls is false, the match fails
[I love ?food (foreign-food? ?food) (hot-food? ?food)]
;; the ?number must greater than 10 but smaller than 100
[I have ?number books (> ?number 10) (< ?number 100)]
;; same as above, only longer
[I have ?number books (and (>= ?number 10) (< ?number 100))]
;; this is actually the best, short and sweet, isn't S-expression great?
[I have ?number books (> 100 ?number 10)]

Because function calls happen at runtime, when pattern matching is performed on user input, the call should not take too long to complete in order to obtain a good response time.

To define a function, the defn form in Clojure can be used in the script. The defined function resides in the namespace of the script (see below). Calling these user defined functions in the script do not require namespace prefix. Core functions or macros of Clojure, such as >=, and, or,if, as well as REP system functions can also be called without namespace prefix.


## Topic

In the [Conceptual Overview](concept.md), we have seen that topics are the
building blocks of REP script.

### Declaration

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

### Invocation

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

We have seen a few examples of simple rules, which consist of a trigger, an
action, and optionally a number of followup topic invocations.

```Clojure
[I love pizza]
"Me too, what's your favirate topping?" ; action here is a string
(topping)
```
The trigger and action represent one turn of conversation. When user input
matches the trigger, the corresponding action will be taken. If a rule
successfully generated a response, its attached followup topics will be tried
first for the next turn. In this example, the follow up turns of conversation
might be on the topic of pizza topping.

If a simple rule’s trigger pattern is `[]`, it means that this rule is a
proactive rule and will fire regardless when tried.

#### Branched Rule

Branched rules allow further refinement for a rule trigger, which will be refined into a tree of further triggers, with corresponding actions and followup topics. That is to say, instead of a single action, a trigger will be paired with a list of sub-rules, each can be a rule of its own. The list can optionally end with a default action (optionally with a list of followup topics), which will be returned when all the sub-rules fail to trigger.

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
