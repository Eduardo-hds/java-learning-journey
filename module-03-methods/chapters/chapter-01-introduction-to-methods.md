# Chapter 01 — Introduction to Methods

## Overview

So far in the Bootcamp, every program you've written has been centered around a single method:

```java
public static void main(String[] args)
```

Even when your programs became more complex—with loops, conditions, and calculations—all of the logic lived inside `main()`.

This works for small programs, but as software grows, putting everything into one place quickly becomes difficult to read, understand, test, and maintain.

Methods solve this problem.

A method is a **named block of code that performs a specific task**. Instead of writing the same logic multiple times, you write it once inside a method and call it whenever you need it.

This idea is called **modular programming**—breaking a large problem into smaller, manageable pieces.

By the end of this module, writing methods will become as natural as writing `if` statements or `for` loops.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Explain what a method is.
* Understand why methods exist.
* Recognize the benefits of modular programming.
* Identify methods in a Java program.
* Understand the relationship between `main()` and other methods.

---

# What Is a Method?

A method is a reusable block of code designed to perform one specific task.

Think of it like a machine.

```
Input
   │
   ▼
+-----------+
|  Method   |
+-----------+
   │
   ▼
Output (optional)
```

For example:

```
Method: add()

Input:
5 and 8

Process:
5 + 8

Output:
13
```

Instead of rewriting the addition every time, you simply call the method.

---

# Real-World Analogy

Imagine a restaurant.

There are different employees, each with a specific responsibility.

```
Customer
    │
    ▼
Cashier
    │
    ▼
Kitchen
    │
    ▼
Cook
    │
    ▼
Meal Ready
```

The cashier doesn't cook.

The cook doesn't take payments.

Each person performs a single task.

Methods work the same way.

Instead of one enormous block doing everything, each method has one clear responsibility.

---

# Without Methods

Suppose a program prints a decorative title many times.

```text
====================
Java Calculator
====================
```

Without methods, you might repeatedly write:

```java
System.out.println("====================");
System.out.println("Java Calculator");
System.out.println("====================");
```

Every time the title is needed, the same three lines are copied again.

Problems:

* duplicated code;
* harder maintenance;
* greater chance of mistakes;
* longer programs.

---

# With Methods

Instead, create one method:

```java
printTitle();
```

Now, whenever the title is needed:

```java
printTitle();
```

The implementation exists only once.

If you later decide to change the title, you edit only one place.

---

# Why Methods Matter

Methods provide many advantages.

## 1. Code Reuse

Write once.

Use many times.

Instead of:

```java
// repeated code
```

You simply call the method.

---

## 2. Better Organization

Large programs become collections of small tasks.

Instead of reading hundreds of lines continuously, you read one logical step at a time.

Example:

```text
main()

├── showMenu()
├── readOption()
├── calculate()
└── printResult()
```

Even without seeing the implementation, the program is easy to understand.

---

## 3. Easier Maintenance

Suppose a calculation changes.

Without methods:

You might need to edit the same code in ten different places.

With methods:

You update only one method.

---

## 4. Easier Debugging

If something goes wrong, it's easier to identify which method contains the problem.

Instead of searching through an entire file, you inspect one small section.

---

## 5. Better Readability

Compare these two examples.

### Version A

```java
// 200 lines inside main()
```

Finding a specific part is difficult.

---

### Version B

```text
main()

showMenu()

readNumber()

calculateAverage()

printResult()
```

Even without opening each method, you already understand the overall flow.

---

# Every Java Program Already Uses a Method

Believe it or not, you've been using methods since Module 00.

```java
public static void main(String[] args)
```

This is a method.

Java starts executing your program by calling `main()`.

You can think of it like this:

```
Java
   │
   ▼
main()
```

The `main()` method is simply the entry point of every console application.

Later, you'll create additional methods that `main()` can call.

---

# A Program as a Team

Imagine your program as a company.

```
               main()
                  │
      ┌───────────┼───────────┐
      ▼           ▼           ▼
 showMenu()   calculate()   printResult()
```

`main()` acts like a manager.

It doesn't have to perform every task itself.

Instead, it delegates work to specialized methods.

This keeps programs clean and scalable.

---

# Good Method Philosophy

A good method usually performs **one clear task**.

Examples:

✅ Good

```text
calculateArea()

printMenu()

readNumber()

convertTemperature()

isPrime()
```

Each name clearly communicates its purpose.

---

Poor examples:

```text
doEverything()

process()

executeStuff()

run()
```

These names don't reveal what the method actually does.

As programs grow, descriptive names become essential.

---

# Summary

In this chapter, you learned that:

* A method is a named block of reusable code.
* Methods help organize programs into smaller tasks.
* They reduce duplicated code.
* They improve readability and maintenance.
* Every Java application already starts with one method: `main()`.
* As your programs grow, `main()` should coordinate the program rather than contain all of its logic.

---

# Chapter 01 Practice (Conceptual)

Before writing your own methods, answer these questions:

1. Why are methods useful in programming?
2. What problems arise when all code is written inside `main()`?
3. What is the role of the `main()` method?
4. What does it mean for a method to have a "single responsibility"?
5. Which version is easier to maintain: one with duplicated code or one using reusable methods? Why?

Try answering them in your own words. then we'll continue to **Chapter 02 — Declaring and Invoking Methods**, where you'll write your first custom methods.
