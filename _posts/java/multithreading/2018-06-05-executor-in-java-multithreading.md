---
layout: post
title: Executor in Java Multithreading
sidebar: nav-java-multithreading
toc: true
categories: java multi-threading
---
* Table of Contents
{:toc}
## What is an Executor ?


## Creating Simple Executors
In this section we will create some basic executors.

### Simlpe Executor
An Executor can be as simple as following

```java
package ekiras.multithreading;

import java.util.concurrent.Executor;

/**
 * @author ekiras
 */
public class SimpleExecutor implements Executor {

    @Override
    public void execute(Runnable runnable) {
        runnable.run();
    }
}

```
The above executor takes a runnable object and calls the run method.  

### Thread Executor
Another example of a simple exector can be as following

```java
package ekiras.multithreading;

import java.util.concurrent.Executor;

/**
 * @author ekiras
 */
public class SimpleThreadExecutor implements Executor{

    @Override
    public void execute(Runnable runnable) {
        new Thread(runnable).run();
    }
}

```
The above executor takes a runnable and creates a new thread with the runnable and calls the run method.
This will make the runnable to execute in a new thread. 