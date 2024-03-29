---
layout: default
title: Java 8
parent: Java
resource: true
desc: "Java 8 interview questions and answers."
categories: [Java 8]
---

# Java 8
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
 

## Java 8 New features

- Lambda expressions: These allow you to create anonymous functions, which can be passed as arguments to methods or stored in variables.

- Streams: These provide a way to process data in a declarative manner, allowing you to perform operations on collections of data in a more functional style.

- Functional interfaces: These are interfaces that have a single abstract method, which can be used in combination with lambda expressions to create more concise and expressive code.

- Default methods: These allow interfaces to have code implemented in them, which can be inherited by classes that implement the interface.

- Optional class: This is a container class that is used to represent optional values, which can help prevent NullPointerExceptions.

- Date and time API (java.time): This new API replaces the java.util.Date class and provides a more comprehensive set of classes for working with dates and times.

- Nashorn JavaScript engine: This is a new JavaScript engine that allows you to execute JavaScript code from within a Java application.


- **Lambda Expressions** − a new language feature allowing treating actions as objects •Method References − enable
  defining Lambda Expressions by referring to methods directly using their names
- **Optional** − This class is to provide a type-level solution for representing optional values instead of using null
  references.
- **Functional Interface** – an interface with maximum one abstract method, implementation can be provided using a
  Lambda Expression
- **Default methods** − give us the ability to add full implementations in interfaces besides abstract methods
- **Nashorn, JavaScript Engine** − Java-based engine for executing and evaluating JavaScript code
- **Stream API** − a special iterator class that allows processing collections of objects in a functional manner
- **Date and Time API** − an improved, immutable JodaTime-inspired Date API

---

## Lambda Expressions

A lambda expression is an unnamed block of code (or an unnamed function) with a list of formal parameters and a body.
Sometimes a lambda expression is simply called a lambda. The body of a lambda expression can be a block statement or an
expression. An arrow (->) is used to separate the list of parameters and the body.

###  Examples of lambda expressions

Takes an int parameter and returns the parameter value incremented by 1

> (int x) -> x + 1

Takes two int parameters and returns their sum

> (int x, int y) -> x + y

Takes two int parameters and returns the maximum of the two

> (int x, int y) -> { int max = x > y ? x : y;
> return max;
> }

Takes no parameters and returns void

> () -> { }

Takes no parameters and returns a string "OK"

> () -> "OK"

Takes a String parameter and prints it on the standard output

> (String msg) -> { System.out.println(msg); }

Takes a parameter and prints it on the standard output

> msg -> System.out.println(msg)

Takes a String parameter and returns its length

> (String str) -> str.length()

```java
@FunctionalInterface
interface StringToIntMapper {
    int map(String str);
}

    StringToIntMapper mapper = (String str) -> str.length();

    String name = "Kristy";
    int mappedValue = mapper.map(name);
System.out.println("name="+name+", mapped value="+mappedValue);
```

Output:

```log
name=Kristy, mapped value=6
```

The following snippet of code uses an anonymous class to achieve the same result as the lambda expression used in the
previous example:

```java
StringToIntMapper mapper=new StringToIntMapper(){
@Override
public int map(String str){
        return str.length();
        }
        };

        String name="Kristy";
        int mappedValue=mapper.map(name);
        System.out.println("name="+name+", mapped value="+mappedValue);
```

Output:

```log
name=Kristy, mapped value=6
```

- Lambda Expression facilitates functional programming and simplifies the development a lot.
- It provides a clear and concise way to represent one method interface using an expression. It is very useful in the
  collection library. It helps to iterate, filter, and extract data from the collection.
- The Lambda expression is used to provide the implementation of an interface that has a functional interface. It saves
  a lot of code. In the case of the lambda expression, we don't need to define the method again for providing the
  implementation. Here, we just write the implementation code.
- Java lambda expression is treated as a function, so the compiler does not create a `.class` file.
- Lambda expressions have three parts: a list of parameters, and arrow, and a
  body: `(Object o) -> System.out.println(o)`;
- You can think of lambda expressions as anonymous methods (or functions) as they don't have a name.
- A lambda expression can have zero (represented by empty parentheses), one or more parameters.
- The type of the parameters can be declared explicitly, or it can be inferred from the context.
- If there is a single parameter, the type is inferred, and is not mandatory to use parentheses.
- If the lambda expression uses as a parameter name which is the same as a variable name of the enclosing context, a compile error is generated.
- If the body has one statement, curly brackets are not required, and the value of the expression (if any) is returned.
- If the body has more than one statement, curly brackets are required, and if the expression returns a value, it must
  return with a return statement.
- If the lambda expression doesn't return a result, a return statement is optional.
- The signature of the abstract method of a functional interface provides the signature of a lambda expression.
- In order to use a lambda expression, you first need a functional interface.
- However, lambda expressions don't contain the information about which functional interface are implementing.
- The type of the expression is deduced from the context in which the lambda is used. This type is called a target type.
- The contexts where the target type of a lambda expression can be inferred include an assignment, method or constructor
  arguments, and a cast expression.
- Default methods of a functional interface cannot be accessed from within lambda expressions.

### Why use Lambda Expression


- To provide the implementation of the Java 8 Functional Interface.
- Less coding.
- Lambda Expressions enable you to encapsulate a single unit of behavior and pass it to other code. You can use lambda
  expressions if you want a certain action performed on each element of a collection, when a process is completed, or
  when a process encounters an error.

### Lambda Expressions Syntax


Java Lambda Expression Syntax

```java
(argument-list)->{body}
```

Java lambda expression consists of three components.

- **Argument-list**: It can be empty or non-empty as well.
- **Arrow-token**: It is used to link arguments-list and body of expression.
- **Body:** It contains expressions and statements for the lambda expression.

A lambda expression consists of a list of parameters and a body separated by an arrow (->). The list of parameters is
declared the same way as the list of parameters for methods. The list of parameters is enclosed in parentheses, as is
done for methods. The body of a lambda expression is a block of code enclosed in braces. Like a method’s body, the body
of a lambda expression may declare local variables; use statements including break, continue, and return; throw
exceptions, etc. Unlike a method, a lambda expression does not have the following four parts:

• A lambda expression does not have a name. • A lambda expression does not have a return type. It is inferred by the
compiler from the context of its use and from its body. • A lambda expression does not have a throws clause. It is
inferred from the context of its use and its body. • A lambda expression cannot declare type parameters. That is, a
lambda expression cannot be generic.

Examples of Lambda Expressions and Equivalent Methods

### Java Lambda Expression Syntax 

- Generic Java Lambda Expression Syntax `(argument-list) -> {body} `
- Java Lambda Expression with No Parameter: `() -> { Systen.out.printIn("Lamda Expression"); };`
- Java Lambda Expression with Single Parameter `(msg) -> system.om.printin(msg); } `
- Java Lambda Expression with Multiple Parameters: `(int a,int b) -> (a+b);`
- Java Lambda Expression without return keyword: `(a, b) -> (a + b); `
- Java Lambda Expression with Multiple Statements:

```java
(x,r) -> {
        Systen.out.println("x: ":+x);
        Systen.out.printIn("Y :"+y);
        return(x+y);
        };
```


---

## Stream  

Java provides a new additional package in Java 8 called `java.util.stream`. This package consists of classes,
interfaces, and an enum to allows functional-style operations on the elements. You can use stream by importing
java.util.stream package in your programs.

###  Stream features


- Stream does not store elements. It simply conveys elements from a source such as a data structure, an array, or an I/O
  channel, through a pipeline of computational operations.
- Stream is functional in nature. Operations performed on a stream does not modify its source. For example, filtering a
  Stream obtained from a collection produces a new Stream without the filtered elements, rather than removing elements
  from the source collection.
- Stream is lazy and evaluates code only when required.
- The elements of a stream are only visited once during the life of a stream. Like an Iterator, a new stream must be
  generated to revisit the same elements of the source.

You can use Stream to filter, collect, print, and convert from one data structure to other etc.


---



## Parallel Streams

The Stream API enables developers to create the parallel streams that can take advantage of multi-core architectures and enhance the performance of Java code. In a parallel stream, the operations are executed in parallel and there are two ways to create a parallel stream.

- Using the parallelStream() method on a collection
- Using the parallel() method on a stream

Do remember, Parallel Streams must be used only with stateless, non-interfering, and associative operations i.e.

- **A stateless** operation is an operation in which the state of one element does not affect another element
- **A non-interfering** operation is an operation in which data source is not affected
- **An associative** operation is an operation in which the result is not affected by the order of operands


Let’s take a scenario where you have a list of employee objects and you have to count the employees whose salary is above 15000. Generally, to solve this problem you will iterate over list going through each employee and checking if employee’s salary is above 15000. This takes O(N) time since you go sequentially.

Streams give us the flexibility to iterate over the list in a parallel pattern and can give the total in quick fashion. Stream implementation in Java is by default sequential unless until it is explicitly mentioned in parallel. When a stream executes in parallel, the Java runtime partitions the stream into multiple sub-streams. Aggregate operations iterate over and process these sub-streams in parallel and then combine the results.

The only thing to keep in mind to create parallel stream is to call the parallelStream() method on the collection else by default the sequential stream gets returned by stream() method.

###  Parallel Streams Performance Implications

Parallel Stream has equal performance impacts as like its advantages.

- Since each sub-stream is a single thread running and acting on the data, it has overhead compared to the sequential stream
- Inter-thread communication is dangerous and takes time for coordination

###  When to use Parallel Streams?

- They should be used when the output of the operation is not needed to be dependent on the order of elements present in source collection (i.e. on which the stream is created)
- Parallel Streams can be used in case of aggregate functions
- Parallel Streams quickly iterate over the large-sized collections
- Parallel Streams can be used if developers have performance implications with the Sequential Streams
- If the environment is not multi-threaded, then Parallel Stream creates thread and can affect the new requests coming in
- You have a large dataset to process.
- As you know that Java uses ForkJoinPool to achieve parallelism, ForkJoinPool forks sources stream and submit for execution, so your source stream should be splittable.  
   For example:
  ArrayList is very easy to split, as we can find a middle element by its index and split it but LinkedList is very hard to split and does not perform very well in most of the cases.
- You are actually suffering from performance issues.
- You need to make sure that all the shared resources between threads need to be synchronized properly otherwise it might produce unexpected results.

```java

import java.util.ArrayList;
import java.util.List;

public class ParallelStreamDemo {

  public static void main(String[] args) {

    long t1, t2;
    List<Employee> eList = new ArrayList<Employee>();
    for(int i=0; i<100; i++) {
      eList.add(new Employee("A", 20000));
      eList.add(new Employee("B", 3000));
      eList.add(new Employee("C", 15002));
      eList.add(new Employee("D", 7856));
      eList.add(new Employee("E", 200));
      eList.add(new Employee("F", 50000));
    }

    /***** Here We Are Creating A 'Sequential Stream' & Displaying The Result *****/
    t1 = System.currentTimeMillis();
    System.out.println("Sequential Stream Count?= " + eList.stream().filter(e -> e.getSalary() > 15000).count());

    t2 = System.currentTimeMillis();
    System.out.println("Sequential Stream Time Taken?= " + (t2-t1) + "\n");

    /***** Here We Are Creating A 'Parallel Stream' & Displaying The Result *****/
    t1 = System.currentTimeMillis();
    System.out.println("Parallel Stream Count?= " + eList.parallelStream().filter(e -> e.getSalary() > 15000).count());

    t2 = System.currentTimeMillis();
    System.out.println("Parallel Stream Time Taken?= " + (t2-t1));
  }
}
```

The application shows the following logs as output where creating a Sequential Stream and filtering elements took 178 ms, whereas Parallel Stream only took 15 ms.

```log
# Logs for 'SEQUENTIAL STREAM' #
=============================
Sequential Stream Count?= 300
Sequential Stream Time Taken?= 178
 
# Logs for 'PARALLEL STREAM' #
===========================
Parallel Stream Count?= 300
Parallel Stream Time Taken?= 15 
```

---

## Fork-Join Framework

Parallel streams make use of the fork-join framework and its common pool of worker threads.

The fork-join framework was added to java.util.concurrent in Java 7 to handle task management between multiple threads.

The fork-join framework is in charge of splitting the source data between worker threads and handling callback on task completion.

Let's take a look at an example of calculating a sum of integers in parallel.

We'll make use of the reduce method and add five to the starting sum, instead of starting from zero:

```java
List<Integer> listOfNumbers = Arrays.asList(1, 2, 3, 4);
int sum = listOfNumbers.parallelStream().reduce(5, Integer::sum);
assertThat(sum).isNotEqualTo(15);

```

In a sequential stream, the result of this operation would be 15.

But since the reduce operation is handled in parallel, the number five actually gets added up in every worker thread:

The actual result might differ depending on the number of threads used in the common fork-join pool.

In order to fix this issue, the number five should be added outside of the parallel stream:

```java
List<Integer> listOfNumbers = Arrays.asList(1, 2, 3, 4);
        int sum = listOfNumbers.parallelStream().reduce(0, Integer::sum) + 5;
        assertThat(sum).isEqualTo(15);
```

Therefore, we need to be careful about which operations can be run in parallel.



---


## Intermediate and Terminal operations

 <img src="images/intermediate%20and%20terminal%20operations.png" width="1000" />

### Intermediate vs Terminal operations

- Intermediate operation is lazy while a terminal operation is not. 

- When you invoke an intermediate operation on a stream, the operation is not executed immediately. It is executed only when a terminal operation is invoked on that stream. In a way, an intermediate operation is memorized and is recalled as soon as a terminal operation is invoked. 

- You can chain multiple intermediate operations and none of them will do anything until you invoke a terminal operation. At that time, all of the intermediate operations that you invoked earlier will be invoked along with the terminal operation.

- All intermediate operations return Stream (can be chained), while terminal operations don't.

### Intermediate Operations
- filter(Predicate<T>)
- map(Function<T>)
- flatMap(Function<T>)
- sorted(Comparator<T>)
- peek(Consumer<T>)
- distinct()
- limit(long n)
- skip(long n)

### Terminal Operations
- forEach
- forEachOrdered
- toArray
- reduce
- collect
- min
- max
- count
- anyMatch
- allMatch
- noneMatch
- findFirst    
- findAny

---

## Functional Interface

functional interface is an interface that has a single abstract method. These types of interfaces are used to represent functions as objects, and they can be used with lambda expressions and method references to create concise, functional-style code.

```java
@FunctionalInterface
public interface Converter<F, T> {
T convert(F from);
}
```

This interface has a single abstract method, convert, which takes an argument of type F and returns a value of type T. The @FunctionalInterface annotation is optional, but it is recommended to use it as it helps the compiler to ensure that the interface is indeed a functional interface and can be used with lambda expressions.

Here is an example of how you could use this functional interface with a lambda expression:
```java
Converter<String, Integer> converter = (from) -> Integer.valueOf(from);
Integer converted = converter.convert("123");
System.out.println(converted);  // 123
```

In this example, the lambda expression (from) -> Integer.valueOf(from) implements the convert method of the Converter interface. This allows you to pass the lambda expression as an argument to a method that expects a Converter.


- An Interface that contains exactly one abstract method is known as a functional interface.
- It can have any number of `default`, `static` methods but can contain only one abstract method. It can also declare
  methods of the object class.
- Functional Interface is also known as Single Abstract Method Interfaces or SAM Interfaces. It is a new feature in Java
  8, which helps to achieve a functional programming approach.
- A functional interface can extend another interface only when it does not have any abstract method.
- The Java API has many one-method interfaces such as `Runnable`, `Callable`, `Comparator`, `ActionListener`, and
  others. They can be implemented and instantiated using anonymous class syntax.
- A functional interface is an interface that has exactly one abstract method.
- Since default methods have an implementation, they are not abstract so a functional interface can have any number of
  them.
- If an interface declares an abstract method with the signature of one of the methods of java.lang.Object, it doesn't
  count toward the functional interface method count.
- A functional interface is valid when it inherits a method that is equivalent but not identical to another.
- An empty interface is not considered a functional interface.
- A functional interface is valid even if the @FunctionalInterface annotation would be omitted.
- Functional interfaces are the basis of lambda expressions

### Custom Functional Interface


```java
@FunctionalInterface
interface Sayable{
    void say(String msg);   // abstract method   
}
```

```java
public class FunctionalInterfacesExample {

    public static void main(String[] args) {

        Sayable sayable = (msg) -> {
            System.out.println(msg);
        };
        sayable.say("Say something ..");
    }
}
```


---

### Predefined Functional Interfaces


Java 8 provides predefined functional interfaces to deal with functional programming by using lambda and method
references.

```java
@Setter
@Getter
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        super();
        this.name = name;
        this.age = age;
    }
}
```

#### Predicate


We need a function for checking a condition. A Predicate is one such function accepting a single argument to evaluate to
a boolean result. It has a single method test that returns the boolean value.

Internal implementation of the Predicate interface: Predicate interface contains exactly one abstract method test(T t).
Note that it also contains a default, static methods.

```java
@FunctionalInterface
public interface Predicate<T> {

    /**
     * Evaluates this predicate on the given argument.
     *
     * @param t the input argument
     * @return {@code true} if the input argument matches the predicate,
     * otherwise {@code false}
     */
    boolean test(T t);

    default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) && other.test(t);
    }

    default Predicate<T> negate() {
        return (t) -> !test(t);
    }

    default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) || other.test(t);
    }

   static <T> Predicate<T> isEqual(Object targetRef) {
        return (null == targetRef)
                ? Objects::isNull
                : object -> targetRef.equals(object);
    }
}
```

Example :

```java
public class PredicateExample {
    public static void main(String[] args) {
        Predicate<Person> predicate = (person) -> person.getAge() > 28;
        boolean result = predicate.test(new Person("James", 29));
        System.out.println(result);
    }
}
```

#### Function


It represents a function that accepts one argument and returns a result.

The function interface contains exactly one abstract method apply(T t). Note that it also contains a default, static
methods.

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);

    default <V> Function<V, R> compose(Function<? super V, ? extends T> before) {
        Objects.requireNonNull(before);
        return (V v) -> apply(before.apply(v));
    }

    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
        Objects.requireNonNull(after);
        return (T t) -> after.apply(apply(t));
    }

   
    static <T> Function<T, T> identity() {
        return t -> t;
    }
}
```

Example :

```java
import java.util.function.Function;

public class FunctionExample {

    public static void main(String[] args) {
        // convert centigrade to fahrenheit
        Function < Integer, Double > centigradeToFahrenheitInt = x -> new Double((x * 9 / 5) + 32);

        // String to an integer
        Function < String, Integer > stringToInt = x -> Integer.valueOf(x);
        System.out.println(" String to Int: " + stringToInt.apply("4"));


        Function < PersonEntity, PersonDTO > function = (entity) -> {
            return new PersonDTO(entity.getName(), entity.getAge());
        };
        PersonDTO personDTO = function.apply(new PersonEntity("James", 20));
        System.out.println(personDTO.getName());
        System.out.println(personDTO.getAge());
    }
}

class PersonEntity {
    private String name;
    private int age;

    public PersonEntity(String name, int age) {
        super();
        this.name = name;
        this.age = age;
    }
}

class PersonDTO {
    private String name;
    private int age;

    public PersonDTO(String name, int age) {
        super();
        this.name = name;
        this.age = age;
    }
}
```

#### Supplier


Represents a supplier of results.

Internal implementation of the Supplier interface. The supplier interface contains exactly one abstract method get(T t).
Hence we can apply lambda expression to it.

```java
@FunctionalInterface
public interface Supplier<T> {

    /**
     * Gets a result.
     *
     * @return a result
     */
    T get();
}
```

Example :

```java
import java.util.function.Supplier;

public class SuppliersExample {

   public static void main(String[] args) {
  
       Supplier<Person> supplier = () -> {
           return new Person("John", 30);
       };

       Person p = supplier.get();
       System.out.println("Person Detail:\n" + p.getName() + ", " + p.getAge());
   }
}
```

#### Consumer


It represents an operation that accepts a single argument and returns no result. Internal implementation of the Consumer
interface. The consumer interface contains exactly one abstract method accept(T arg0). Hence we can apply lambda
expression to it.

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T arg0);

    default Consumer<T> andThen(Consumer<? super T> arg0) {
       Objects.requireNonNull(arg0);
       return (arg1) -> {
       this.accept(arg1);
       arg0.accept(arg1);
    };
  }
}
```

Example :

```java
public class ConsumersExample {

    public static void main(String[] args) {
        List<Person> listOfPerson = new ArrayList<Person>();
        listOfPerson.add(new Person("abc", 27));
        listOfPerson.add(new Person("mno", 26));
        listOfPerson.add(new Person("pqr", 28));
        listOfPerson.add(new Person("xyz", 27));

        listOfPerson.forEach((person) -> {
            System.out.println(" Person name : " + person.getName());
            System.out.println(" Person age : " + person.getAge());
        });
  
  
        // Second example
        Consumer<Person> consumer = (person) -> {
           System.out.println(person.getName());
           System.out.println(person.getAge());
        };
        consumer.accept(new Person("John", 30));
    }
}
```

#### BiFunction


To define lambdas with two arguments, we have to use additional interfaces that contain "Bi" keyword in their names: BiFunction, ToDoubleBiFunction, ToIntBiFunction, and ToLongBiFunction.
BiFunction implementation that receives a key and an old value to calculate a new value for the salary and return it.

It represents a function that accepts two arguments and returns a result.
internal implementation of BiFunction interface. BiFunction interface contains exactly one abstract method apply(T arg0, U arg1). Hence we can apply lambda expression to it.

```java
@FunctionalInterface
public interface BiFunction<T, U, R> {
 R apply(T arg0, U arg1);

 default <V> BiFunction<T, U, V> andThen(Function<? super R, ? extends V> arg0) {
  Objects.requireNonNull(arg0);
  return (arg1, arg2) -> {
   return arg0.apply(this.apply(arg1, arg2));
  };
 }
}
```

Example :

```java
public class BiFunctionExample {

    public static void main(String[] args) {
  
       BiFunction<Person, Person, Integer> biFunction = (p1,p2) -> {
           return p1.getAge() + p2.getAge();
       };

        int totalAge = biFunction.apply(new Person("John", 10),
                new Person("James", 10));
        System.out.println(totalAge);

    }
}
```

#### BiConsumer


It represents an operation that accepts two input arguments and returns no result. Internal implementation of BiConsumer
interface. BiConsumer interface contains exactly one abstract method accept(T arg0, U arg1). Hence we can apply lambda
expression to it.

```java
@FunctionalInterface
public interface BiConsumer<T, U> {
    void accept(T arg0, U arg1);

    default BiConsumer<T, U> andThen(BiConsumer<? super T, ? super U> arg0) {
        Objects.requireNonNull(arg0);
        return (arg1, arg2) -> {
             this.accept(arg1, arg2);
            arg0.accept(arg1, arg2);
        };
     }
}
```

Example :

```java
public class BiConsumersExample {

    public static void main(String[] args) {
  
        BiConsumer<Person, Person> biConsumer = (p1, p2) -> {
             System.out.println(" print first persion");
             System.out.println(p1.getName());
             System.out.println(" print second persion");
             System.out.println(p2.getName());
       };
  
       biConsumer.accept(new Person("John", 10), new Person("James", 10));
    }
}
```

You can also define your own custom functional interface. Following is the list of a functional interface that is placed in java.util.function package.

---

## Method References


Method reference is used to refer method of the functional interface. It is a compact and easy form of a lambda expression. Each time when you are using a lambda expression to just referring a method, you can replace your lambda expression with method reference.

### Method References Types

- Reference to a static method : `ContainingClass::staticMethodName`
- Reference to an instance method of a particular object : `containingObject::instanceMethodName`
- Reference to an instance method of an arbitrary object of a particular type : `ContainingType::methodName`
- Reference to a constructor: `ClassName::new`


---

##  Stream map() vs flatMap()

Both `map` and `flatMap` can be applied to a `Stream<T>` and they both return a `Stream<R>`. The difference is that the `map` operation produces one output value for each input value, whereas the `flatMap` operation produces an arbitrary number (zero or more) values for each input value.

###  Stream.map()

The map operation takes a Function, which is called for each value in the input stream and produces one result value, which is sent to the output stream.

###  Stream.flatMap()

The flatMap operation takes a function that conceptually wants to consume one value and produce an arbitrary number of values.

Typical use is for the mapper function of flatMap to return Stream.empty() if it wants to send zero values, or something like Stream.of(a, b, c) if it wants to return several values. But of course any stream can be returned.



| map() | flatMap()                                                                                                                                                                             |
|---|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Stream.map only applies a function to the stream without flattening the stream.  | Stream.flatMap, as it can be guessed by its name, is the combination of a map and a flat operation. That means that you first apply a function to your elements, and then flatten it. |
| The function you pass to the map() operation returns a single value.  | The function you pass to flatMap() operation returns a Stream of value.                                                                                                               |
| map() is used for transformation only  |   flatMap() is used for both transformation and flattening.                                                                                                                                                                                     |


### map() example

```java
class MapExammple {
  public static void main(String[] args) {
    List<String> listOfStrings = Arrays.asList("1", "2", "3", "4", "5");
      List<Integer> listOfIntegers = listOfStrings.stream()
            .map(Integer::valueOf)
            .collect(Collectors.toList());
    System.out.println(listOfIntegers);   //[1, 2, 3, 4, 5]
  }
}
```


### flatMap() example
flatMap() is two step process i.e. map() + Flattening. It helps in converting `Collection<Collection<T>>` to `Collection<T>`

```java
 class MapExammple {
  public static void main(String[] args) {
    List<Integer> list1 = Arrays.asList(1,2,3);
    List<Integer> list2 = Arrays.asList(4,5,6);
    List<Integer> list3 = Arrays.asList(7,8,9);

    List<List<Integer>> listOfLists = Arrays.asList(list1, list2, list3);

    List<Integer> listOfAllIntegers = listOfLists.stream()
            .flatMap(x -> x.stream())
            .collect(Collectors.toList());

    System.out.println(listOfAllIntegers);    //[1, 2, 3, 4, 5, 6, 7, 8, 9]
  }
}
```



---

## For more information

1. [Java 8 Lambda Expressions](https://www.javaguides.net/2018/07/java-8-lambda-expressions.html)
2. [Java 8 Parallel Streams Example](https://examples.javacodegeeks.com/core-java/java-8-parallel-streams-example/)
3. [When to Use a Parallel Stream in Java](https://www.baeldung.com/java-when-to-use-parallel-stream)
4. [The Difference Between map() and flatMap()](https://www.baeldung.com/java-difference-map-and-flatmap)
5. [What's the difference between map() and flatMap() methods in Java 8?](https://stackoverflow.com/questions/26684562/whats-the-difference-between-map-and-flatmap-methods-in-java-8)
6. 

