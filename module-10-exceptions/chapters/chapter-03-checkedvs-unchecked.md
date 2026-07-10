# Chapter 3 — Checked vs Unchecked Exceptions

In the previous chapter, we learned that Java separates problems into **Errors** and **Exceptions**.

However, Java goes one step further.

Not all exceptions are treated the same way.

Some exceptions **must** be handled or declared.

Others can occur without any warning from the compiler.

This distinction is one of Java's most unique features and is a common source of confusion for beginners.

By the end of this chapter, you'll understand why this distinction exists and how professional developers decide which type of exception to use.

---

# Chapter Objectives

By the end of this chapter, you will understand:

* What checked exceptions are
* What unchecked exceptions are
* Why Java distinguishes between them
* How the compiler enforces checked exceptions
* The relationship with `RuntimeException`
* When to create checked vs unchecked custom exceptions
* Best practices used in professional applications

---

# The Exception Hierarchy Revisited

Let's expand the hierarchy we saw in the previous chapter.

```text
Throwable
│
├── Error
│
└── Exception
      │
      ├── RuntimeException
      │      ├── NullPointerException
      │      ├── ArithmeticException
      │      ├── IllegalArgumentException
      │      ├── NumberFormatException
      │      └── ...
      │
      ├── IOException
      ├── SQLException
      ├── ClassNotFoundException
      └── ...
```

Notice something important:

Not every exception extends `RuntimeException`.

This is exactly what creates the distinction between **checked** and **unchecked** exceptions.

---

# Two Categories of Exceptions

Java divides exceptions into two groups.

## Checked Exceptions

These are exceptions that the compiler forces you to deal with.

If your code might produce one of these exceptions, you must either:

* Handle it with `try/catch`, or
* Declare it with `throws`

Otherwise, your program **will not compile**.

---

## Unchecked Exceptions

These exceptions do **not** require handling at compile time.

The compiler allows your code to compile even if you don't handle them.

If they occur at runtime and are not handled, the application will terminate.

---

# Why Does Java Do This?

Imagine you're reading a file.

Many things could go wrong:

* The file doesn't exist.
* You don't have permission.
* The disk fails.
* The file is already in use.

These situations are expected when working with external resources.

Java wants to make sure you think about them.

That's why file-related exceptions are usually **checked**.

---

Now imagine this code:

```java
int number = Integer.parseInt("abc");
```

The developer clearly supplied an invalid value.

This is usually considered a programming mistake rather than an unavoidable external condition.

Therefore, Java treats it as an **unchecked** exception.

---

# Checked Exceptions

Checked exceptions represent situations that are often outside the programmer's control.

Examples:

* Missing files
* Network failures
* Database communication problems
* Interrupted threads

These are problems that well-written applications should anticipate.

---

## Example

Imagine a method that reads a file.

```java
public void readFile() {
    // read file
}
```

Internally, Java knows reading a file may fail.

Therefore, it requires the developer to acknowledge that possibility.

Until you handle or declare the exception, the compiler reports an error.

This is called **compile-time checking**.

---

# Unchecked Exceptions

Unchecked exceptions extend:

```java
RuntimeException
```

These usually represent programming mistakes, invalid state, or broken assumptions.

Examples:

```java
NullPointerException
```

```java
ArithmeticException
```

```java
IllegalArgumentException
```

```java
NumberFormatException
```

These often indicate that something in the code should have been validated or corrected earlier.

---

# Why Doesn't Java Force Us to Handle Them?

Imagine this code:

```java
String name = null;

System.out.println(name.length());
```

This will eventually produce a `NullPointerException`.

Should the compiler force us to write a `try/catch` every time we access an object?

That would make almost every Java program filled with unnecessary exception handling.

Instead, Java expects developers to write correct code and validate their data when appropriate.

---

# Visual Comparison

| Checked Exception                                | Unchecked Exception                                     |
| ------------------------------------------------ | ------------------------------------------------------- |
| Checked by the compiler                          | Not checked by the compiler                             |
| Must be handled or declared                      | Optional to handle                                      |
| Usually caused by external conditions            | Usually caused by programming mistakes or invalid input |
| Extends `Exception` (but not `RuntimeException`) | Extends `RuntimeException`                              |
| Examples: `IOException`, `SQLException`          | Examples: `NullPointerException`, `ArithmeticException` |

---

# Compile-Time vs Runtime

Understanding **when** these exceptions are considered is very important.

### Checked Exception

The compiler detects that a method may throw one.

It stops compilation until you decide how to deal with it.

```text
Write code
     ↓
Compiler detects checked exception
     ↓
Handle or declare it
     ↓
Compilation succeeds
```

---

### Unchecked Exception

The compiler allows the program to compile.

If the exception occurs while the program is running, Java throws it immediately.

```text
Write code
     ↓
Compiler allows it
     ↓
Program runs
     ↓
Problem occurs
     ↓
Exception is thrown
```

---

# A Real-World Analogy

Imagine you're going on a road trip.

### Checked Exception

Before leaving, someone reminds you:

> "The road might be closed."

You can prepare by:

* choosing another route,
* checking traffic,
* or delaying the trip.

You are warned in advance.

---

### Unchecked Exception

While driving, you accidentally hit a curb because you weren't paying attention.

Nobody could reasonably force you to prepare for every careless mistake beforehand.

Instead, you're expected to drive correctly.

---

# Which One Should My Custom Exception Extend?

This is one of the most common design decisions you'll make.

## Use a Checked Exception When

The caller can reasonably recover from the problem.

Examples:

* File not found
* Invalid bank transaction that should be retried
* Temporary network issue

The caller should be made aware that the operation may fail.

---

## Use an Unchecked Exception When

The problem represents:

* Invalid arguments
* Invalid object state
* Programming mistakes
* Violated assumptions
* Impossible situations

Examples:

* Negative age passed to a constructor
* Null object where null isn't allowed
* Invalid enum value
* Incorrect method usage

---

# Our Bootcamp Examples

We'll build these custom exceptions later.

### Checked

```java
InsufficientFundsException
```

Why?

Because the caller may choose another withdrawal amount or ask the user for a different action.

---

### Unchecked

```java
InvalidLoginException
```

In our learning project, we'll model this as a runtime exception to demonstrate custom unchecked exceptions. In a real application, whether login failures should be represented as exceptions or regular control flow depends on the design.

---

### Unchecked

```java
IllegalArgumentException
```

If a method receives an impossible value, that's usually a programming error.

---

# Common Beginner Mistakes

## Mistake 1

Thinking checked exceptions are "better."

They are not.

They solve a different problem.

---

## Mistake 2

Making every custom exception checked.

This often forces unnecessary `try/catch` blocks throughout the codebase.

---

## Mistake 3

Making every custom exception unchecked.

This removes compile-time guidance and can make important failures easier to overlook.

---

## Mistake 4

Using exceptions instead of validation.

Example:

```java
if (age < 0) {
    // Validate directly
}
```

When a simple condition can prevent an invalid operation, validate first instead of relying on an exception.

---

# Professional Best Practices

* Use checked exceptions for recoverable situations that callers should explicitly consider.
* Use unchecked exceptions for programming mistakes and invalid API usage.
* Choose the exception type based on how callers are expected to respond.
* Don't create custom exceptions unless they add meaningful information to your domain.
* Keep exception hierarchies simple and intentional.

---

# Chapter Summary

In this chapter, you learned that:

* Java divides exceptions into **checked** and **unchecked** categories.
* Checked exceptions must be handled or declared because the compiler enforces them.
* Unchecked exceptions extend `RuntimeException` and are not checked at compile time.
* Checked exceptions usually represent recoverable external problems.
* Unchecked exceptions usually represent programming mistakes or violated assumptions.
* Choosing the correct exception type improves the clarity and maintainability of your applications.

This distinction will become much clearer once we begin writing code with `try`, `catch`, `throw`, and `throws`.

---

# ✔️ Next Step

Proceed to **Chapter 4 — Understanding Exception Flow**, where you'll see exactly what happens inside the JVM when an exception is thrown, how the call stack is unwound, how propagation works, and how to read a stack trace.
