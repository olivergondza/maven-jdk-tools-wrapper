# Maven jdk.tools wrapper

Universal dependency to build against jdk.tools (AKA tools.jar) in a portable way

## TL;DR

When maven gives you headaches trying to use some of the `tools.jar` classes (because
the system scoped dependency have different paths in different JDKs or does not
even exist), following dependency should get you going:

```
    <dependency>
      <groupId>com.github.olivergondza</groupId>
      <artifactId>maven-jdk-tools-wrapper</artifactId>
      <version>0.1</version>
    </dependency>
```

## Problem

Prior Jigsaw introduced in Java 9, maven needs to pass the jar on `javac` classpath
at compile time to build projects referring to its classes. Despite the fact the jar
is distributed together with JDK, maven needs to be instructed to use it explicitly.
`system` dependency scope is here to do just that but there are still some caveats
to keep in mind:

- The path to the jar is different on OS X variant of sun/oracle JDKs.
- The file was removed in Java 9 and the dependency should not be declared.

## Solution

There are tricks to get this working across Java versions and systems. Maven profiles
can distinguish those situations and [declare particular dependency](/olivergondza/maven-jdk-tools-wrapper/blob/master/pom.xml) if needed.

Maintaining such a beast in `pom.xml` is what we all try to stay away from. Hence
this module exists so you do not have to know or care.
