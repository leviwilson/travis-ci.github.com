---
title: Building a Java project
layout: en
permalink: java/
---

### What This Guide Covers

This guide covers build environment and configuration topics specific to Java projects. Please make sure to read our [Getting Started](/docs/user/getting-started/) and [general build configuration](/docs/user/build-configuration/) guides first.

## Overview

Travis CI environment provides OpenJDK 6, Maven 3, Gradle 1.0-milestone 7 and Ant 1.7. Java project builder has reasonably good defaults for projects that use Gradle, Maven or Ant, so quite often you won't have to configure anything beyond

    language: java

in your `.travis.yml` file.

Support for multiple JDKs will be available in the future.

## Projects Using Maven

### Default Test Command

if your project has `pom.xml` file in the repository root but no `build.gradle`, Travis Java builder will use Maven 3 to build it. By default it will use

    mvn test

to run your test suite. This can be overriden as described in the [general build configuration](/docs/user/build-configuration/) guide.

### Dependency Management

Before running tests, Java builder will execute

    mvn install -DskipTests=true

to install your project's dependencies with Maven.

## Projects Using Gradle

### Default Test Command

if your project has `build.gradle` file in the repository root, Travis Java builder will use Gradle to build it. By default it will use

    gradle check

to run your test suite. This can be overriden as described in the [general build configuration](/docs/user/build-configuration/) guide.

### Dependency Management

Before running tests, Java builder will execute

    gradle assemble

to install your project's dependencies with Gradle.

## Projects Using Ant

### Default Test Command

If Travis could not detect Maven or Gradle files, Travis Java builder will use Ant to build it. By default it will use

    ant test

to run your test suite. This can be overriden as described in the [general build configuration](/docs/user/build-configuration/) guide.

### Dependency Management

Because there is no single standard way of installing project dependencies with Ant, Travis CI Java builder does not have any default for it. You need to specify the exact commend to run using `install:` key in your `.travis-yml`, for example:

    language: java
    install: ant deps


## Testing Against Multiple JDKs

To test against multiple JDKs, use the `:jdk` key in `.travis.yml`. For example, to test against OpenJDK 6 and OpenJDK 7:

    jdk:
      - openjdk6
      - openjdk7

To test against OpenJDK 7 and Oracle JDK 7u4:

    jdk:
      - openjdk7
      - oraclejdk7

Travis CI provides OpenJDK 6, OpenJDK 7 and Oracle JDK 7u4. Sun JDK 6 is not provided and because it is EOL in November 2012,
will not be provided.

JDK 7 is backwards compatible, we think it's time for all projects to start testing against JDK 7 first and JDK 6 if resources permit.



## Examples

* [JRuby](https://github.com/jruby/jruby/blob/master/.travis.yml)
* [Riak Java client](https://github.com/basho/riak-java-client/blob/master/.travis.yml)
* [Cucumber JVM](https://github.com/cucumber/cucumber-jvm/blob/master/.travis.yml)
* [Symfony 2 Eclipse plugin](https://github.com/pulse00/Symfony-2-Eclipse-Plugin/blob/master/.travis.yml)
* [RESTHub](https://github.com/pullrequest/resthub/blob/master/.travis.yml)
* [Joni](https://github.com/jruby/joni/blob/master/.travis.yml), JRuby's regular expression implementation
* [Android](https://gist.github.com/2864158), using the [maven-android-plugin](http://code.google.com/p/maven-android-plugin/)
