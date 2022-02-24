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

Spring Data Commons project provides repository abstraction which is extended by the datastore-specific subprojects.

We have to be familiar with the Spring Data repository interfaces as it will help us with the implementation of the interfaces. Let’s have a look at the interfaces.

###  Spring Data Commons

Following interfaces are provided as part of this project:

**Repository<T, ID extends Serializable>**  : 
This interface is a marker interface.
- It captures the type of the managed entity and the type of the entity’s id.
- It helps the Spring container to discover the “concrete” repository interfaces when classpath is scanned.

**CrudRepository<T, ID extends Serializable>** : 
- It provides CRUD operations for the managed entity.
- CrudRepository interface defines a repository that offers standard create, read, update and delete operations.

**PagingAndSortingRepository<T, ID extends Serializable>** : 
- This interface declares the methods that are used to sort and paginate entities that are retrieved from the database.
- The PagingAndSortingRepository extends the CrudRepository and adds findAll methods that enable you to sort the result and to retrieve it in a paginated way. Both interface are also supported by other Spring Data projects, so that you can apply the same concepts to different datastores.

**QueryDslPredicateExecutor<T>** : 
- It is not a `repository interface`. 
- It declares the methods that are used to retrieve entities from the database by using QueryDsl Predicate objects.


###  Spring Data JPA
This project provides the following interfaces:

**JpaRepository<T, ID extends Serializable>**  : 
- This interface is a JPA specific repository interface that combines the methods declared by the common repository interfaces behind a single interface.
- The JpaRepository adds JPA-specific methods, like flush() to trigger a flush on the persistence context or `findAll(Example<S> example)` to find entities by example, to the PagingAndSortingRepository.

**JpaSpecificationExecutor<T>** : 
- This is again not a repository interface. 
- It declares the methods that are used to retrieve entities from the database by using `Specification<T>` objects that use the JPA criteria API.

The repository hierarchy looks as follows:

<img src="images/JpaRepositoryUml.png" width="1000" />






---

## More Details: 
1. [What is Spring Data JPA? And why should you use it?](https://thorben-janssen.com/what-is-spring-data-jpa-and-why-should-you-use-it/)