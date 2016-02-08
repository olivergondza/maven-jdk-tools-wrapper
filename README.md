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

- The path to the jar is different on OS X variant of sun/oracle JDKs ([JDK tools.jar as maven dependency](http://stackoverflow.com/questions/3080437/jdk-tools-jar-as-maven-dependency/29585979#29585979))
- The file was removed in Java 9 and the dependency should not be declared ([Declare maven dependency on tools.jar to work on JDK 9](http://stackoverflow.com/a/35244168/2091470))

## Solution

There are tricks to get this working across Java versions and systems. Maven profiles
can distinguish those situations and declare particular dependency if needed.
Consult the `pom.xml` for more details.

As the actual maven wizardry is quite elaborate, surprising to newcomers and a
subject of future improvements, it is better not co copy-paste it around. Hence
this module exists so you do not have to know or care about the details.

This dependency (hosted on maven central) do not have any runtime footprint (external
dependencies, classes loaded) but merely instruct maven what to do on compile time.
All the transitive dependencies brought to the client projects are `system` scoped.
