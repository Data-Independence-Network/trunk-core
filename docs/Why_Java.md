# Why Java

The reason why Java is chosen.

## 1 - Well Known and close

Java is the most popular framework for writing server code, period.  Also it's 
syntactically close to TypeScript, which makes it a natural choice for DIN, since
[Beyond Decentralized](https://github.com/beyond-decentralized) code is in TypeScript.
Even more importantly, it's very familiar to the initial programmer for DIN.

## 2 - It can be CPU & RAM efficient

A core goal of DIN is to provide the ability to run small family/group servers at minimal
cost. Writing server code in Java is ideal for this:
* [GraalVM](https://www.graalvm.org/) can compile Java to statically linked native
binaries that can run in a scratch image (without an OS wrapper or libraries, with just
the one binary) and provides a build-time initialization mechanism to remove JVM runtime
checks.
* [Quarkus](https://quarkus.io/) is a [Vert.x](https://vertx.io/) based web framework that
optimizes OS thread utilization.
* [AIRport](https://github.com/beyond-decentralized/AIRport) JS apps can compile to JVM
bytecode via GraalJS and run in the same process as the rest of the server infrastructure.

## 3 - It can be file access efficient

With the same core goal of a minimal cost, small family/group server in mind:
* [Chronile Queue](https://github.com/OpenHFT/Chronicle-Queue) provides off-heap file
management with random queue access which can be embeded into the same micro
trunk/branch binary (for small family/group servers).
* Once code stability has been proven, SQLite can also be embedded into the same GraalVM
binary (again for micro servers).
* The entire small family/group server can run in one process, sharing its memory and
making it optimal for deployment on shared VCPU infrastructure.  Possibly it can be made
to (or may already be capable of) run(ning) everything in the same OS thread (if needed).

## 4 - Lots of libraries

Java has a library for just about anything you can think of.

## 5 - It has room to grow
Java is still under active development (Thank you Oracle!) and so is GraalVM with
future performance improvements to come.
