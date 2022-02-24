---
layout: default
title: Spring Data JPA
parent: Spring
resource: true
desc: "Spring Data JPA interview questions and answers."
categories: [ Spring Data JPA]
---

# Spring Data JPA
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

When you implement a new application, you should focus on the business logic instead of technical complexity and boilerplate code. That’s why the Java Persistence API (JPA) specification and Spring Data JPA are extremely popular. JPA handles most of the complexity of JDBC-based database access and object-relational mappings. On top of that, Spring Data JPA reduces the amount of boilerplate code required by JPA. That makes the implementation of your persistence layer easier and faster.

## What is JPA?

JPA or Java Persistence API is the Java specification for accessing, managing and persisting data between Java classes or objects and relational database. The specification was introduced as part of EJB 3.0.

JPA is not an implementation or product, it is just a specification. It contains set of interfaces which need to be implemented. It is a framework that provides an extra layer of abstraction on the JPA implementation. The repository layer will contain three layers as mentioned below.

**Spring Data JPA**: – This provides spring data repository interfaces which are implemented to create JPA repositories.
**Spring Data Commons**: – It provides the infrastructure that is shared between data store specific spring data projects.
**The JPA provider** which implements the JPA persistence API.

Spring data JPA allows us not to write any boilerplate code by adding an additional repository layer.

##  Features

### No-code Repositories

The repository pattern is one of the most popular persistence-related patterns. It hides the data store specific implementation details and enables you to implement your business code on a higher abstraction level.

Implementing that pattern isn’t too complicated but writing the standard CRUD operations for each entity creates a lot of repetitive code. Spring Data JPA provides you a set of repository interfaces which you only need to extend to define a specific repository for one of your entities.

###  Reduced boilerplate code
To make it even easier, Spring Data JPA provides a default implementation for each method defined by one of its repository interfaces. That means that you no longer need to implement basic read or write operations. And even so all of these operations don’t require a lot of code, not having to implement them makes life a little bit easier and it reduces the risk of stupid bugs.

###  Generated queries

Another comfortable feature of Spring Data JPA is the generation of database queries based on method names. As long as your query isn’t too complex, you just need to define a method on your repository interface with a name that starts with find…By. Spring then parses the method name and creates a query for it.

Here is a simple example of a query that loads a Book entity with a given title. Internally, Spring generates a JPQL query based on the method name, sets the provided method parameters as bind parameter values, executes the query and returns the result.

```java
public interface BookRepository extends CrudRepository<Book, Long> {
    Book findByTitle(String title);
}
```

## Repositories in Spring Data JPA

There are 3 repository interfaces that you should know when you use Spring Data JPA:

###  CrudRepository
CrudRepository interface defines a repository that offers standard create, read, update and delete operations.

###  PagingAndSortingRepository
The PagingAndSortingRepository extends the CrudRepository and adds findAll methods that enable you to sort the result and to retrieve it in a paginated way. Both interface are also supported by other Spring Data projects, so that you can apply the same concepts to different datastores.

###  JpaRepository
The JpaRepository adds JPA-specific methods, like flush() to trigger a flush on the persistence context or findAll(Example<S> example) to find entities by example, to the PagingAndSortingRepository. 




---

## More Details: 
1. [What is Spring Data JPA? And why should you use it?](https://thorben-janssen.com/what-is-spring-data-jpa-and-why-should-you-use-it/)