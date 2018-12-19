# User Defined Functions

Users may define and call custom functions of their own in REP script.
Currently, Juji supports user defined functions (UDF) written in programming
languages running on Java Virtual Machine (JVM), such as Java, Clojure, Scala,
Kotlin and so on, as long as they can be called through [Clojure's Java
interop syntax](https://clojure.org/reference/java_interop).

Juji does not make a lot of assumptions about what your UDFs do, except that
these functions will be used similarly as REP system functions in REP script, i.e.
as Boolean functions in trigger pattern and as output functions in action pattern.

Different engagement's UDF run in different isolated sandbox to ensure security
and privacy. Exceptions thrown in UDFs are logged and the thowing UDF will
return `nil` in these cases.

## JVM UDF

User can write code in JVM languages and package the compiled classes into a JAR
file, e.g. using standard package management tools such as
[Maven](https://maven.apache.org/). User then upload the JAR file to Juji, so
that the JAR is deployed to a secure private Maven repository for the user's REP
script to access.

### Upload JAR

In IDE file browser, click open the desired engagement, click open `Config` file, on the menu bar of the main content panel, you will see a `Add Jar` button.

<p align="center"><img src="../img/config-jar.png" alt="Add JAR button" width="650"/></p>

Click the button to see a dialog for uploading the JAR file.

<p align="center"><img src="../img/upload-jar.png" alt="Upload JAR dialog" width="550"/></p>

The JAR file field is required and other fields are optional. However, `groupId`
(organization identifier), `artifactId` (package identifier) and `version`
are all required information for deployment to the private Maven
repository. You can supply a `pom.xml` file that contains these entries, or Juji
will attempt to find the `pom.xml` file inside the JAR file, or you can fill in
the form.

#### JAR without dependencies

To reduce the size of the uploaded file, it is recommended to upload JAR files that
only contain your own classes. The dependencies should be described in a
`pom.xml` file that is inside the JAR or is uploaded along with the JAR. Juji will
automatically resolve these dependencies if they are available on [Maven
Central](https://mvnrepository.com/repos/central) or [clojars](https://clojars.org).
rarroup
#### JAR with dependencies

If the package uses libraries that are not publicly available on Maven Central
or clojars, these libraries should be included in the uploaded JAR file, e.g. by
using tools such as
[maven-assembly-plugin](http://maven.apache.org/plugins/maven-assembly-plugin/).

### Import Dependencies

Follow these two steps to import dependencies into your REP script, whether the
dependency is on a uploaded JAR file or on an artifact available on Maven
Central or clojars public repositories.

#### Add `:dependencies` in `config` form

First the REP script needs to tell the compiler that there are external
dependencies. The dependencies should be declared in the `config` form of the
script, under `:dependencies` key.

When the script is compiled by clicking the `Compile` button, the referred
dependencies will be fetched from remote repositories and add to the class path.
A dedicated Java class loader will then be created to load the dependencies.

##### Uploaded dependency

After a JAR file is successfully uploaded, the `Chat Config` document will be
automatically updated to include the dependencies under a `:dependencies` key. The
value is a vector of dependency coordinates, and the individual dependency
coordinate has this format: `[<groupId>/<artifactId>  <version>]`

```Clojure
;; Chat Config document
{...
 :dependencies [["io.juji/java-test" "1.2.2"]
                ["com.mycorp/mylib" "2.3.1"]]}
```

Click `Generate Script` drop down menu, and select either `Preview` or `Web`
releases, a REP script will be generated from the config document. Find the
generated script in file browser, click open the file, you will see that the
dependency coordinates have been copied to the `config` form of the script, also
under `:dependencies` key.

```Clojure
;; REP script
(config {...
         :dependencies [[io.juji/java-test "1.2.2"]
                        [com.mycorp/mylib "2.3.1"]]})
```

!!! note
    There is a slight difference in the format of the dependencies value:
    `groupId/artifactId` in REP script is not quoted.


##### Public dependency

If you know the coordinate of a publicly available library on Maven Central or
clojars, you can add it to the `:dependencies` key manually in the `config`
section of the REP script, just like the auto-generated ones above.

#### Add `:import` in `ns` form

The second step is to tell the REP runtime which classes should be imported into
the script namespace, so that these classes can be used by UDFs. To do that, you
need to modify the `ns` form of the script to include a `(:import
[<class1 path>] [<class2 path>] ...)` clause, e.g.

```clojure
(ns juji.eng1.kaya
  (:import [io.juji.javatest Client]
           [com.mycorp.mylib AwesomeClass UsefulClass]))

```
This will make three classes available for the REP script: `io.juji.javatest.Client`,
`com.mycorp.mylib.AwesomeClass` and `com.mycorp.mylib.UsefulClass`.

### Call Function via Java Interop

Once the classes are imported, standard [Clojure-Java interop
syntax](https://clojure.org/reference/java_interop) can be used in REP script to
call JVM UDF, e.g.

```Clojure
(AClass/aClassMethod "argument")      ; call class method
(doto (AClass. "constructorArgument") ; create new object with constructor
  (.instanceMethodA "argument1")      ; invoke instance method on object
  (.instanceMethodB))                 ; invoke another method on the same object
```

As you can see, this is a very concise way of calling Java.

## Clojure UDF

Juji is developed in [Clojure](https://clojure.org), a powerful general
purpose programming language. Juji users can harness the most of
the same power in REP script as well, by directly writing Clojure functions in
REP scripts using the standard
[Clojure function syntax](https://clojure.org/guides/learn/functions).

```Clojure
(ns com.mycorp.eng2.kaya
  (:require [java-time :as time])) ; this is a Clojure library

(defn first-monday-of-month
  "Define a UDF that returns the date object of the first Monday
  of this month"
  []
  (time/adjust (time/local-date) :first-in-month :monday))

(deftopic first-monday-month []
  [you know first monday month]
  ["I know. It is" (time/format "MM/dd" (first-monday-of-month))])

(config {...
         :dependencies [[clojure.java-time "0.3.2"]]
         ...})
```

This code requires a Clojure library called `java-time`. Instead of using
the `:import` keyword for Java classes, `:require` should be used for Clojure
libraries.

The UDF is defined using a `defn` form, a standard way of creating new function
in Clojure. The function is called in the topic as part of the action.

We also added the coordinate of the library to `:dependencies` key of the
`config` map. Since this library is publicly available on clojars, Juji will
fetch the library and put it on classpath during script compilation.



## Other Languages

For custom functionalities written in non-JVM languages, it is possible to
access them via HTTP requests using `make-request` [system
function](function.md) if they are exposed as REST APIs. If they are accessible
via other protocols, you can write JVM based UDFs to implement these protocols.

Or if you prefer to write your own program in whatever languages and run your
own application on your own platform, e.g. on mobile devices, we have a suite of [GraphQL
API](api.md) that you can use to access Juji platform remotely, as long as your
program can access Juji through HTTPS and can talk GraphQL.
