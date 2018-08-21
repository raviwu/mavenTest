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
