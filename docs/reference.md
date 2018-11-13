# REP Language Reference

The REP Language is the main glue for various capabilities of Juji platform.

## Design Goals

The language deign has evolved slowly overtime, mainly driven by the use cases.
However, there are a few design goals that we strive to achieve.

### Expressive

As a domain specific language (DSL), REP itself is not designed to be general purpose. However, the complexity of the domain, human conversation, requires that the language to be expressive enough to easily specify a large percentage of normal conversations, and to make the rest possible.

### Simple

The concepts and constructs of the language should not involve too much
incidental complexity. The basis of the language is a rule engine. A small core set of orthogonal and consistent rules should cover the vast majority of cases. A simple language is easier to learn and helps with adoption.

### Concise

The code should be easy to write and read, without too much noise or boilerplate. Writing a chatbot should be a fun process, not a chore. In addition to programmers, the target audience includes the line of business people who are used to writing scripts for applications such as Excel, the hard core gamers who are used to doing game modifications, or the technology hobbyists who like to tinker.

### Composible

In order to support a graphic user interface layer on top of the DSL, the code
should be easily generated and manipulated by programs. Smaller components
should be readily composed together to form larger components. Components should
be reusable. The most composible solution is to use pure data, and we will take
this approach.

### Extensible

To enable the functionalities beyond rules, the system is designed to be easily extensible by directly embedding user defined functions in the script. The goal is to have a system framework where advanced technology components such as natural language processing, machine learning and others could be plugged into.

## Data Structure

REP reuses the Clojure data structure for base syntax. On that syntactical
basis, REP codifies some specialized semantic rules. A reference to Clojure data
structures is at [this page](https://clojure.org/reference/data_structures).

Here we summarize the basic syntactic elements used in our language. Content
after `;` is comment. We use the following primitive data types:

### Scalar Values

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
### Collections

The following collection types are used in REP extensively.

#### Vector
Vector collection literal starts with `[` and ends with `]`. It contains an ordered collection of elements. Each element of the vector can be anything: scalar values or other collections.

```Clojure
;; a vector containing three elements: a double, a long, and ends with a string
[1.0 2 "a-string"]
;; another vector, containg three elements: a string, followed by
;; another vector, and ends with a symbol
["a-string" [:a 1] something]
```
