# Chapter 2 — Errors vs Exceptions

Now that we understand **why exception handling exists**, it's time to look at how Java organizes all problems internally.

One of Java's greatest strengths is that it does **not** treat every failure the same way.

Some failures can be recovered from.

Others cannot.

Java separates these categories using a class hierarchy centered around a single base class.

Understanding this hierarchy is essential before learning `try` and `catch`.

---

# Chapter Objectives

By the end of this chapter, you will understand:

* What `Throwable` is
* The difference between `Error` and `Exception`
* Why Java separates recoverable and unrecoverable problems
* The basic exception hierarchy
* When your code should (and should not) handle different types of problems
* How Java decides what can be thrown

---

# Everything Starts with `Throwable`

At the top of Java's error handling system is the class:

```java
Throwable
```

Every object that can be thrown by Java inherits from this class.

The hierarchy begins like this:

```text
               Throwable
               /       \
          Error     Exception
```

This means:

* Every `Error` **is a** `Throwable`.
* Every `Exception` **is a** `Throwable`.

Since both are subclasses of `Throwable`, both can technically be thrown using the `throw` keyword.

However, they represent very different situations.

---

# Why Have Two Categories?

Imagine two completely different problems.

### Situation 1

A user enters:

```text
abc
```

when your program expects a number.

Can the program recover?

Yes.

You can simply ask the user to enter another value.

---

### Situation 2

The Java Virtual Machine runs out of memory.

Can your program easily recover?

Usually not.

There may not even be enough memory left to create the objects needed for recovery.

These are fundamentally different kinds of failures.

Java represents them with different branches of the hierarchy.

---

# The `Error` Branch

`Error` represents serious problems that applications are generally **not expected to handle**.

These problems usually originate from:

* The Java Virtual Machine (JVM)
* The operating system
* Resource exhaustion
* Corrupted runtime state

Examples include:

* `OutOfMemoryError`
* `StackOverflowError`
* `VirtualMachineError`

These indicate that something has gone wrong at a very low level.

---

# Example: Out of Memory

Imagine a program that keeps creating objects without stopping.

Eventually, the JVM may throw:

```java
OutOfMemoryError
```

At this point:

* Memory is exhausted.
* New objects may not be created.
* The application may not continue safely.

Trying to "recover" from this situation is often unrealistic.

---

# Example: Stack Overflow

Consider a method that accidentally calls itself forever.

```java
public void infinite() {
    infinite();
}
```

Each method call consumes stack memory.

Eventually, Java throws:

```java
StackOverflowError
```

The problem is not invalid user input.

It is a programming error that exhausted the call stack.

---

# Should We Catch `Error`?

In almost all applications:

**No.**

Errors usually indicate that the environment itself is no longer reliable.

Professional developers generally allow the application to terminate, investigate the cause, and fix the underlying problem rather than trying to continue.

As a beginner, you should think of `Error` as:

> "Something is fundamentally wrong with the runtime environment."

---

# The `Exception` Branch

`Exception` represents problems that applications are **expected to detect and handle**.

Examples include:

* Invalid input
* Missing files
* Division by zero
* Invalid business rules
* Failed parsing
* Invalid object state

Unlike `Error`, these situations often allow the application to continue.

---

# Real-World Example

Imagine an ATM.

A customer enters the wrong PIN.

Should the ATM shut down?

Of course not.

Instead, it should display a message and allow another attempt.

This is exactly the kind of situation exceptions are designed for.

---

# Visualizing the Hierarchy

Here is a simplified view of Java's exception system:

```text
Throwable
│
├── Error
│     ├── OutOfMemoryError
│     ├── StackOverflowError
│     └── ...
│
└── Exception
      │
      ├── IOException
      ├── RuntimeException
      │      ├── NullPointerException
      │      ├── ArithmeticException
      │      ├── IllegalArgumentException
      │      ├── NumberFormatException
      │      └── ...
      │
      └── Other Checked Exceptions
```

Don't worry about every class yet.

We'll study the important ones throughout this module.

---

# Why Is Everything a Class?

Remember from previous modules that Java is object-oriented.

Instead of representing failures as numbers or strings, Java represents them as objects.

An exception object can contain:

* A descriptive message
* The type of problem
* The location where it occurred
* The chain of method calls that led to it (the stack trace)
* Another exception that caused it (the cause)

This rich information makes debugging much easier than simple error codes.

---

# What Does "Throwing" Mean?

When Java encounters a problem, it creates an exception object and **throws** it.

Conceptually:

```text
Problem occurs
        ↓
Create exception object
        ↓
Throw exception
        ↓
Search for someone to handle it
```

If nobody handles it, the program terminates and prints information about the failure.

We'll learn the exact execution flow in Chapter 4.

---

# Errors vs Exceptions

| Error                                              | Exception                                                                    |
| -------------------------------------------------- | ---------------------------------------------------------------------------- |
| Serious runtime problem                            | Recoverable application problem                                              |
| Usually caused by the JVM                          | Usually caused by user input, business rules, or expected runtime conditions |
| Applications normally do not handle them           | Applications are expected to handle them                                     |
| Recovery is often impossible                       | Recovery is often possible                                                   |
| Examples: `OutOfMemoryError`, `StackOverflowError` | Examples: `IOException`, `ArithmeticException`, `IllegalArgumentException`   |

---

# Can Developers Create Errors?

Technically, yes.

You could write:

```java
public class MyError extends Error {

}
```

However, this is almost never appropriate.

Custom application failures should almost always extend `Exception` or `RuntimeException`, not `Error`.

`Error` is reserved for severe runtime problems.

---

# Can Developers Create Exceptions?

Absolutely.

In fact, professional applications create custom exceptions all the time.

Examples:

```text
InvalidAgeException
```

```text
InsufficientFundsException
```

```text
InvalidLoginException
```

These describe business problems much more clearly than generic Java exceptions.

We'll build these classes later in this module.

---

# Common Beginner Mistakes

## Mistake 1: Thinking every failure is an exception

Not all failures are exceptions.

Some are `Error`s, which indicate serious runtime problems.

---

## Mistake 2: Catching everything

Some beginners try to catch every `Throwable`.

```java
catch (Throwable t) {
    // ...
}
```

This is almost always a bad idea because it also catches serious `Error`s that your application should generally not try to recover from.

---

## Mistake 3: Confusing programming bugs with user mistakes

A wrong password is an expected application scenario.

A `StackOverflowError` caused by infinite recursion is a programming bug.

These should be handled differently.

---

## Mistake 4: Ignoring the hierarchy

Understanding inheritance is important here.

Because all exceptions inherit from `Throwable`, Java can treat them polymorphically while still allowing specific handling for different exception types.

---

# Professional Best Practices

* Treat `Error` as a signal of severe runtime failure.
* Handle `Exception` when recovery is possible.
* Create custom exceptions for business rules instead of using generic exceptions.
* Use the exception hierarchy to write clear and maintainable code.
* Avoid catching `Throwable` unless you have a very specialized reason.

---

# Chapter Summary

In this chapter, you learned that:

* `Throwable` is the root of Java's exception system.
* Java divides problems into two main branches: `Error` and `Exception`.
* `Error` represents severe runtime failures that applications generally do not recover from.
* `Exception` represents recoverable problems that applications are expected to handle.
* Exceptions are objects that carry detailed information about failures.
* The exception hierarchy makes Java's error handling flexible and extensible.

Understanding this hierarchy is the foundation for everything that follows.

---

# ✔️ Next Step

Proceed to **Chapter 3 — Checked vs Unchecked Exceptions**, where you'll learn why the Java compiler forces you to handle some exceptions but not others, and how to decide which type of exception to use in your own applications.
