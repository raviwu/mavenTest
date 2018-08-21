Simple Repo for Maven studying

## Version

Development starts off as a SNAPSHOT.

- myapp-1.0-SHAPSHOT.jar
- changes always downloaded
- saves you from rereleasing versions for development
- never deploy to production with a SNAPSHOT

Besides from SNAPSHOT, other naming conventions were left by the users. A release doesn't have a specific naming convension.

[Maven Guide for version naming convension](https://maven.apache.org/guides/mini/guide-naming-conventions.html)


- myapp-1.0.jar
- myapp-1.0.1.jar

Industry common terms that does not affect maven.

- myapp-1.0-M1.jar (milestone release)
- myapp-1.0-RC1.jar (release candidate)
- myapp-1.0-RELEASE.jar (release)
- myapp-1.0-Final.jar (release)

## Type (packaging)

Current core packaging types: pom, jar, maven-plugin, ejb, war, ear, rar, par

Default packaging type is jar.

The type of pom is referred to as a dependency pom. Maven downloads dependencies from that pom.

## Scope

- compile: default scope, artifacts available everywhere
- provided: like compile, means that the artifact is going to be provided where it is deployed
    - servlet-api.jar
    - xml-apis
    - Available in all phases, but not included in final artifact
- runtime: not needed for compilation, but needed for execution
    - Not available for compilation, but included in all other phases
    - Not included in final artifact
- test: only available for the test compilation and execution phase
- system: similar to provided, you specify a path to the jar on your file system (rarely use)
- import: related to dependencyManagement

## Repository

### Local repository

Local repo is where maven stores everything it downloads, default directory is `~/.m2`. It stores artifacts using the information that you provided for artifactId, groupId, and version.

### Maven repositories

Maven repositories is a http accessible location that user download files from.

Default location is http://repo.maven.apache.org/maven2, most open source projects can be found here.

Multiple repositories allowed in Maven setup.

### Plugin repositories

Identical to Dependency Repositories, but just deals with Plugins. Will only look for Plugins, by design usually a separate repository.

## Plugins

### Goals

The default goals are plugins configured in the maven install. Things like `clean`, `compile`, `test`, `package`, `install`, and `deploy`.

Super pom has these goals defined in it, which are added to users' effective pom.

Goals are always tied to a phase.

### Phases

1. validate: validate the project is correct and all necessary information is available
2. compile: compile the source code of the project
3. test: test the compiled source code
4. package: pachages all the code in its defined package type, like `jar`
5. integration-test: deploy and run integration test (function after maven 3)
6. verify: run checks against package to verify integrity
7. install: install the package in our local repo
8. deploy: copy final package to a remote repository

### Compiler Plugin

Used to compile source code, which invokes `javac` with the classpath set from the dependencies.

Default to Java 1.5 regardless of what JDK is installed.

Configuration section allows customization

- Includes/Excludes
- Fork
- Memory
- Source/target

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>2.5.1</version>
    <configuration>
        <fork>true</fork>
        <meminitial>128m</meminitial>
        <maxmem>512m</maxmem>
        <source>1.8</source>
        <target>1.8</target>
    </configuration>
</plugin>
```

### Jar Plugin

Used to package code into a jar, which is tied to the package phase.

Configuration section allows customization:

- Includes/Excludes
- Manifest

### Source Plugin

Used to attach source code to a jar, tied to the package phase in default but often overridden to a later phase.

### Javadoc Plugin

Used to attach Javadocs to a jar, tied to the package phase in default but often overridden to a later phase.

Usually just use the defaults, but many customization optios for Javadoc format. [REF](https://maven.apache.org/plugins/maven-javadoc-plugin/)
