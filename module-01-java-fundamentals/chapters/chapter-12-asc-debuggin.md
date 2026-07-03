# Chapter 12 — Basic Debugging

## Overview

Writing code is only half of programming.

The other half is **finding and fixing problems**.

No matter how experienced a developer becomes, bugs are inevitable. Professional developers don't avoid bugs—they know how to locate them efficiently.

This process is called **debugging**.

In this chapter, you'll learn what debugging is, the different types of errors in Java, how to use the debugger in IntelliJ IDEA, and how to systematically investigate problems instead of guessing.

---

# What Is Debugging?

**Debugging** is the process of identifying, understanding, and fixing errors in a program.

The word **bug** originally referred to unexpected behavior in software. While there's a famous story about an actual moth found in a computer, today the term simply means **an error or defect in a program**.

Debugging is not about randomly changing code until it works.

It is a structured investigation:

1. Observe the problem.
2. Reproduce the problem.
3. Find the cause.
4. Fix the cause.
5. Test the solution.

---

# Types of Errors

Java programs commonly have three categories of errors:

* Syntax Errors
* Runtime Errors
* Logical Errors

Understanding the difference helps you know where to look when something goes wrong.

---

# Syntax Errors

A **syntax error** occurs when your code violates Java's grammar rules.

Example:

```java
int age = ;
```

The compiler immediately reports an error.

Other examples:

```java
System.out.println("Hello"
```

Missing closing parenthesis.

Or:

```java
public clas Main
```

Misspelled keyword.

### Characteristics

* Detected before execution.
* Prevent the program from compiling.
* Usually easy to fix because the compiler points to the location.

---

# Runtime Errors

A **runtime error** occurs after the program starts running.

Example:

```java
Scanner scanner = new Scanner(System.in);

int age = scanner.nextInt();
```

If the user enters:

```text
twenty
```

Java throws an exception because `"twenty"` cannot be converted into an integer.

The program compiled successfully.

The error only appeared during execution.

Examples of runtime errors:

* Division by zero
* Invalid user input
* Accessing an invalid array index (later module)
* Null reference (later module)

---

# Logical Errors

Logical errors are the most difficult to find.

The program:

* Compiles successfully.
* Runs successfully.
* Produces the wrong result.

Example:

```java
int width = 5;
int height = 4;

int area = width + height;
```

The code runs.

Output:

```text
9
```

But the formula is wrong.

Correct:

```java
int area = width * height;
```

The compiler cannot detect logical mistakes because the syntax is valid.

---

# The Worst Debugging Strategy

Many beginners debug like this:

> "I'll randomly change things until it works."

This approach often creates new bugs.

Instead:

* Understand the problem.
* Isolate the code.
* Test one hypothesis at a time.

Professional debugging is based on evidence, not guesses.

---

# Using `System.out.println()`

The simplest debugging technique is printing values.

Example:

```java
int width = 5;
int height = 4;

System.out.println(width);
System.out.println(height);

int area = width * height;

System.out.println(area);
```

Printing intermediate values helps confirm whether variables contain the expected data.

This technique is often called **print debugging**.

Even experienced developers still use it occasionally.

---

# What Is a Debugger?

A **debugger** is a tool that lets you pause your program while it is running.

Instead of only seeing the final output, you can inspect the program step by step.

You can observe:

* Variable values
* Program flow
* Method calls (later modules)
* Memory state (later modules)

This is much more powerful than printing values.

---

# Breakpoints

A **breakpoint** tells the debugger:

> "Pause execution here."

In IntelliJ IDEA:

1. Open your Java file.
2. Click in the left margin next to a line number.
3. A red dot appears.
4. Start the program using **Debug** instead of **Run**.

When execution reaches that line, the program pauses.

---

# Stepping Through Code

Once paused, IntelliJ provides several options.

## Step Over (F8)

Executes the current line and moves to the next one.

Most commonly used.

---

## Step Into (F7)

Enters a method call.

You'll use this frequently after learning methods.

---

## Step Out (Shift + F8)

Finishes the current method and returns to the caller.

---

## Resume Program (F9)

Continues execution until the next breakpoint or until the program finishes.

---

# Watching Variables

When execution pauses, IntelliJ displays the current values of variables.

Example:

```java
int age = 25;
```

The debugger shows:

```text
age = 25
```

As the program executes, these values update automatically.

This lets you see exactly when a value changes.

---

# Evaluating Expressions

The debugger can also calculate expressions.

Suppose:

```java
int price = 100;
int tax = 18;
```

Without modifying the code, you can evaluate:

```java
price + tax
```

The debugger immediately shows:

```text
118
```

This feature is useful for testing ideas without editing the program.

---

# Reading Error Messages

Beginners often ignore error messages.

Professionals read them carefully.

Suppose Java prints:

```text
NumberFormatException
```

The message tells you:

> Java expected a number but received invalid text.

Learning to interpret error messages is one of the fastest ways to become a better developer.

---

# Common Beginner Mistakes

## Ignoring Compiler Errors

Read the first error carefully.

Many later errors are simply consequences of the first one.

---

## Debugging Without Reproducing the Problem

If you cannot consistently reproduce the bug, it's much harder to fix.

Always identify the exact steps that cause the issue.

---

## Printing Everything

Avoid:

```java
System.out.println(a);
System.out.println(b);
System.out.println(c);
System.out.println(d);
System.out.println(e);
```

Print only the values relevant to your current hypothesis.

Too much output can make debugging harder.

---

## Changing Multiple Things at Once

Bad approach:

* Rename variables.
* Rewrite logic.
* Change calculations.
* Rearrange methods.

All before testing.

Instead:

Make **one change**, then test again.

This makes it much easier to identify what fixed—or introduced—the bug.

---

# Best Practices

* Read compiler errors carefully.
* Reproduce bugs consistently.
* Use breakpoints instead of excessive print statements.
* Test one change at a time.
* Verify assumptions by inspecting variable values.
* Keep debugging systematic and evidence-based.

---

# Guided Exercise

Create a program called `DebugDemo.java`.

Intentionally introduce three different errors:

1. A syntax error.
2. A logical error.
3. A runtime error.

Then:

* Fix the syntax error.
* Run the program to observe the runtime error.
* Correct the runtime error.
* Compare the incorrect and correct logic.

Finally, place a breakpoint before the calculations and step through the program using IntelliJ's debugger, observing how variable values change.

---

# Independent Exercises

## Easy

Create a simple calculator.

Use breakpoints to inspect:

* The two input values.
* The calculated result.

Verify that every variable contains the expected value.

---

## Medium

Write a program that intentionally calculates an incorrect rectangle area.

Use debugging techniques to discover and fix the mistake.

Document what led you to the solution.

---

## Hard

Create a program called `BugHunt.java`.

Include:

* One logical error.
* One runtime error that only appears with certain input.
* At least three variables whose values should be inspected with the debugger.

Use IntelliJ's debugger to locate and correct both issues without relying solely on `System.out.println()`.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

1. What is debugging?
2. What is the difference between a syntax error and a runtime error?
3. Why are logical errors often the hardest to detect?
4. What is a breakpoint?
5. What does **Step Over (F8)** do?
6. When would you use **Step Into (F7)**?
7. Why is `System.out.println()` considered a debugging technique?
8. Why should you avoid changing many things at once while debugging?
9. What information can the debugger show while a program is paused?
10. Why is reading error messages carefully important?

---

# Chapter Summary

In this chapter, you learned:

* What debugging is and why it is an essential programming skill.
* The three main categories of errors: syntax, runtime, and logical.
* How to use `System.out.println()` for basic debugging.
* How IntelliJ IDEA's debugger works, including breakpoints and stepping through code.
* How to inspect variable values and evaluate expressions during execution.
* Best practices for debugging efficiently and systematically.

---

## Progress Checkpoint

Congratulations! You have completed the content of **Module 01 — Java Fundamentals**.

You can now:

* Structure basic Java programs.
* Declare and use variables and primitive data types.
* Perform type casting safely.
* Use constants and follow naming conventions.
* Build and evaluate expressions.
* Read user input using `Scanner`.
* Write meaningful comments and documentation.
* Apply Java's standard naming conventions.
* Debug basic console applications using both print statements and IntelliJ's debugger.

The next step is the **Module Final Project**, where you'll progressively combine everything learned throughout this module into a complete console application before moving on to Module 02.
