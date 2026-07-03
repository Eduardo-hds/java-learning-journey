# Chapter 08 — Factorial Using Methods

## Overview

Back in **Module 02**, you implemented the factorial algorithm using loops.

A typical solution looked something like this:

```java
int number = 5;
int factorial = 1;

for (int i = 1; i <= number; i++) {
    factorial *= i;
}

System.out.println(factorial);
```

The algorithm works perfectly.

However, it has one limitation:

If another part of your program needs to calculate a factorial, you'll probably end up copying the same code again.

This chapter is about **refactoring**—taking existing code and reorganizing it into reusable methods without changing its behavior.

This is one of the most valuable skills a programmer can develop.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Move an algorithm into a reusable method.
* Separate calculation from presentation.
* Reuse methods multiple times.
* Design methods that perform one clear task.
* Prepare existing code for larger applications.

---

# From Algorithm to Method

Instead of writing:

```java
int factorial = 1;

for (int i = 1; i <= number; i++) {
    factorial *= i;
}
```

every time, create a method.

```java
public static long factorial(int number) {

    long result = 1;

    for (int i = 1; i <= number; i++) {
        result *= i;
    }

    return result;

}
```

Now the calculation exists in only one place.

---

# Why Return the Result?

Imagine two versions.

### Version A

```java
public static void factorial(int number) {

    long result = 1;

    for (int i = 1; i <= number; i++) {
        result *= i;
    }

    System.out.println(result);

}
```

This only prints the answer.

---

### Version B

```java
public static long factorial(int number) {

    long result = 1;

    for (int i = 1; i <= number; i++) {
        result *= i;
    }

    return result;

}
```

Now you can:

```java
System.out.println(factorial(5));
```

or

```java
long value = factorial(8);
```

or

```java
if (factorial(5) > 100) {
    System.out.println("Large value");
}
```

Returning values makes the method much more useful.

---

# Why Use `long` Instead of `int`?

Factorials grow **extremely quickly**.

Examples:

```text
5!  = 120
10! = 3,628,800
15! = 1,307,674,368,000
20! = 2,432,902,008,176,640,000
```

An `int` can store values only up to:

```text
2,147,483,647
```

A `long` can store much larger values:

```text
9,223,372,036,854,775,807
```

Even `long` has limits—`21!` is already too large—but it's sufficient for this exercise.

---

# Step-by-Step Execution

Suppose:

```java
factorial(5);
```

Execution:

```text
result = 1

↓

1 × 1 = 1

↓

1 × 2 = 2

↓

2 × 3 = 6

↓

6 × 4 = 24

↓

24 × 5 = 120

↓

return 120
```

---

# Handling Special Cases

What is:

```text
0!
```

By mathematical definition:

```text
0! = 1
```

Our method already works correctly.

Why?

Because:

```java
for (int i = 1; i <= number; i++)
```

If `number` is `0`, the loop never executes.

`result` remains:

```text
1
```

Exactly what we want.

---

# Negative Numbers

Should factorial accept negative numbers?

No.

Factorial is defined only for non-negative integers.

A simple validation:

```java
if (number < 0) {
    return -1;
}
```

Then:

```java
if (factorial(number) == -1) {
    System.out.println("Invalid input.");
}
```

> **Note:** Later in the Bootcamp, you'll learn better ways to report invalid input using exceptions. For now, returning `-1` is a simple way to indicate an error.

---

# Reusing the Method

Imagine your Utility Toolkit contains:

* Calculator
* Number Analyzer
* Factorial
* Fibonacci

Whenever the user selects "Factorial":

```java
System.out.println(factorial(number));
```

No duplicated logic.

One method.

Many uses.

---

# Building Larger Methods

Instead of mixing everything together:

```java
public static void factorialMenu() {

    // read input

    // calculate factorial

    // print result

}
```

Split responsibilities.

```text
factorial()

↓

printFactorial()

↓

factorialMenu()
```

Each method has one clear purpose.

---

# Common Beginner Mistakes

### Returning inside the loop

Incorrect:

```java
for (int i = 1; i <= number; i++) {

    result *= i;

    return result;

}
```

This returns after the **first iteration**.

The complete calculation never happens.

---

### Forgetting to initialize with `1`

Incorrect:

```java
long result = 0;
```

Multiplication by zero always produces zero.

Correct:

```java
long result = 1;
```

---

### Printing instead of returning

Avoid:

```java
System.out.println(result);
```

inside the calculation method.

Let the caller decide when and where to display the value.

---

# Best Practices

✔ Keep calculation separate from output.

✔ Return the computed value.

✔ Validate invalid input when appropriate.

✔ Choose a data type large enough for the expected result.

✔ Reuse the method instead of rewriting the algorithm.

---

# Exercise 4 — Factorial with Methods

Implement:

```java
public static long factorial(int number)
```

Requirements:

* Accept an integer.
* Return the factorial.
* Return `-1` for negative numbers.
* Use a loop (do **not** use recursion yet).

---

Create a demonstration program.

Example:

```text
Factorial Calculator

5! = 120
8! = 40320
0! = 1
-3 -> Invalid input
```

---

# Mini Challenge

Create:

```java
public static void printFactorialReport(int number)
```

Example output:

```text
========================
Factorial Calculator
========================

Input : 6
Result: 720

========================
```

The report method should call:

```java
factorial(number)
```

It should **not** contain the factorial algorithm itself.

---

# Summary

In this chapter, you learned:

* How to refactor an existing algorithm into a reusable method.
* Why calculation methods should return values instead of printing them.
* Why `long` is more appropriate than `int` for factorials.
* How to handle edge cases like `0!`.
* How to deal with invalid input.
* How to separate calculation from presentation.
* How reusable methods reduce duplicated code and simplify larger applications.

---

## Looking Ahead

You've now transformed one of your previous Module 02 exercises into a reusable component.

In the next chapter, you'll do exactly the same with another classic algorithm:

**The Fibonacci sequence.**

This time, you'll learn how to organize sequence generation into methods that can be reused throughout your Utility Toolkit, further strengthening your ability to write clean, modular programs.
