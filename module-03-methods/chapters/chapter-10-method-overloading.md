# Chapter 10 — Method Overloading

## Overview

Up to this point, every method in your programs has had a **unique name**.

For example:

```java
add(int a, int b)
```

```java
multiply(int a, int b)
```

```java
factorial(int number)
```

```java
isPrime(int number)
```

But what if you want methods that perform the **same kind of operation**, just with different types or different numbers of parameters?

For example:

```java
sum(5, 10)
```

```java
sum(2.5, 7.8)
```

```java
sum(1, 2, 3)
```

Should you create methods like:

```java
sumInt()
sumDouble()
sumThreeNumbers()
```

You could...

But Java offers a much cleaner solution:

**Method Overloading.**

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what method overloading is.
* Create overloaded methods.
* Understand how Java chooses which method to execute.
* Recognize valid and invalid overloads.
* Apply overloading to build cleaner APIs.

---

# What Is Method Overloading?

Method overloading means:

> **Having multiple methods with the same name but different parameter lists.**

Example:

```java
public static int sum(int a, int b) {
    return a + b;
}
```

```java
public static double sum(double a, double b) {
    return a + b;
}
```

Both methods are called:

```text
sum
```

But Java knows which one to use based on the arguments.

---

# First Example

```java
public static int sum(int a, int b) {
    return a + b;
}

public static double sum(double a, double b) {
    return a + b;
}
```

Calling:

```java
System.out.println(sum(5, 3));
```

Output:

```text
8
```

Calling:

```java
System.out.println(sum(2.5, 4.8));
```

Output:

```text
7.3
```

Java automatically selects the correct version.

---

# How Java Chooses

When you write:

```java
sum(5, 3);
```

Java searches for:

```text
sum(int, int)
```

When you write:

```java
sum(2.5, 3.8);
```

Java searches for:

```text
sum(double, double)
```

The parameter list determines which method is called.

---

# Overloading with Different Numbers of Parameters

Example:

```java
public static int sum(int a, int b) {
    return a + b;
}
```

```java
public static int sum(int a, int b, int c) {
    return a + b + c;
}
```

Usage:

```java
sum(2, 3);
```

↓

```text
5
```

---

```java
sum(2, 3, 4);
```

↓

```text
9
```

Again, Java selects the appropriate version.

---

# Overloading with Different Types

Example:

```java
public static void printValue(int value) {
    System.out.println("Integer: " + value);
}
```

```java
public static void printValue(double value) {
    System.out.println("Double: " + value);
}
```

```java
public static void printValue(String value) {
    System.out.println("Text: " + value);
}
```

Usage:

```java
printValue(10);
printValue(8.5);
printValue("Java");
```

Output:

```text
Integer: 10
Double: 8.5
Text: Java
```

---

# Method Signature Revisited

Recall from Chapter 02:

A method signature consists of:

* Method name
* Parameter types
* Parameter order
* Number of parameters

The **return type is NOT part of the signature**.

---

## Invalid Overloading

This is **not allowed**:

```java
public static int sum(int a, int b) {
    return a + b;
}
```

```java
public static double sum(int a, int b) {
    return a + b;
}
```

Compilation error.

Why?

Because both methods have the same signature:

```text
sum(int, int)
```

Changing only the return type does **not** create a new overload.

---

# Parameter Order

Different parameter orders also create different signatures.

Example:

```java
show(String text, int number)
```

Different from:

```java
show(int number, String text)
```

Although valid, this kind of overloading is often confusing.

Prefer overloads that improve readability.

---

# Exercise 6 — Part 1: Sum

Create these methods:

```java
public static int sum(int a, int b)
```

```java
public static int sum(int a, int b, int c)
```

```java
public static double sum(double a, double b)
```

Example:

```java
sum(5, 3);
```

↓

```text
8
```

---

```java
sum(5, 3, 2);
```

↓

```text
10
```

---

```java
sum(2.5, 3.5);
```

↓

```text
6.0
```

---

# Exercise 6 — Part 2: Printing Values

Create overloaded methods:

```java
printValue(int value)
```

```java
printValue(double value)
```

```java
printValue(boolean value)
```

```java
printValue(String value)
```

Each should clearly identify the type being printed.

Example:

```text
Integer: 15
```

```text
Double: 9.8
```

```text
Boolean: true
```

```text
Text: Hello
```

---

# Exercise 6 — Part 3: Area Calculations

Create overloaded methods named:

```java
area(...)
```

Rectangle:

```java
area(double width, double height)
```

Formula:

```text
width × height
```

---

Square:

```java
area(double side)
```

Formula:

```text
side × side
```

---

Circle:

```java
area(double radius, boolean circle)
```

Formula:

```text
π × radius²
```

For now, the `boolean` parameter exists only to create a different signature. Later, you'll learn better design approaches using Object-Oriented Programming.

---

# Overload Resolution

Imagine these methods:

```java
sum(int, int)
```

```java
sum(double, double)
```

Calling:

```java
sum(5, 8);
```

Java selects:

```text
sum(int, int)
```

Calling:

```java
sum(5.0, 8.0);
```

Java selects:

```text
sum(double, double)
```

The compiler performs this decision **before the program runs**.

---

# Common Beginner Mistakes

### Trying to overload by return type

❌ Invalid:

```java
int calculate(int x)
```

```java
double calculate(int x)
```

Same signature.

Compilation error.

---

### Giving overloaded methods unrelated purposes

Avoid:

```java
print()

calculate()

save()

```

all using the same name for unrelated tasks.

Overloaded methods should represent **the same conceptual operation**.

---

### Creating confusing overloads

Example:

```java
show(int, String)
```

```java
show(String, int)
```

Although legal, these are easy to misuse.

Prefer clarity over cleverness.

---

# Best Practices

✔ Overload methods only when they perform the same logical operation.

✔ Keep behavior consistent across overloads.

✔ Avoid overloads that differ only by parameter order.

✔ Never rely on the return type to distinguish overloads.

✔ Choose method names that clearly describe the operation.

---

# Summary

In this chapter, you learned:

* What method overloading is.
* How Java distinguishes overloaded methods.
* Why the return type is not part of a method's signature.
* How to overload methods using different parameter types and counts.
* How to design clear and consistent overloaded methods.
* How overloading improves code readability and usability.

---

# Mini Challenge

Create a small **Geometry Calculator**.

Your `main()` should call different versions of:

```java
area(...)
```

Example:

```text
Square Area: 25.0

Rectangle Area: 24.0

Circle Area: 78.54
```

Notice how all calculations use the same method name, making the code expressive and easy to read.

---

## What's Next?

In **Chapter 11 — Variable Arguments (Varargs)**, you'll learn how to create methods that accept **an unknown number of arguments**.

Instead of writing:

```java
sum(1, 2);
sum(1, 2, 3);
sum(1, 2, 3, 4);
```

you'll be able to write **a single method** that handles them all using Java's `...` (varargs) syntax. This feature builds naturally on everything you've learned about methods and parameters so far.
