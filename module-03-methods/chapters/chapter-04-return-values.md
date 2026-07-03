# Chapter 04 — Return Values

## Overview

Until now, every method you've created has been a **`void` method**.

For example:

```java
public static void greet(String name) {
    System.out.println("Hello, " + name + "!");
}
```

This method **performs an action** (printing text), but it doesn't give anything back to the code that called it.

However, many methods exist to **calculate** something rather than display it.

Imagine you want to calculate the area of a rectangle.

Should the method print the result directly?

```java
public static void calculateArea(double width, double height) {
    System.out.println(width * height);
}
```

This works, but what if you want to:

* store the area in a variable?
* compare two areas?
* multiply the area by another value?
* print it later?
* use it in another calculation?

Printing inside the method isn't flexible enough.

Instead, the method should **return** the calculated value.

This is one of the most important concepts in programming.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what a return value is.
* Distinguish between `void` methods and methods that return values.
* Use the `return` keyword.
* Store returned values in variables.
* Use returned values inside expressions.
* Combine multiple methods together.

---

# What Is a Return Value?

A **return value** is information that a method sends back to whoever called it.

Think of a vending machine.

```text
Money
   │
   ▼
+----------------+
| Vending Machine|
+----------------+
   │
   ▼
Snack
```

You provide an input, and the machine gives something back.

A method behaves similarly.

```text
5 and 8
   │
   ▼
add()
   │
   ▼
13
```

The value `13` is the **return value**.

---

# `void` vs Returning Methods

## `void`

A `void` method performs an action but returns nothing.

```java
public static void sayHello() {
    System.out.println("Hello!");
}
```

Calling it:

```java
sayHello();
```

Output:

```text
Hello!
```

---

## Returning Method

A returning method sends a value back.

```java
public static int add(int a, int b) {
    return a + b;
}
```

Calling it:

```java
int result = add(5, 8);

System.out.println(result);
```

Output:

```text
13
```

Notice that **the method does not print anything**.

It only returns the value.

The caller decides what to do with it.

---

# The Return Type

Every method declaration specifies the type of value it returns.

```java
public static int add(int a, int b)
```

The `int` tells Java:

> "This method will return an integer."

Examples:

```java
public static int getAge()
```

Returns an integer.

---

```java
public static double calculateArea(double radius)
```

Returns a `double`.

---

```java
public static boolean isEven(int number)
```

Returns `true` or `false`.

---

```java
public static String getGreeting()
```

Returns a `String`.

---

```java
public static void printMenu()
```

Returns nothing.

---

# The `return` Statement

The `return` keyword immediately ends the method and sends a value back.

Example:

```java
public static int square(int number) {

    return number * number;

}
```

Calling it:

```java
int value = square(6);

System.out.println(value);
```

Output:

```text
36
```

Execution flow:

```text
main()

↓

square(6)

↓

return 36

↓

main() continues
```

After `return`, the method finishes executing.

---

# Storing Returned Values

The returned value can be stored in a variable.

```java
int total = add(10, 20);
```

Now:

```text
total = 30
```

You can use it later.

```java
System.out.println(total);
```

---

# Using Returned Values Directly

You don't always need a variable.

```java
System.out.println(add(5, 3));
```

Output:

```text
8
```

The returned value goes directly into `println()`.

---

# Using Returned Values in Expressions

Methods can participate in larger calculations.

```java
int result = add(2, 3) * 10;
```

Execution:

```text
add(2,3)

↓

5

↓

5 × 10

↓

50
```

This makes returning methods much more powerful than methods that only print.

---

# Combining Methods

Methods can call other methods that return values.

Example:

```java
public static int multiply(int a, int b) {
    return a * b;
}

public static int square(int number) {
    return multiply(number, number);
}
```

Calling:

```java
System.out.println(square(5));
```

Execution:

```text
square(5)

↓

multiply(5,5)

↓

25

↓

return 25
```

This is an example of building larger functionality from smaller, reusable methods.

---

# Multiple Return Points

A method may have more than one `return`.

Example:

```java
public static boolean isPositive(int number) {

    if (number > 0) {
        return true;
    }

    return false;

}
```

A shorter version:

```java
public static boolean isPositive(int number) {
    return number > 0;
}
```

Both are correct.

---

# Returning Early

`return` immediately ends the method.

Example:

```java
public static void checkNumber(int number) {

    if (number < 0) {
        System.out.println("Negative number.");
        return;
    }

    System.out.println("Positive or zero.");

}
```

If `number` is negative:

```text
Negative number.
```

The second `println()` never executes.

---

# Common Beginner Mistakes

### Forgetting to return a value

```java
public static int add(int a, int b) {

}
```

Compilation error.

Java expected an `int` to be returned.

---

### Returning the wrong type

```java
public static int getName() {
    return "Eduardo";
}
```

Compilation error.

Expected:

```text
int
```

Received:

```text
String
```

---

### Trying to store the result of a `void` method

```java
int value = printMenu();
```

Compilation error.

`printMenu()` returns nothing.

---

### Printing instead of returning

```java
public static int add(int a, int b) {

    System.out.println(a + b);

}
```

The method printed the answer but never returned it.

Java will report an error because the declared return type is `int`.

---

# Best Practices

✔ Methods that calculate something should usually **return** the result.

✔ Methods that only display information are often `void`.

✔ Keep responsibilities separate.

Good:

```java
int total = add(5, 8);

System.out.println(total);
```

Instead of mixing calculation and printing unnecessarily.

---

# Exercise 1 — Calculator (Part 1)

Now we'll begin the first core exercise of this module.

Create the following methods:

```java
public static int add(int a, int b)
```

```java
public static int subtract(int a, int b)
```

```java
public static int multiply(int a, int b)
```

```java
public static double divide(int a, int b)
```

Each method should:

* receive two numbers;
* return the calculated result;
* **not print anything**.

---

## Example

```java
int sum = add(10, 5);

System.out.println("Sum: " + sum);
```

Output:

```text
Sum: 15
```

---

# Challenge

Without writing duplicate code, create a program that displays:

```text
Calculator

10 + 5 = 15
10 - 5 = 5
10 * 5 = 50
10 / 5 = 2.0
```

The calculations must come from your methods.

---

# Summary

In this chapter, you learned:

* The difference between `void` methods and methods that return values.
* How to use the `return` keyword.
* How to declare methods with different return types.
* How to store returned values in variables.
* How to use returned values inside expressions.
* How to combine methods to build more complex logic.
* Why separating calculation from output leads to cleaner, more reusable code.

---

## What's Next?

In **Chapter 05 — Variable Scope**, you'll learn why some variables are accessible only inside certain methods, how long variables live, and how Java manages them during program execution. This knowledge is essential before you start building larger applications with many methods.
