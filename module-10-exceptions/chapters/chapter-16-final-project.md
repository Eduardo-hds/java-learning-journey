# Chapter 16 — Final Project: Testing, Refactoring & Module Completion

Congratulations!

Your banking system is now complete.

Before considering any software "finished," professional developers perform one final phase:

* Testing
* Reviewing
* Refactoring
* Verifying edge cases

Writing code is only part of software development.

Ensuring that the code behaves correctly is equally important.

In this final chapter, you'll verify that your application works as expected and review everything learned throughout Module 10.

---

# Chapter Objectives

By the end of this chapter, you will:

* Test every feature of the banking system
* Identify edge cases
* Verify exception handling
* Perform small refactoring improvements
* Review the concepts learned in Module 10
* Complete the module successfully

---

# Why Test?

Testing answers an important question:

> **"Does the application behave correctly in both expected and unexpected situations?"**

A banking system should not only work when everything goes right.

It must also behave safely when users make mistakes.

Examples:

* Wrong password
* Negative deposit
* Invalid withdrawal
* Invalid menu option
* Invalid numeric input

These are all situations your application should handle gracefully.

---

# Functional Test Checklist

Run your application and verify each scenario.

| Test                       | Expected Result                 |
| -------------------------- | ------------------------------- |
| Valid login                | Login successful                |
| Empty username             | `InvalidLoginException`         |
| Empty password             | `InvalidLoginException`         |
| Wrong credentials          | `InvalidLoginException`         |
| Deposit positive amount    | Balance increases               |
| Deposit zero               | `InvalidDepositException`       |
| Deposit negative amount    | `InvalidDepositException`       |
| Withdraw valid amount      | Balance decreases               |
| Withdraw more than balance | `InsufficientFundsException`    |
| Withdraw negative amount   | `IllegalArgumentException`      |
| Invalid menu option        | Error message and continue      |
| Invalid numeric input      | Error message and continue      |
| Exit option                | Application terminates normally |

Try every one of these.

Professional developers never assume code works—they verify it.

---

# Edge Case Testing

Edge cases are inputs that sit at or beyond the boundaries of valid values.

For example:

Initial balance:

```text id="mxx0az"
500
```

Test:

```text id="gl7llj"
Withdraw 500
```

Expected:

```text id="xtix9h"
Success
Balance = 0
```

Now test:

```text id="7tfjkp"
Withdraw 501
```

Expected:

```text id="oe0zht"
InsufficientFundsException
```

Boundary testing often reveals bugs that normal testing misses.

---

# Test Invalid Input

Menu:

```text id="8kqlm2"
abc
```

Expected:

```text id="a4t9qk"
Please enter a valid menu option.
```

Application continues.

---

Deposit:

```text id="qeq7ww"
xyz
```

Expected:

```text id="zlhm4g"
Invalid number.
```

Application continues.

---

Withdrawal:

```text id="s2te8w"
abc
```

Expected:

```text id="ox5rwp"
Invalid number.
```

Again, the application should continue running.

---

# Verify Exception Messages

Professional applications avoid vague messages.

Poor:

```text id="8ev8lc"
Error
```

Better:

```text id="xk1zj9"
Deposit amount must be greater than zero.
```

Even better:

```text id="rhwwtz"
Deposit amount (-50.0) must be greater than zero.
```

Including the invalid value can make debugging much easier, especially in larger applications.

---

# Small Refactoring Opportunities

Now that the project works, look for improvements that don't change its behavior.

### Example 1 — Remove Duplicate Messages

Instead of repeating:

```java
System.out.println("Invalid number.");
```

multiple times, you could create a helper method:

```java
private static void printInvalidNumberMessage() {
    System.out.println("Invalid number.");
}
```

This reduces duplication.

---

### Example 2 — Extract Constants

Instead of:

```java
new User("admin", "1234");
```

consider:

```java
private static final String DEFAULT_USERNAME = "admin";
private static final String DEFAULT_PASSWORD = "1234";
```

This makes changes easier in the future.

---

### Example 3 — Improve Variable Names

Prefer:

```java
BankService bankService;
```

instead of:

```java
BankService service;
```

Longer, descriptive names often improve readability.

---

# Review of Module Concepts

Let's revisit everything you learned.

---

## Exception Fundamentals

You learned:

* What exceptions are
* Why they exist
* Why Java uses exceptions instead of error codes
* The difference between recoverable and unrecoverable problems

---

## Exception Hierarchy

You explored:

```text id="jpb54l"
Throwable
│
├── Error
│
└── Exception
      │
      └── RuntimeException
```

You learned that application code should generally extend:

* `Exception`
* `RuntimeException`

—not `Error`.

---

## Checked vs. Unchecked Exceptions

You practiced both.

Checked:

* Must be handled or declared.
* Represent recoverable situations.

Unchecked:

* Usually indicate programming mistakes or invalid API usage.
* Do not require explicit handling.

---

## `try`

You used `try` blocks to monitor risky operations.

---

## `catch`

You handled specific exception types and displayed meaningful messages.

---

## Multiple `catch` Blocks

You learned to catch different exceptions separately based on how each should be handled.

---

## `finally`

You learned that `finally` executes whether an exception occurs or not, making it ideal for cleanup tasks such as closing resources.

---

## `throw`

You created exceptions intentionally to enforce business rules.

---

## `throws`

You declared checked exceptions in method signatures so callers were aware of potential failures.

---

## Exception Propagation

You observed how exceptions move up the call stack until they are caught.

---

## Custom Exceptions

You created:

* `InvalidLoginException`
* `InvalidDepositException`
* `InsufficientFundsException`

These exceptions made your business rules much clearer than generic exceptions would.

---

## Defensive Programming

You consistently validated:

* Method arguments
* User input
* Null references
* Business rules

This prevented many runtime errors before they occurred.

---

# Final Project Architecture

Your finished application follows a clean layered structure:

```text id="jlwm5x"
Main
 │
 ▼
Services
 │
 ▼
Models
```

Exceptions are used whenever a business rule is violated.

This organization reflects the architecture used in many professional Java applications.

---

# What You've Built

By completing this project, you've created a console application that:

* Authenticates users
* Validates credentials
* Handles deposits
* Handles withdrawals
* Protects account integrity
* Uses custom checked exceptions
* Uses custom unchecked exceptions
* Handles invalid user input
* Recovers gracefully from errors
* Maintains a clean package structure

This is a significant step toward writing robust, maintainable Java applications.

---

# Looking Ahead

In the next module, you'll move beyond error handling and begin exploring more advanced features of the Java language and standard library.

You'll discover new ways to organize data, process collections, and write cleaner, more expressive code.

Everything you've learned about object-oriented programming and exception handling will continue to play an important role.

---

# Module 10 Summary

By completing Module 10, you have learned:

* ✅ Exception fundamentals
* ✅ Errors vs. Exceptions
* ✅ Checked vs. Unchecked exceptions
* ✅ Exception hierarchy (`Throwable`)
* ✅ `try`
* ✅ `catch`
* ✅ Multiple `catch` blocks
* ✅ `finally`
* ✅ `throw`
* ✅ `throws`
* ✅ Exception propagation
* ✅ Custom checked exceptions
* ✅ Custom unchecked exceptions
* ✅ Professional exception handling practices
* ✅ Defensive programming
* ✅ Java built-in exceptions
* ✅ Building resilient console applications

---

# 🎉 Congratulations!

You have successfully completed **Module 10 — Exceptions**.

At this point in the bootcamp, you've developed a strong understanding of how Java applications detect, communicate, and recover from errors. More importantly, you've learned to design applications that **prevent invalid states** instead of simply reacting to failures.

This knowledge is foundational for building reliable, production-quality software.

---

# ✔️ Next Step

Proceed to **Module 11**, where you'll continue expanding your Java skills with more advanced language features and APIs, applying the same professional project structure and development practices you've built throughout this bootcamp.
