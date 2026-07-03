# Chapter 11 — Variable Arguments (Varargs)

## Overview

In the previous chapter, you learned **method overloading**.

For example:

```java
sum(5, 10);
sum(5, 10, 15);
sum(5, 10, 15, 20);
```

One way to support these calls is to create many overloaded methods:

```java
sum(int a, int b)

sum(int a, int b, int c)

sum(int a, int b, int c, int d)

sum(int a, int b, int c, int d, int e)
```

But what if you wanted to sum **100 numbers**?

Creating dozens of overloads would be impractical.

Java solves this with **Variable Arguments**, commonly called **Varargs**.

A varargs parameter allows a method to receive **zero or more arguments** of the same type.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what varargs are.
* Declare methods using `...`.
* Pass any number of arguments to a method.
* Understand how Java treats varargs internally.
* Know the limitations and best practices of varargs.

---

# What Are Varargs?

A varargs parameter lets you write one method that accepts many arguments.

Instead of:

```java
sum(5, 10);
sum(5, 10, 15);
sum(5, 10, 15, 20);
```

You write only one method:

```java
public static int sum(int... numbers)
```

Notice the syntax:

```java
int...
```

The three dots (`...`) mean:

> "This method can receive any number of `int` values."

---

# First Example

```java
public static int sum(int... numbers) {

    int total = 0;

    for (int number : numbers) {
        total += number;
    }

    return total;

}
```

Now you can call:

```java
sum();
```

```java
sum(5);
```

```java
sum(5, 10);
```

```java
sum(5, 10, 15, 20);
```

All of them call **the same method**.

---

# How Does It Work?

Internally, Java treats a varargs parameter as an **array**.

This method:

```java
public static int sum(int... numbers)
```

is handled by Java almost like:

```java
public static int sum(int[] numbers)
```

This is why you can loop through it:

```java
for (int number : numbers) {
    total += number;
}
```

You don't have to create the array yourself—Java does it automatically.

---

# Calling Varargs Methods

Examples:

```java
System.out.println(sum());
```

Output:

```text
0
```

---

```java
System.out.println(sum(5));
```

Output:

```text
5
```

---

```java
System.out.println(sum(5, 10));
```

Output:

```text
15
```

---

```java
System.out.println(sum(5, 10, 15));
```

Output:

```text
30
```

---

# Varargs with Strings

Varargs work with any type.

Example:

```java
public static void printNames(String... names) {

    for (String name : names) {
        System.out.println(name);
    }

}
```

Calling:

```java
printNames("Alice", "Bob", "Charlie");
```

Output:

```text
Alice
Bob
Charlie
```

---

# Mixing Regular Parameters and Varargs

A varargs parameter doesn't have to be the only parameter.

Example:

```java
public static void printLine(String title, int... values)
```

Usage:

```java
printLine("Scores", 10, 20, 30);
```

Inside the method:

* `title` receives:

```text
Scores
```

* `values` receives:

```text
10, 20, 30
```

---

# Important Rule

The varargs parameter **must always be the last parameter**.

Correct:

```java
public static void example(String title, int... values)
```

Incorrect:

```java
public static void example(int... values, String title)
```

Compilation error.

Java wouldn't know where the variable arguments end.

---

# Varargs vs Overloading

Without varargs:

```java
sum(int a, int b)

sum(int a, int b, int c)

sum(int a, int b, int c, int d)

sum(int a, int b, int b, int c, int d, int e)
```

With varargs:

```java
sum(int... numbers)
```

One method replaces many overloads.

---

# When Should You Use Varargs?

Good use cases:

* Sum many numbers.
* Print multiple values.
* Process lists of names.
* Handle optional groups of values.

Poor use cases:

* When the method always requires a fixed number of arguments.
* When different parameter counts represent different operations.

For example:

```java
area(width, height)
```

and

```java
area(radius)
```

should remain overloaded methods, not varargs.

---

# Exercise — Sum Using Varargs

Replace your overloaded `sum()` methods with one method:

```java
public static int sum(int... numbers)
```

Example:

```java
sum(5, 8);
```

↓

```text
13
```

---

```java
sum(5, 8, 10, 12);
```

↓

```text
35
```

---

```java
sum();
```

↓

```text
0
```

---

# Exercise — Print Values

Create:

```java
public static void printValues(int... values)
```

Calling:

```java
printValues(5, 10, 15, 20);
```

Output:

```text
5
10
15
20
```

---

# Exercise — Average

Create:

```java
public static double average(double... values)
```

Example:

```java
average(8.0, 9.5, 10.0);
```

Output:

```text
9.166666666666666
```

> **Challenge:** What should happen if the user calls `average()` with **no arguments**? Think about how you can avoid dividing by zero.

A common solution is:

```java
if (values.length == 0) {
    return 0;
}
```

---

# Common Beginner Mistakes

### Declaring two varargs parameters

Incorrect:

```java
public static void example(int... a, int... b)
```

Compilation error.

A method can have **only one** varargs parameter.

---

### Placing varargs first

Incorrect:

```java
public static void example(int... numbers, String title)
```

Compilation error.

Varargs must be the **last** parameter.

---

### Forgetting that varargs are arrays

This works:

```java
numbers.length
```

Because internally, `numbers` is an array.

---

# Best Practices

✔ Use varargs only when the number of arguments is naturally variable.

✔ Don't replace every overload with varargs—sometimes fixed parameters are clearer.

✔ Handle the case where no arguments are passed.

✔ Remember that varargs are arrays, so you can iterate over them using a `for-each` loop.

✔ Keep method responsibilities focused, even when using varargs.

---

# Summary

In this chapter, you learned:

* What varargs (`...`) are.
* How to declare methods with variable arguments.
* How Java internally treats varargs as arrays.
* Why the varargs parameter must be last.
* When varargs are appropriate and when overloading is a better choice.
* How varargs simplify APIs that accept many values.

---

# Mini Challenge

Expand your **Utility Toolkit** by creating a simple statistics utility.

Implement these methods:

```java
sum(int... numbers)
```

```java
average(double... values)
```

```java
printValues(int... values)
```

Example output:

```text
Values: 10 20 30 40

Sum: 100

Average: 25.0
```

Notice how a single method can now process **any number of values**, making your code much more flexible than creating many overloaded methods.

---

## What's Next?

In the **final chapter of this module**, you'll learn **Recursion**—a technique where a method calls **itself**.

You'll discover:

* how recursive methods work;
* what a **base case** is;
* what a **recursive case** is;
* how recursion compares to iterative solutions (loops);
* when recursion is appropriate and when it should be avoided.

Recursion is one of the most important programming concepts and serves as an excellent conclusion to everything you've learned about methods in this module.
