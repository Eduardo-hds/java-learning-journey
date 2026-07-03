# Chapter 07 — Number Analysis with Methods

## Overview

In the previous chapter, you built methods that **transformed** data:

```text
25°C → 77°F
```

Now you'll build methods that **analyze** data.

Instead of asking:

> "What is the converted temperature?"

You'll ask questions like:

* Is this number even?
* Is it positive?
* Is it prime?

Methods that answer questions usually return a **boolean** (`true` or `false`), making them incredibly useful in conditions like `if` statements.

This chapter also begins **Exercise 3 — Number Analyzer**, one of the core projects of this module.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Create methods that return `boolean`.
* Build reusable decision-making methods.
* Combine multiple methods.
* Separate analysis from output.
* Organize logical checks into independent methods.

---

# Methods That Answer Questions

Consider this method:

```java
public static boolean isEven(int number) {
    return number % 2 == 0;
}
```

It doesn't print anything.

Instead, it answers a question.

Example:

```java
System.out.println(isEven(8));
```

Output:

```text
true
```

Another example:

```java
System.out.println(isEven(5));
```

Output:

```text
false
```

---

# Why Return `boolean`?

Imagine two different designs.

### Version A

```java
public static void checkEven(int number) {

    if (number % 2 == 0) {
        System.out.println("Even");
    } else {
        System.out.println("Odd");
    }

}
```

Works...

...but you can only print the result.

---

### Version B

```java
public static boolean isEven(int number) {

    return number % 2 == 0;

}
```

Now you can do much more.

Example:

```java
if (isEven(number)) {

    System.out.println("Even");

}
```

Or:

```java
boolean result = isEven(10);
```

Or:

```java
while (!isEven(number)) {

    number++;

}
```

Returning information makes methods reusable in many situations.

---

# Exercise 3 — Part 1: Even or Odd

Create:

```java
public static boolean isEven(int number) {

    return number % 2 == 0;

}
```

Example:

```java
int value = 14;

if (isEven(value)) {

    System.out.println("Even");

} else {

    System.out.println("Odd");

}
```

Output:

```text
Even
```

---

# Positive, Negative, or Zero

This analysis has three possible results.

One approach is to return a `String`.

```java
public static String numberType(int number) {

    if (number > 0) {
        return "Positive";
    }

    if (number < 0) {
        return "Negative";
    }

    return "Zero";

}
```

Usage:

```java
System.out.println(numberType(-8));
```

Output:

```text
Negative
```

---

# Why Return a String Here?

Unlike "even or odd," this method has **three** possible answers.

Returning a `boolean` wouldn't be enough.

Returning a `String` makes the result easy to display and understand.

---

# Prime Number Analysis

A prime number:

* is greater than 1;
* has exactly two divisors:

  * 1
  * itself

Examples:

```text
2 ✔
3 ✔
5 ✔
7 ✔
11 ✔
13 ✔
```

Not prime:

```text
1 ✘
4 ✘
6 ✘
8 ✘
9 ✘
10 ✘
```

---

# Building `isPrime()`

Start by eliminating impossible cases.

```java
if (number <= 1) {
    return false;
}
```

Now check whether another number divides it exactly.

```java
for (int i = 2; i < number; i++) {

    if (number % i == 0) {
        return false;
    }

}
```

If no divisor is found:

```java
return true;
```

Complete method:

```java
public static boolean isPrime(int number) {

    if (number <= 1) {
        return false;
    }

    for (int i = 2; i < number; i++) {

        if (number % i == 0) {
            return false;
        }

    }

    return true;

}
```

---

# Understanding Early Returns

Imagine checking whether 12 is prime.

Execution:

```text
isPrime(12)

↓

i = 2

↓

12 % 2 == 0

↓

return false
```

The loop stops immediately.

There is no reason to continue checking.

This makes the method efficient and easy to read.

---

# Combining Methods

Methods become powerful when used together.

Example:

```java
public static void analyzeNumber(int number) {

    System.out.println("Number: " + number);

    if (isEven(number)) {
        System.out.println("Even");
    } else {
        System.out.println("Odd");
    }

    System.out.println(numberType(number));

    if (isPrime(number)) {
        System.out.println("Prime");
    } else {
        System.out.println("Not prime");
    }

}
```

Notice that `analyzeNumber()` doesn't contain the logic for checking parity or primality.

It delegates those responsibilities to other methods.

This keeps the code clean and modular.

---

# Thinking in Small Methods

Instead of writing one huge method:

```text
analyzeEverything()
```

Break the work into specialized methods:

```text
analyzeNumber()

├── isEven()
├── numberType()
└── isPrime()
```

This is much easier to maintain.

---

# Common Beginner Mistakes

### Printing instead of returning

```java
public static boolean isEven(int number) {

    System.out.println(number % 2 == 0);

}
```

Compilation error.

The method declared `boolean` but never returned a value.

---

### Forgetting numbers less than or equal to 1

```java
isPrime(1)
```

If you skip the initial check, your method may incorrectly return `true`.

Always handle edge cases first.

---

### Mixing multiple responsibilities

Avoid methods like:

```java
checkNumberAndPrintEverything()
```

Instead:

```text
isEven()

numberType()

isPrime()

analyzeNumber()
```

Each method has a single responsibility.

---

# Best Practices

✔ Methods that answer questions should usually return `boolean`.

✔ Keep analysis separate from presentation.

✔ Handle special cases first (like numbers less than or equal to 1).

✔ Reuse methods instead of rewriting logic.

✔ Build larger methods by combining smaller ones.

---

# Exercise 3 — Number Analyzer

Implement the following methods:

```java
public static boolean isEven(int number)
```

```java
public static String numberType(int number)
```

Returns:

* `"Positive"`
* `"Negative"`
* `"Zero"`

---

```java
public static boolean isPrime(int number)
```

---

Then create:

```java
public static void analyzeNumber(int number)
```

Example output:

```text
Number: 17
Odd
Positive
Prime
```

---

# Mini Challenge

Modify `analyzeNumber()` so it prints a decorative report.

Example:

```text
========================
Number Analyzer
========================

Number: 25

Parity : Odd
Sign   : Positive
Prime  : No

========================
```

Notice that the report method doesn't perform the calculations.

It simply calls the helper methods and displays their results.

---

# Summary

In this chapter, you learned:

* How to create methods that return `boolean`.
* When to return a `String` instead of a `boolean`.
* How to implement `isEven()`, `numberType()`, and `isPrime()`.
* How to combine multiple helper methods into a larger analysis method.
* The importance of separating logic from presentation.
* How modular methods make programs easier to read, test, and maintain.

---

## Optimization Note (Preview)

The current implementation of `isPrime()` checks every number from `2` to `number - 1`.

This is correct for learning purposes, but it's **not the most efficient**.

Later in your Java journey, you'll optimize it by checking only up to the square root of the number (`√n`), greatly improving performance for large numbers.

For now, the current version is the best choice because it prioritizes **clarity over optimization**, which is exactly what you should focus on at this stage.

---

## What's Next?

In **Chapter 08 — Factorial Using Methods**, you'll take an algorithm you've already written in Module 02 and refactor it into reusable methods, reinforcing one of the most important skills in software development: transforming working code into clean, modular, and reusable code.
