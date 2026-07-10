# Module 10 — Exception Handling

Welcome to **Module 10**.

Up until now, our applications have assumed that users always provide valid input and that everything works perfectly. In real software, that assumption is never true.

Users type letters where numbers are expected.

Files may not exist.

Network connections fail.

Business rules are violated.

Unexpected situations happen constantly.

Professional software must **detect**, **communicate**, and **recover** from these situations whenever possible.

That is exactly why Java has an exception handling system.

Unlike many beginner tutorials that treat exceptions as merely `try/catch`, this module will teach **the complete exception mechanism**, how Java propagates errors internally, and how professionals decide where exceptions should be handled.

---

# Module Objectives

By the end of this module you will be able to:

* Understand Java's exception system
* Distinguish Errors from Exceptions
* Understand checked and unchecked exceptions
* Read exception stack traces
* Handle exceptions safely
* Throw exceptions intentionally
* Propagate exceptions through methods
* Create custom exception classes
* Design domain-specific exceptions
* Build resilient console applications
* Organize exception classes professionally
* Apply exception handling best practices

---

# Prerequisites

Before starting this module you should already understand:

* Variables
* Methods
* Classes
* Constructors
* Objects
* Encapsulation
* Inheritance
* Polymorphism
* Abstract Classes
* Interfaces
* Enums
* Packages
* Collections
* Control Flow

Everything learned so far will now be combined.

---

# Module Structure

---

# Chapter 1 — Why Programs Fail

* What is an error?
* What is an exception?
* Unexpected situations
* Defensive programming
* Why exceptions exist
* Error codes vs exceptions

---

# Chapter 2 — Errors vs Exceptions

* `Throwable`
* `Error`
* `Exception`
* Runtime failures
* Recoverable vs unrecoverable problems
* Java exception hierarchy

---

# Chapter 3 — Checked vs Unchecked Exceptions

* Checked exceptions
* Runtime exceptions
* Compiler enforcement
* When to use each
* Professional guidelines

---

# Chapter 4 — Understanding Exception Flow

* What happens internally
* Stack unwinding
* Call stack
* Exception propagation
* Reading stack traces

---

# Chapter 5 — try / catch

* Basic syntax
* Catching exceptions
* Program recovery
* Execution flow
* Multiple examples

---

# Chapter 6 — Multiple catch Blocks

* Catching specific exceptions
* Catch ordering
* Exception hierarchy
* Best practices

---

# Chapter 7 — finally

* Guaranteed execution
* Cleanup code
* Resource management
* Common mistakes

---

# Chapter 8 — throw

* Throwing exceptions manually
* Business rule validation
* Illegal arguments
* Guard clauses

---

# Chapter 9 — throws

* Declaring exceptions
* Method contracts
* Exception propagation
* Checked exception requirements

---

# Chapter 10 — Custom Exceptions

* Creating your own exceptions
* Extending `Exception`
* Extending `RuntimeException`
* Domain exceptions
* Professional organization

---

# Chapter 11 — Built-in Java Exceptions

We'll study the most common exceptions you'll encounter:

* `NullPointerException`
* `ArithmeticException`
* `ArrayIndexOutOfBoundsException`
* `IllegalArgumentException`
* `NumberFormatException`
* `IOException`

For each one we'll cover:

* Why it happens
* How to reproduce it
* How to prevent it
* Best practices

---

# Chapter 12 — Exception Handling Best Practices

Topics include:

* Catch only what you can handle
* Never ignore exceptions
* Don't catch `Exception` unnecessarily
* Write meaningful messages
* Rethrow when appropriate
* Validate inputs early
* Prefer fail-fast behavior
* Avoid exceptions for normal program flow

---

# Guided Exercises

Throughout the module we'll progressively build several small applications.

---

## Exercise 1 — Division Calculator

Concepts:

* `try`
* `catch`
* `ArithmeticException`

Goal:

Safely divide two numbers.

---

## Exercise 2 — Number Parser

Concepts:

* User input
* Parsing
* `NumberFormatException`

Goal:

Accept only valid numbers.

---

## Exercise 3 — Student Registration

Concepts:

* Validation
* Custom exceptions

Goal:

Reject invalid ages.

---

## Exercise 4 — Bank Account

Concepts:

* Business rules
* Custom checked exception

Goal:

Reject withdrawals larger than the balance.

---

## Exercise 5 — Login System

Concepts:

* Authentication
* Runtime exceptions

Goal:

Throw an exception for invalid credentials.

---

## Exercise 6 — Exception Propagation

Concepts:

* Multiple methods
* `throws`
* Propagation
* Stack unwinding

Goal:

Observe how Java propagates exceptions until they are handled.

---

## Exercise 7 — finally Practice

Concepts:

* Cleanup
* Guaranteed execution

Goal:

Simulate closing resources even when errors occur.

---

# Project Organization

We'll continue using a professional project structure.

```text
src/
│
├── Main.java
│
├── model/
│
├── service/
│
├── exception/
│     ├── InvalidAgeException.java
│     ├── InsufficientFundsException.java
│     └── InvalidLoginException.java
│
└── util/
```

---

## Why a dedicated exception package?

Professional projects separate responsibilities.

Instead of mixing exception classes with business classes, custom exceptions live inside their own package because they represent **error contracts**, not business entities.

This organization makes projects:

* easier to navigate
* easier to maintain
* easier to scale
* more readable for teams

---

## Domain Exceptions vs Java Exceptions

During this module you'll encounter two categories.

### Java Exceptions

These are provided by the Java language.

Examples:

* `NullPointerException`
* `IOException`
* `ArithmeticException`

They describe technical problems.

---

### Domain Exceptions

These are created by developers.

Examples:

* `InvalidAgeException`
* `InsufficientFundsException`
* `InvalidLoginException`

They describe business rule violations.

Instead of saying:

> Something went wrong.

They communicate:

> The customer attempted to withdraw more money than available.

This makes applications much easier to understand and maintain.

---

# Final Project

## Banking System with Exception Handling

Throughout the second half of this module we'll build a progressively more robust banking application.

Features include:

* Deposit
* Withdraw
* Balance inquiry
* Login validation
* Business rule validation
* Safe user input
* Exception propagation
* Multiple `try/catch`
* Multiple custom exceptions
* Package organization
* Clean architecture

The project will **not** be built all at once.

Each chapter introduces new concepts, and we'll integrate them into the project step by step.

By the end of the module, you'll have a realistic console application that demonstrates professional exception handling practices.

---

# Learning Philosophy

This module is about much more than avoiding crashes.

Professional developers don't ask:

> "How do I stop the program from crashing?"

They ask:

* What can go wrong?
* Who should handle this problem?
* Can the program recover?
* Should this exception propagate?
* Is this a programming mistake or a business rule violation?
* What information should be communicated to the caller?

These questions lead to software that is more reliable, maintainable, and easier to debug.

---

# ✔️ Next Step

Proceed to **Chapter 1 — Why Programs Fail**, where we'll begin by understanding **why exceptions exist**, the difference between **errors and exceptions**, and why modern programming languages prefer exceptions over traditional error codes before we write our first `try/catch` block.
