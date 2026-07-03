# Chapter 10 — Comments and Documentation

## Overview

Programs are written for computers to execute, but they're also written for **people to read**.

In a professional environment, your code will likely be read many more times than it is written. That reader could be:

* A teammate
* Your future self
* A reviewer
* A new developer joining the project

Comments and documentation help explain code when the code itself cannot express the intent clearly.

However, **good developers don't write as many comments as possible—they write as many as necessary.**

In this chapter, you'll learn the different types of comments in Java, when to use them, when to avoid them, and how to write documentation using Javadoc.

---

# Why Do Comments Exist?

Imagine seeing this code:

```java
double result = price * 0.18;
```

What does `0.18` represent?

* Tax?
* Discount?
* Commission?
* Interest?

A comment could explain the intent:

```java
// Apply the sales tax
double result = price * 0.18;
```

Even better would be eliminating the magic number:

```java
final double SALES_TAX = 0.18;

double result = price * SALES_TAX;
```

Notice that the second version doesn't need a comment because the code explains itself.

This demonstrates an important principle:

> **The best comment is often well-written code.**

---

# Single-Line Comments

Single-line comments begin with:

```java
//
```

Everything after `//` on that line is ignored by the compiler.

Example:

```java
// Store the user's age
int age = 25;
```

You can also comment out code temporarily:

```java
// System.out.println("Debug");
```

This is useful while testing.

---

# Multi-Line Comments

For longer explanations:

```java
/*
   This program calculates
   the final product price
   after tax has been applied.
*/
```

Everything between:

```java
/*
```

and

```java
*/
```

is ignored.

Example:

```java
/*
   Temporary implementation.

   Will be replaced after
   the database module.
*/
```

---

# Javadoc Comments

Java has a special type of comment:

```java
/**
 * ...
 */
```

These are called **Javadoc comments**.

Unlike normal comments, Javadoc can be processed to automatically generate professional documentation for classes, methods, and packages.

Example:

```java
/**
 * Calculates the area of a rectangle.
 */
```

Later in the Bootcamp, you'll learn how to generate HTML documentation directly from Javadoc comments.

---

# When Should You Write Comments?

Comments should explain **why**, not **what**.

Poor comment:

```java
// Add 1 to count
count++;
```

The code already makes that obvious.

Better:

```java
// Count the current player's turn
count++;
```

This explains the intention behind the operation.

---

# Avoid Explaining Obvious Code

Bad:

```java
// Declare an integer
int age;
```

Bad:

```java
// Print the name
System.out.println(name);
```

These comments provide no useful information.

If a comment simply repeats the code, it should usually be removed.

---

# Explain Business Rules

Sometimes the code is correct but the reason isn't obvious.

Example:

```java
// Customers under 18 cannot create an account
if (age < 18) {
    // ...
}
```

This explains a business requirement that isn't obvious from the code alone.

---

# TODO Comments

Developers often leave reminders.

Example:

```java
// TODO: Validate user input
```

Or:

```java
// TODO: Replace hardcoded values with database data
```

Most IDEs, including IntelliJ IDEA, highlight `TODO` comments automatically.

These help developers track unfinished work.

---

# FIXME Comments

Another common convention:

```java
// FIXME: Incorrect calculation for negative numbers
```

This indicates known bugs that need to be fixed.

Unlike `TODO`, which usually refers to future work, `FIXME` points to an existing problem.

---

# Commented-Out Code

Example:

```java
// int total = price * quantity;
```

Leaving old code commented out is generally discouraged.

Professional teams use **Git** for version control.

Instead of keeping obsolete code in comments, delete it.

If needed later, Git allows you to recover previous versions.

---

# Writing Self-Documenting Code

Compare these examples.

Poor:

```java
double x = price * 0.18;
```

Better:

```java
final double SALES_TAX = 0.18;

double salesTax = price * SALES_TAX;
```

The second version is understandable without comments.

Good naming often eliminates the need for explanations.

---

# Formatting Comments

Good:

```java
// Calculate the customer's final balance
```

Avoid:

```java
//calculatecustomerfinalbalance
```

Keep comments:

* Short
* Clear
* Grammatically correct
* Focused on intent

---

# Common Beginner Mistakes

## Commenting Every Line

Poor:

```java
// Declare age
int age = 20;

// Print age
System.out.println(age);
```

The comments add no value.

---

## Outdated Comments

Example:

```java
// Maximum score is 100
final int MAX_SCORE = 200;
```

The code changed.

The comment didn't.

Outdated comments are worse than no comments because they mislead readers.

---

## Using Comments Instead of Good Names

Poor:

```java
double x = total * 0.15; // Tax
```

Better:

```java
double tax = total * SALES_TAX;
```

The code becomes self-explanatory.

---

# Best Practices

* Explain **why**, not **what**.
* Prefer self-documenting code.
* Keep comments up to date.
* Remove obsolete commented-out code.
* Use Javadoc for public classes and methods.
* Use `TODO` and `FIXME` when appropriate.

---

# Guided Exercise

Create a program called `CommentsDemo.java`.

Include:

* At least three single-line comments.
* One multi-line comment.
* One Javadoc comment above the class.
* A `TODO` comment.
* A `FIXME` comment.

Ensure that every comment serves a clear purpose.

---

# Independent Exercises

## Easy

Write a simple program containing:

* Two variables.
* One useful single-line comment explaining a business rule.

---

## Medium

Create a program with at least:

* Three meaningful comments.
* One `TODO`.
* One multi-line comment.

Avoid comments that merely repeat the code.

---

## Hard

Create a program called `DocumentationExample.java`.

Write a fully documented class using:

* Javadoc comments.
* Single-line comments.
* Multi-line comments.

Make sure every comment adds useful information and improves readability.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

1. Why do comments exist?
2. What is the difference between `//` and `/* ... */`?
3. What is Javadoc used for?
4. What should comments explain: **what** or **why**?
5. Why are outdated comments dangerous?
6. What is a `TODO` comment?
7. What is a `FIXME` comment?
8. Why is commented-out code discouraged?
9. What is self-documenting code?
10. When is a comment unnecessary?

---

# Chapter Summary

In this chapter, you learned:

* The purpose of comments in professional software development.
* The difference between single-line, multi-line, and Javadoc comments.
* When comments improve code and when they simply add noise.
* Why good naming often removes the need for comments.
* How `TODO` and `FIXME` help organize development work.
* Why outdated comments and commented-out code should be avoided.

---

## Progress Checkpoint

Before moving on to **Chapter 11 — Java Naming Conventions**, make sure you can:

* Use single-line, multi-line, and Javadoc comments correctly.
* Explain the difference between documenting **what** code does and **why** it exists.
* Recognize unnecessary or outdated comments.
* Write self-documenting code using meaningful names.
* Use `TODO` and `FIXME` comments appropriately.
