---
layout: post
title: How to run Spring boot Application
tags: Gradle Maven SpringBoot Spring
author: Ekansh Rastogi
sidebar: nav-spring-boot-setup
categories: spring-boot setup
---

### How to run a Spring Boot Application using Maven/ Gradle

If you are using Maven as a build tool you can run the project using the following command

```
mvn spring:run
```
If you are using Gradle as a build tool you can the project as

```
gradle bootRun
```

### Running applicaion using Gradle wrapper
You can also the spring boot application using the gradle wrapper as follows

```
gradlew bootRun 
```
and on windows 

```
gradlew.bat bootRun
```