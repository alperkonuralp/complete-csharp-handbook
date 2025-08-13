# 📚 **Complete C# Handbook**

## **Chapter 1 – Getting Started** 📖 [Read Chapter](chapters/01-getting-started.md)

1. **Introduction and Development Environment**

   * What is C# and where is it used?
   * Overview of the .NET ecosystem
   * Development environment setup (Visual Studio / VS Code)
   * Creating our first C# project ("Hello World")
   * Program flow and execution logic
   * **Practical:** First console application

   * **Try It Yourself:**

     1. Open and run a "Hello World" project in Visual Studio.
     2. Write an application that prints your name to the console.
   * **Reference Note:** *(See Appendix A: C# Version Features)*

2. **Fundamental Programming Concepts**

   * Variables and data types (int, string, bool, etc.)
   * Operators (+, -, \*, /, %, &&, ||, !, etc.)
   * Type conversions (`Convert`, `Parse`, `TryParse`)
   * **Practical:** Simple calculator

   * **Try It Yourself:**

     1. Get two numbers from the user and print addition and multiplication results.
     2. Create an example that converts between different data types.
   * **Reference Note:** *(See Appendix B: Data Types and Memory Sizes)*

---

## **Chapter 2 – Decision Structures and Loops** 📖 [Read Chapter](chapters/02-decision-structures-and-loops.md)

1. **Conditional Statements**

   * `if`, `else if`, `else`
   * `switch-case`
   * Flow control with decision structures
   * **Practical:** Pass/fail calculator based on grade average

2. **Loops**

   * `for`, `while`, `do-while`
   * Iterating over collections with `foreach`
   * Loop control keywords (`break`, `continue`)
   * **Practical:** Creating multiplication tables

* **Try It Yourself:**

  1. Print "Passed" or "Failed" based on user input grade.
  2. Find the sum of numbers from 1 to 100 using a `for` loop.
  3. Print names in an array using `foreach`.

---

## **Chapter 3 – Arrays and Collections** 📖 [Read Chapter](chapters/03-arrays-and-collections.md)

1. **Arrays**

   * Single-dimensional arrays
   * Multi-dimensional arrays
   * Array methods (`Length`, `Sort`, `Reverse`)
   * **Practical:** Sorting and searching operations

2. **List and Other Collections**

   * Using `List<T>`
   * `Dictionary<TKey, TValue>`
   * `Queue`, `Stack`
   * **Practical:** Student list management

* **Try It Yourself:**

  1. Create a 10-element array, get numbers from user and find the average.
  2. Create a shopping list application using `List<string>`.
  3. Create student-number mapping using `Dictionary`.

---

## **Chapter 4 – Methods and Parameters** 📖 [Read Chapter](chapters/04-methods-and-parameters.md)

1. **Method Definition and Usage**

   * Return types and parameters
   * `ref`, `out`, `in` keywords
   * Default parameters
   * **Practical:** Bank interest calculation method

2. **Functional Features**

   * Lambda expressions
   * Local functions
   * Expression-bodied methods
   * **Practical:** Simple filtering function

* **Try It Yourself:**

  1. Write a method that returns the product of two numbers.
  2. Write a method that swaps two numbers using `ref`.
  3. Create a discount calculation application with default parameters.

---

## **Chapter 5 – Object-Oriented Programming (OOP)** 📖 [Read Chapter](chapters/05-object-oriented-programming.md)

1. **Classes and Objects**

   * Class definition and object creation
   * Fields and properties
   * Constructor methods
   * **Practical:** Product class for inventory tracking

2. **Encapsulation and Access Modifiers**

   * `public`, `private`, `protected`, `internal`
   * Getter/Setter logic
   * **Practical:** User management system

3. **Inheritance and Polymorphism**

   * `base` keyword
   * Virtual and override methods
   * **Practical:** Vehicle class hierarchy

4. **Abstraction and Interfaces**

   * Abstract classes
   * Interface usage
   * **Practical:** Payment methods design

* **Try It Yourself:**

  1. Create a `Student` class and store name, number information.
  2. Create inheritance example with `Vehicle` class and `Car` subclass.
  3. Implement `IPayment` and `IShipping` interfaces.

---

## **Chapter 6 – Advanced Language Features** 📖 [Read Chapter](chapters/06-advanced-language-features.md)

1. **Generics (Type-Parameterized Structures)**

   * Generic classes and methods
   * **Practical:** Type-safe data store

2. **Data Querying with LINQ**

   * Basic LINQ queries
   * Filtering, sorting, grouping
   * **Practical:** Student list queries

3. **Delegates and Events**

   * Delegate definition and usage
   * Event triggering
   * **Practical:** Notification system

4. **Extension Methods**

   * Adding new methods to existing classes
   * **Practical:** String abbreviation method

* **Try It Yourself:**

  1. Filter even numbers from `List<int>` using LINQ.
  2. Create a simple event mechanism (e.g., show message when user logs in).
  3. Create an extension method for `string` to capitalize the first letter.

---

## **Chapter 7 – Asynchronous and Parallel Programming** 📖 [Read Chapter](chapters/07-asynchronous-and-parallel-programming.md)

1. **Asynchronous Operations with Async/Await**

   * Task structure
   * Async methods
   * **Practical:** API data fetching simulation

2. **Parallel Processing**

   * `Parallel.For` and `Parallel.ForEach`
   * Using PLINQ
   * **Practical:** Large data list processing

* **Try It Yourself:**

  1. Print a message to screen after 2-second delay using async method.
  2. Calculate sum of numbers from 1 to 1,000,000 using `Parallel.For`.

---

## **Chapter 8 – File and Data Operations** 📖 [Read Chapter](chapters/08-file-and-data-operations.md)

1. **File Reading/Writing**

   * `File`, `Stream`, `StreamReader`, `StreamWriter`
   * **Practical:** Log file creation

2. **Working with JSON and XML**

   * Using `System.Text.Json`
   * **Practical:** Configuration file management

* **Try It Yourself:**

  1. Get text from user and save to `log.txt` file.
  2. Create and read a configuration file in JSON format.

---

## **Chapter 9 – Database Operations** 📖 [Read Chapter](chapters/09-database-operations.md)

1. **Entity Framework Core Fundamentals**

   * DbContext and Entities
   * Migration management
   * **Practical:** Product database application

2. **LINQ to Entities**

   * Data insertion, updating, deletion
   * **Practical:** CRUD operations

* **Try It Yourself:**

  1. Create `Product` table using Entity Framework and add data.
  2. List products with price greater than 100 using LINQ.

---

## **Chapter 10 – Web Applications** 📖 [Read Chapter](chapters/10-web-applications.md)

1. **ASP.NET Core MVC Fundamentals**

   * Model, View, Controller structure
   * Routing logic
   * **Practical:** Simple blog application

2. **Web API Development**

   * REST architecture
   * Controller and Endpoint development
   * **Practical:** Product management with API

* **Try It Yourself:**

  1. Create a "ToDo List" application using ASP.NET Core MVC.
  2. Implement product CRUD operations with Web API.

---

## **Chapter 11 – Test Development** 📖 [Read Chapter](chapters/11-test-development.md)

1. **Unit Testing Logic**

   * Using xUnit
   * **Practical:** Bank interest calculation tests

2. **Mocking**

   * Testing with Moq library
   * **Practical:** Mocking API dependencies

* **Try It Yourself:**

  1. Write unit tests for bank interest calculation method.
  2. Create tests by mocking a service with Moq.

---

## **Chapter 12 – Real-World Project** 📖 [Read Chapter](chapters/12-real-world-project.md)

* Full project development with layered architecture
* API + MVC + Database integration
* Validation with unit tests
* **Practical:** E-commerce mini system

* **Practical Project:**

  * Layered architecture
  * API + MVC + Database
  * Unit tests
  * **Try It Yourself:** E-commerce mini system

---

## 📖 **Appendices – Reference Section**

* **Appendix A:** [C# Version Features Table](chapters/appendices/appendix-a-csharp-version-features.md)
* **Appendix B:** [Data Types and Memory Sizes](chapters/appendices/appendix-b-data-types-and-memory-sizes.md) (short, int, long, float, double, decimal, bool, char, string)
* **Appendix C:** [Operators Table](chapters/appendices/appendix-c-operators-table.md)
* **Appendix D:** [Access Modifiers Table](chapters/appendices/appendix-d-access-modifiers-table.md) (public, private, protected, internal)
* **Appendix E:** [Collections Comparison Table](chapters/appendices/appendix-e-collections-comparison-table.md) (List, Dictionary, Queue, Stack)
* **Appendix F:** [LINQ Methods Reference](chapters/appendices/appendix-f-linq-methods-reference.md)
* **Appendix G:** [Async/Await Usage Examples](chapters/appendices/appendix-g-async-await-usage-examples.md)
* **Appendix H:** [Entity Framework Core Migration Commands](chapters/appendices/appendix-h-entity-framework-core-migration-commands.md)
* **Appendix I:** [HTTP Status Codes Table](chapters/appendices/appendix-i-http-status-codes-table.md)
