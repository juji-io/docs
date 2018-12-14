# User Defined Functions 

Users may define and call custome functions of their own in REP script. Currently, Juji supports user defined functions (UDF) written in programming languages running on Java Virtual Machine (JVM), such as Java, Clojure, Scala, Kotlin and so on, as long as they can be called through Java inter-operations. 

For custom functionalities written in non-JVM languages, it is possible to access them via HTTP requests using `make-request` system function if they are exposed as REST APIs.

Juji does not make a lot of assumptions on what your JVM UDFs do, except that these functions will be treated similarly as REP system functions, i.e. as boolean functions in trigger pattern and as output functions in action pattern.

Different users' UDFs run in their own isolated environment and are not aware of one another. UDFs also run in a JVM sandbox to ensure security of the system.

Exceptions thrown in UDFs are logged and the thowing UDF will return `nil` in these cases.

## JVM UDFs

User can write code in JVM languages and package the compiled classes into a jar file, e.g. using standard package management tools such as maven. User can then upload the jar file to Juji so that these code is avaiable for the user's REP script. 

### Upload Jar

In IDE file browser, click open the desired engagement, click open `Config` file, on the menu bar of the main content panel, you will see a `Add Jar` button. 

#### Jar without dependencies

To reduce the sizes of uploaded file, it is recommended to upload jar files that only contain your own classes. The dependencies should be described in a `pom.xml` file that must also be uploaded. Juji will automatically resolve these dependencies if they are available on maven central.

#### Jar with dependencies

If the package uses libriaries that are not available on maven central, these libriaries should be included in the uploaded jar file, e.g. using maven-assembly-plugin. 

If all required dependencies are included in the uploaded jar file, it is not necessary to upload a `pom.xml` file.

### Call UDFs via Java Interops

Standard Clojure-Java interops syntax can be used in REP script to call UDFs:

```Clojure
(AClass/aClassMethod "argument")
(doto (AClass. "constructorArgument")
  (.instanceMethodA "argument1")
  (.instanceMethodB))
```

## Clojure UDF

User can directly write Clojure functions in REP script.
