# Chapter 09 — Fibonacci Using Methods

## Overview

In **Module 02**, you learned how to generate the Fibonacci sequence using loops.

Now you'll refactor that solution into reusable methods.

Like the factorial exercise, the algorithm itself doesn't change. What changes is **how you organize it**.

The goal is to separate:

* the logic that generates the sequence;
* the code that displays it;
* the code that interacts with the user.

By the end of this chapter, you'll see how even algorithms that produce multiple values can still be organized into clean, reusable methods.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Move the Fibonacci algorithm into methods.
* Separate sequence generation from presentation.
* Design methods with clear responsibilities.
* Reuse methods to avoid duplicated logic.
* Prepare algorithms for integration into larger programs.

---

# What Is the Fibonacci Sequence?

The Fibonacci sequence starts with:

```text id="jepuh8"
0, 1
```

Every next number is the sum of the previous two.

Example:

```text id="cpx0oq"
0
1
1
2
3
5
8
13
21
34
55
...
```

Visualization:

```text id="fm54qc"
0 + 1 = 1
1 + 1 = 2
1 + 2 = 3
2 + 3 = 5
3 + 5 = 8
```

---

# Reviewing the Algorithm

A common solution is:

```java id="1ujjq2"
int first = 0;
int second = 1;

for (int i = 0; i < 10; i++) {

    System.out.print(first + " ");

    int next = first + second;

    first = second;
    second = next;

}
```

This works well.

Now we'll organize it into methods.

---

# First Refactoring

Instead of placing everything inside `main()`:

```java id="j39v0m"
printFibonacci(10);
```

Method:

```java id="zujwl4"
public static void printFibonacci(int terms) {

    int first = 0;
    int second = 1;

    for (int i = 0; i < terms; i++) {

        System.out.print(first + " ");

        int next = first + second;

        first = second;
        second = next;

    }

}
```

Now the sequence can be generated anywhere in your application with a single method call.

---

# Why Is This Method `void`?

Unlike methods such as:

```java id="t8f83t"
add(5, 8)
```

which produce a **single value**, Fibonacci produces **many values**.

At our current level, printing them directly is a perfectly reasonable design.

Later, when you learn arrays and collections, you'll redesign this method to **return** the sequence instead of printing it.

For now, the focus is on organizing the code.

---

# Building a Report Method

Instead of:

```java id="99um4r"
printFibonacci(10);
```

Create another method:

```java id="a9sqpc"
public static void fibonacciReport(int terms) {

    System.out.println("========================");
    System.out.println("Fibonacci Sequence");
    System.out.println("========================");

    printFibonacci(terms);

    System.out.println();

}
```

Now your application becomes more organized.

---

# Handling Invalid Input

What happens if:

```java id="d47a5x"
printFibonacci(-5);
```

The loop simply doesn't execute.

Although this isn't dangerous, it's not very informative.

A simple validation:

```java id="cjlwmq"
if (terms <= 0) {

    System.out.println("Invalid number of terms.");

    return;

}
```

Notice the use of an **early return**.

If the input is invalid, the method finishes immediately.

---

# Separating Responsibilities

Avoid writing one huge method like this:

```text id="18ok1b"
Read input

↓

Generate sequence

↓

Print title

↓

Print sequence

↓

Print footer
```

Instead, divide the work.

```text id="rjlwmj"
showTitle()

↓

printFibonacci()

↓

showFooter()
```

Or:

```text id="ckvvq8"
fibonacciReport()

↓

printFibonacci()
```

Each method has one responsibility.

---

# Reusing the Method

Imagine your Utility Toolkit has this menu.

```text id="e72yid"
1 - Calculator

2 - Temperature Converter

3 - Number Analyzer

4 - Factorial

5 - Fibonacci
```

When the user chooses option 5:

```java id="rjndg5"
printFibonacci(15);
```

No duplicated algorithm.

Just reuse the existing method.

---

# Thinking Beyond This Module

Currently:

```java id="yp0htq"
printFibonacci(10);
```

prints the sequence.

Later in the Bootcamp, you'll learn to design methods like:

```java id="8lgzot"
int[] fibonacci(int terms)
```

which return an array.

Even later:

```java id="e4t0sz"
List<Integer> fibonacci(int terms)
```

using collections.

The underlying algorithm remains the same.

Only the way data is returned changes.

This demonstrates an important lesson:

> Good algorithms often outlive the technologies used to implement them.

---

# Common Beginner Mistakes

### Incorrect variable update order

Incorrect:

```java id="4vvlsh"
first = second;

second = first + second;
```

After updating `first`, its original value is lost.

Always calculate the next value first.

Correct:

```java id="shc68s"
int next = first + second;

first = second;

second = next;
```

---

### Forgetting to print the current value

Incorrect:

```java id="mu4c6h"
int next = first + second;

first = second;

second = next;

System.out.print(first);
```

This changes the sequence.

Print the current value **before** updating the variables.

---

### Mixing menu code with algorithm code

Avoid:

```java id="n9d3tw"
print menu

↓

read option

↓

generate Fibonacci

↓

print footer
```

inside one method.

Keep each responsibility separate.

---

# Best Practices

✔ Keep the Fibonacci algorithm in its own method.

✔ Validate invalid input.

✔ Use meaningful variable names.

Good:

```java id="vk3gmh"
first
second
next
```

instead of:

```java id="rn8c5r"
a
b
c
```

unless writing very short examples.

✔ Separate the algorithm from presentation.

---

# Exercise 5 — Fibonacci with Methods

Implement:

```java id="b5j21n"
public static void printFibonacci(int terms)
```

Requirements:

* Print the sequence.
* Validate invalid input.
* Use a loop.
* Do not use recursion yet.

---

Create:

```java id="k2rtjlwm"
public static void fibonacciReport(int terms)
```

Example output:

```text id="smu3dw"
========================
Fibonacci Sequence
========================

0 1 1 2 3 5 8 13 21 34

========================
```

---

# Mini Challenge

Create a small menu:

```text id="8g6rwb"
How many Fibonacci terms?

10
```

Then call:

```java id="zcjlwm"
fibonacciReport(terms);
```

Your program should contain methods similar to:

```text id="zc4rqp"
showTitle()

readTerms()

printFibonacci()

fibonacciReport()
```

Notice how `main()` continues becoming smaller and easier to read.

---

# Summary

In this chapter, you learned:

* How to move the Fibonacci algorithm into reusable methods.
* Why some methods remain `void` when they primarily produce output.
* How to validate input before executing an algorithm.
* How to separate sequence generation from presentation.
* How to reuse algorithms throughout larger applications.
* How good program organization makes even familiar algorithms easier to maintain.

---

## Looking Ahead

So far, every method you've created has had a **unique name**.

Examples:

```text id="eqj8a4"
add()

factorial()

isPrime()

printFibonacci()
```

But what if you want multiple methods with the **same name**, as long as they perform similar tasks with different kinds of input?

Java allows this through a feature called **Method Overloading**.

In the next chapter, you'll learn how Java decides **which version of a method to call**, opening the door to writing cleaner and more expressive APIs.
