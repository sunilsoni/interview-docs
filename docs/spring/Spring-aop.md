---
layout: default
title: Spring AOP
parent: Spring
resource: true
desc: "Spring AOP interview questions and answers."
categories: [Spring AOP]
---

# Spring AOP
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

##  Introducing Spring AOP

Aspect oriented Programming is programming paradigm which is analogous to object oriented programming. Key unit of object oriented programming is class, similarly key unit for AOP is Aspect. Aspect enable modularisation of concerns such as transaction management, it cut across multiple classes and types. It also refers as a crosscutting concerns.

## Why AOP?
It provides pluggable way to apply concern before, after or around business logic.
Lets understand with the help of logging. You have put logging in different classes but for some reasons, if you want to remove logging now, you have to make changes in all classes but you can easily solve this by using aspect. If you want to remove logging, you just need to unplug that aspect.

## AOP concepts
- **Aspect**: An Aspect is a class that implements concerns that cut across different classes such as logging. It is just a name.
- **Joint Point** : It is a point in execution of program such as execution of method. In Spring AOP, a join point always represents a method execution.
- **Advice** : Action taken by  aspect at particular join point. For example: Before execution of getEmployeeName() method, put logging. So here, we are using before advice.
- **Pointcut** : Pointcut is an expression that decides execution of advice at matched joint point. Spring uses the AspectJ pointcut expression language by default.
- **Target object** : These are the objects on which advices are applied. For example: There are the object on which you want to apply logging on joint point.
- **AOP proxy** : Spring will create JDK dynamic proxy to create proxy class around target object with advice invocations.
- **Weaving** : The process of creating proxy objects from target object may be termed as weaving.

## Types of Advices 
Advice is action taken by aspect at particular joint point.
- **Before Advice**: it executes before a join point.
- **After Returning Advice**: it executes after a joint point completes without any exception.
- **After Throwing Advice**: it executes if method exits by throwing an exception.
- **After Advice**: it executes after a join point regardless of outcome.
- **Around Advice**: It executes before and after a join point.

## Reference Links
- [Spring AOP tutorial-java2blog.com](https://java2blog.com/spring-aop-tutorial/)