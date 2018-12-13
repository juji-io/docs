# User Defined Functions 

Users may define and call custome functions of their own in REP script. Currently, Juji support user defined functions (UDF) written in Java and Clojure programming languages. For custom functionalities written in other languages, it is possible to access them with HTTP requests using `make-request` system function.

Juji does not make a lot of assumptions on what these UDFs do, except that these functions will be treated as the same as REP functions, i.e. as boolean functions in trigger pattern and as output functions in action pattern.

Different users' UDFs run in their own isolated environment and do not interfere with one another. They also run in JVM sandbox to ensure security of the system.

Exceptions thrown in UDFs are logged and the thowing UDF will return nil in these cases.

## Java UDF

User can write code in Java and package the compiled classes into a jar file, e.g. using standard tools such as maven. User can then upload the jar file to Juji so that these code is avaiable for the user's REP script. 

### Upload Jar

In IDE broswer, right click an engagement.

#### Jar without dependencies

To reduce the sizes of uploaded file, it is recommended to upload jar file that only contains your own classes. The dependencies should be described in a `pom.xml` file that should also be uploaded. Juji will automatically resolve these dependencies if they are available on maven central.

#### Jar with dependencies

If the package use libriaries that are not available on maven central, these libriaries should be included in the uploaded jar file. 

If all required dependencies are included in the uploaded jar files, it is no longer necessary to upload a `pom.xml` file.

### Call Java

Standard Clojure Java interops syntax can be used in REP script to call Java functionalities.

## Clojure UDF


