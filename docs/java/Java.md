---
layout: default
title: Java
has_children: true
nav_order: 2
resource: true
desc: "Java interview questions and answers."
categories: [Java,Java8,Multithreading]
permalink: docs/java
---



# Java

{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

Java is a general-purpose, class-based, object-oriented programming language designed for having lesser implementation dependencies. It is a computing platform for application development. Java is fast, secure, and reliable, therefore. It is widely used for developing Java applications in laptops, data centers, game consoles, scientific supercomputers, cell phones, etc.

**Java Features**

Here are some important Java features:

- It is one of the easy-to-use programming languages to learn.
- Write code once and run it on almost any computing platform.
- Java is platform-independent. Some programs developed in one machine can be executed in another machine.
- It is designed for building object-oriented applications.
- It is a multithreaded language with automatic memory management.
- It is created for the distributed environment of the Internet.
- Facilitates distributed computing as its network-centric.

---

## Components Of Java

A Java Programmer writes a program in a human-readable language called Source Code. Therefore, the CPU or Chips never understand the source code written in any programming language.

###  Java Development kit (JDK)

JDK is a software development environment used for making applets and Java applications. The full form of JDK is Java Development Kit. Java developers can use it on Windows, macOS, Solaris, and Linux. JDK helps them to code and run Java programs. It is possible to install more than one JDK version on the same computer.

**Why use JDK?**

Here are the main reasons for using JDK:


JDK contains tools required to write Java programs and JRE to execute them.
It includes a compiler, Java application launcher, Appletviewer, etc.
Compiler converts code written in Java into byte code.
Java application launcher opens a JRE, loads the necessary class, and executes its main method.

###  Java Virtual Machine (JVM)
Java Virtual Machine (JVM) is an engine that provides a runtime environment to drive the Java Code or applications. It converts Java bytecode into machine language. JVM is a part of the Java Run Environment (JRE). In other programming languages, the compiler produces machine code for a particular system. However, the Java compiler produces code for a Virtual Machine known as Java Virtual Machine.

**Why JVM?**

Here are the important reasons of using JVM:

JVM provides a platform-independent way of executing Java source code.
It has numerous libraries, tools, and frameworks.
Once you run a Java program, you can run on any platform and save lots of time.
JVM comes with JIT (Just-in-Time) compiler that converts Java source code into low-level machine language. Hence, it runs faster than a regular application.

###  Java Runtime Environment (JRE)
JRE is a piece of software that is designed to run other software. It contains the class libraries, loader class, and JVM. In simple terms, if you want to run a Java program, you need JRE. If you are not a programmer, you don’t need to install JDK, but just JRE to run Java programs.

**Why use JRE?**

Here are the main reasons of using JRE:

JRE contains class libraries, JVM, and other supporting files. It does not include any tool for Java development like a debugger, compiler, etc.
It uses important package classes like math, swing, util, lang, awt, and runtime libraries.
If you have to run Java applets, then JRE must be installed in your system.

---

## Exceptions

Exception is an error event that can happen during the execution of a program and disrupts its normal flow.

Types of Java Exceptions

###  Checked Exception
The classes which directly inherit Throwable class except RuntimeException and Error are known as checked exceptions e.g. IOException, SQLException etc. Checked exceptions are checked at compile-time.

###  Unchecked Exception
The classes which inherit RuntimeException are known as unchecked exceptions e.g. ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException etc. Unchecked exceptions are not checked at compile-time, but they are checked at runtime.

###  Error
Error is irrecoverable e.g. OutOfMemoryError, VirtualMachineError, AssertionError etc.


###  Hierarchy of Java Exception classes


<img src="images/Exceptions.png" width="700"  />





## For more information

1. [Java, J2EE, JSP, Servlet, Hibernate Interview Questions](https://github.com/learning-zone/java-interview-questions)

