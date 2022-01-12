---
layout: default
title: Spring
has_children: true
nav_order: 2
permalink: Docs/ui-component/Spring
---

# Spring

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

The Spring Framework provides a comprehensive programming and configuration model for modern Java-based enterprise applications - on any kind of deployment platform.

A key element of Spring is infrastructural support at the application level: Spring focuses on the "plumbing" of enterprise applications so that teams can focus on application-level business logic, without unnecessary ties to specific deployment environments.

---

## Features

### Core technologies
Dependency injection, events, resources, i18n, validation, data binding, type conversion, SpEL, AOP.

### Testing
mock objects, TestContext framework, Spring MVC Test, WebTestClient.

### Data Access
transactions, DAO support, JDBC, ORM, Marshalling XML.

### Spring MVC and Spring WebFlux web frameworks.

### Integration
remoting, JMS, JCA, JMX, email, tasks, scheduling, cache.

### Languages
Kotlin, Groovy, dynamic languages.

---

## Inversion Of Control (IOC) and Dependency Injection

These are the design patterns that are used to remove dependency from the programming code. They make the code easier to test and maintain. Let's understand this with the following code:

```java
class Employee{  
    Address address;  
    Employee(){  
        address=new Address();  
    }  
}  
```

In such case, there is dependency between the Employee and Address (tight coupling). In the Inversion of Control scenario, we do this something like this:
```java
class Employee{  
    Address address;  
    Employee(Address address){  
        this.address=address;  
    }  
}  
```

Thus, IOC makes the code loosely coupled. In such case, there is no need to modify the code if our logic is moved to new environment.

In Spring framework, IOC container is responsible to inject the dependency. We provide metadata to the IOC container either by XML file or annotation.

---

## Advantage of Dependency Injection
- makes the code loosely coupled so easy to maintain
- makes the code easy to test

---

## Advantages of Spring Framework


There are many advantages of Spring Framework. They are as follows:

| Name        | Details          | 
|:-------------|:------------------|
| Predefined Templates           | Spring framework provides templates for JDBC, Hibernate, JPA etc. technologies. So there is no need to write too much code. It hides the basic steps of these technologies. Let's take the example of JdbcTemplate, you don't need to write the code for exception handling, creating connection, creating statement, committing transaction, closing connection etc. You need to write the code of executing query only. Thus, it save a lot of JDBC code.| 
| Loose Coupling | The Spring applications are loosely coupled because of dependency injection.   | 
| Easy to test           | The Dependency Injection makes easier to test the application. The EJB or Struts application require server to run the application but Spring framework doesn't require server.      |
| Lightweight           | Spring framework is lightweight because of its POJO implementation. The Spring Framework doesn't force the programmer to inherit any class or implement any interface. That is why it is said non-invasive. | 
| Fast Development           | The Dependency Injection feature of Spring Framework and it support to various frameworks makes the easy development of JavaEE application. | 
| Powerful abstraction           | It provides powerful abstraction to JavaEE specifications such as JMS, JDBC, JPA and JTA. | 
|  Declarative support           | It provides declarative support for caching, validation, transactions and formatting. | 



---

## Dependency Injection

Dependency Injection is the most important feature of Spring framework. Dependency Injection is a design pattern where the dependencies of a class are injected from outside, like from an xml file. It ensures loose-coupling between classes.

In a Spring MVC application, the controller class has dependency of service layer classes and the service layer classes have dependencies of DAO layer classes.

Suppose class A is dependent on class B. In normal coding, you will create an object of class B using ‘new’ keyword and call the required method of class B. However, what if you can tell someone to pass the object of class B in class A? Dependency injection does this. You can tell Spring, that class A needs class B object and Spring will create the instance of class B and provide it in class A.

In this example, we can see that we are passing the control of objects to Spring framework, this is called Inversion of Control (IOC) and Dependency injection is one of the principles that enforce IOC.


---

## Types of Dependency Injection

```yaml
---
layout: default
title: Types of Dependency Injection
nav_order: 2
has_children: true
---
```

## Reference Links

###  [Spring Framework](https://spring.io/projects/spring-framework#overview)
