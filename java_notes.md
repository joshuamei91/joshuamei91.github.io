---
layout: page
title: System Design
permalink: /java/
---

- [How to do deep copy](https://www.baeldung.com/java-deep-copy)
  - Implement copy constructor 
    ``` java
    public Address(Address that) {
      this(that.getStreet(), that.getCity(), that.getCountry());
    }

    public User(User that) {
      this(that.getFirstName(), that.getLastName(), new Address(that.getAddress()));
    }
    ```
  - Serialise to JSON then deserialize to new object
    ``` java
    Address address = new Address("Downing St 10", "London", "England");
    User pm = new User("Prime", "Minister", address);
    Gson gson = new Gson();
    User deepCopy = gson.fromJson(gson.toJson(pm), User.class);
    ```

- [try-with-resouces](https://www.baeldung.com/java-try-with-resources): Declare resources to be used in a try block with the assurance that the resources will be closed after the execution of that block.
  ``` java
  try (PrintWriter writer = new PrintWriter(new File("test.txt"))) {
      writer.println("Hello World");
  }
  ```

- [Disambiguate which beans to inject](https://www.baeldung.com/spring-qualifier-annotation)
  Use the `@Qualifier` or `@Primary` annotation

- [Override equals() and hashCode()](https://www.baeldung.com/java-equals-hashcode-contracts) to compare equality in values between objects. Use `@EqualsAndHashCode` from `Lombok` or let IDE generate the methods.

- What are classes?
  > A class is a user defined blueprint or prototype from which objects are created.  It represents the set of properties or methods that are common to all objects of one type.

- [Difference between method overloading and method overriding](https://www.geeksforgeeks.org/difference-between-method-overloading-and-method-overriding-in-java/)
  > In method overloading, more than one method shares the same method name with different signature in the class. In method overloading, return type can or can not be be same.

  > In method overriding, derived class provides the specific implementation of the method that is already provided by the base class or parent class.

- [Inheritance](https://www.geeksforgeeks.org/inheritance-in-java/)
  - Single inheritance (A -> B)
  - Mulitlevel inheritance (A -> B -> C)
  - Hierarchical Inheritance (A -> B, A -> C)
  - Multiple Inheritance (Through Interfaces)

  - [SOLID](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)
    - Single Responsibility Principle
    - Open-Closed Principle (Objects or entities should be open for extension but closed for modification)
    - Liskov Substitution Principle (This means that every subclass or derived class should be substitutable for their base or parent class)
    - Interface Segregation Principle (A client should never be forced to implement an interface that it doesn’t use, or clients shouldn’t be forced to depend on methods they do not use)
    - Dependency Inversion Principle (Entities must depend on abstractions, not on concretions. It states that the high-level module must not depend on the low-level module, but they should depend on abstractions.) This principle allows for decoupling.