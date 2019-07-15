![Coderland logo](images/Coderland_logo.png)

# `vertx-starter`

## Overview

This is a simple application to get you started with the Vert.x toolkit. 
To illustrate the Vert.x event loop, it features
two processes running simultaneously. One process (`vertx.setPeriodic()`) 
writes a message to the
console every two seconds, while the other (`vertx.createHttpServer()`) 
servers requests on HTTP port 8080. 

## Building and running the code

The following commands build and run the code: 

```
mvn clean package
java -jar target/vertx-starter-1.0-SNAPSHOT.jar
```

## Sample output 

Sample output looks like this: 

```
doug@dtidwell-mac:~/vertx-starter $ java -jar target/vertx-starter-1.0-SNAPSHOT.jar 
----------------------------------------------
---> Coderland now listening on localhost:8080
----------------------------------------------
Jun 26, 2019 8:33:59 AM io.vertx.core.impl.launcher.commands.VertxIsolatedDeployer
INFO: Succeeded in deploying verticle
Server run time: 2 seconds.
Server run time: 4 seconds.
Request #1 from 192.168.1.67
Server run time: 6 seconds.
Request #2 from 192.168.1.76
Server run time: 8 seconds.
Server run time: 10 seconds.
Request #3 from 0:0:0:0:0:0:0:1
Server run time: 12 seconds.
Server run time: 14 seconds.
Server run time: 16 seconds.
Request #4 from 192.168.1.67
Server run time: 18 seconds.
Server run time: 20 seconds.
Request #5 from 192.168.1.76
Server run time: 22 seconds.
Server run time: 24 seconds.
^C---------------------------------------------
---> Coderland signing off! Have a great day.
---------------------------------------------
```

## Some notes on the output: 

First of all, notice that we `@Override` the `start()` and `stop()` methods. 
Overriding the `start()` method is typical because you probably want to set 
up some things when your verticle is loaded. Overriding `stop()` is less 
common, but notice that typing Ctrl+C at the command line invoked the `stop()` 
method before the system killed the code. 
 
Second, the print statements in the `start()` method were executed before the 
verticle was up and running. The Vert.x runtime doesn’t print the 
“Succeeded in deploying verticle” message until the `start()` method is 
finished. The output says the code is listening on port 8080, but that’s not
technically true until a fraction of a second later when the verticle is fully loaded. 
 
You can see the two asynchronous processes the verticle uses. 
One (`vertx.setPeriodic()`) is invoked every 
two seconds, the other (`vertx.createHttpServer()`) is invoked whenever an 
HTTP request comes in on localhost:8080. 
As long as the verticle is running, these two processes operate 
independently of each other.

## The Reactica roller coaster

Coderland's [Reactica roller coaster](https://developers.redhat.com/coderland/reactive)
features a complete, sophisticated example of a system 
of reactive Vert.x microservices that work together. 

:gift: [REPO: The Reactica roller coaster](https://github.com/reactica/rhte-demo)

### Part 1: An introduction to reactive programming and Vert.x 

:page_facing_up: [ARTICLE: Part 1: An introduction to reactive programming and Vert.x](https://developers.redhat.com/coderland/reactive/reactive-intro)

:clapper: [VIDEO: Part 1: An introduction to reactive programming and Vert.x](https://youtu.be/)

### Part 2: Building a reactive system

:page_facing_up: [ARTICLE: Part 2: Building a reactive system](https://developers.redhat.com/coderland/reactive/building-a-reactive-system/)

:clapper: [VIDEO: Part 2: Building a reactive system](https://youtu.be/)

### Part 3: A reactive system in action

:page_facing_up: [ARTICLE: Part 3: A reactive system in action](https://developers.redhat.com/coderland/reactive/reactive-system-in-action/)

:clapper: [VIDEO: Part 3: A reactive system in action](https://youtu.be/)

## Other useful links

:book: Clement Escoffier's excellent book [Building Reactive Microservices in Java](https://developers.redhat.com/books/building-reactive-microservices-java/old/), available for free from [the Red Hat Developer Program](https://developers.redhat.com/)

:page_facing_up: Andre Staltz's [The introduction to Reactive Programming you've been missing](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754)

:page_facing_up: [The Reactive Manifesto](https://www.reactivemanifesto.org/)

:page_facing_up: [The Vert.x home page](https://vertx.io)

***

Coderland :roller_coaster::rocket::ferris_wheel: is an imaginary theme park for learning. developer training and Red Hat software. See [the Red Hat Developer Program](https://developers.redhat.com/) for more great stuff.