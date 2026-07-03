# Chapter 3 — Primitive Data Types

## Overview

Imagine trying to store every piece of information in a program exactly the same way.

A person's age, a bank account balance, a letter, and a true/false answer are all different kinds of data. They require different amounts of memory and different operations.

This is why programming languages use **data types**.

In this chapter, you'll learn what primitive data types are, why they exist, how Java stores them in memory, and when to use each one.

---

# Why Do Data Types Exist?

Computers only understand **binary** (0s and 1s).

Everything—a number, a letter, an image, or a video—is ultimately represented as binary.

However, the CPU needs to know **how to interpret those bits**.

For example:

```text
00000001
```

Depending on the data type, those same bits could represent:

* The integer `1`
* The character `SOH` (Start of Heading in ASCII)
* Part of a floating-point number
* A boolean value (depending on implementation)

Without a data type, Java wouldn't know how to interpret the stored bits.

---

# What Is a Primitive Data Type?

A **primitive data type** is one of Java's built-in types that stores a single value directly.

Primitive types are:

* Simple
* Fast
* Memory-efficient

Unlike objects (which you'll learn in later modules), primitive values are stored directly, not as collections of data and behavior.

Java has **8 primitive data types**.

| Category  | Types                          |
| --------- | ------------------------------ |
| Integer   | `byte`, `short`, `int`, `long` |
| Decimal   | `float`, `double`              |
| Character | `char`                         |
| Logical   | `boolean`                      |

---

# Integer Types

Integers store **whole numbers** (no decimal places).

Examples:

```text
-100
0
25
9999
```

Java provides four integer types.

---

## `byte`

Size:

```text
8 bits (1 byte)
```

Range:

```text
-128 to 127
```

Example:

```java
byte age = 25;
```

Because it uses only one byte, it is memory-efficient.

Typical uses:

* Binary data
* File processing
* Network protocols
* Large arrays where memory matters

It is **rarely used** in everyday business applications.

---

## `short`

Size:

```text
16 bits (2 bytes)
```

Range:

```text
-32,768 to 32,767
```

Example:

```java
short year = 2026;
```

Also uncommon in modern Java applications.

---

## `int`

Size:

```text
32 bits (4 bytes)
```

Range:

```text
-2,147,483,648 to 2,147,483,647
```

Example:

```java
int population = 500000;
```

This is the **default integer type** in Java.

If you need an integer and don't have a special reason to choose another type, use `int`.

---

## `long`

Size:

```text
64 bits (8 bytes)
```

Range:

Approximately:

```text
±9 quintillion
```

Example:

```java
long distance = 384400000L;
```

Notice the `L` at the end.

Without it:

```java
long value = 5000000000;
```

Compilation error.

Correct:

```java
long value = 5000000000L;
```

Use `long` when `int` isn't large enough.

Examples:

* Milliseconds since 1970
* Database IDs
* Population statistics
* File sizes

---

# Floating-Point Types

Floating-point numbers contain decimal values.

Example:

```text
3.14
10.5
0.25
```

Java provides two types.

---

## `float`

Size:

```text
32 bits
```

Precision:

Approximately **7 decimal digits**.

Example:

```java
float price = 19.99F;
```

Notice the `F`.

Without it:

```java
float price = 19.99;
```

Compilation error, because decimal literals are `double` by default.

`float` is mostly used when saving memory is more important than precision.

---

## `double`

Size:

```text
64 bits
```

Precision:

Approximately **15–16 decimal digits**.

Example:

```java
double temperature = 21.5;
```

This is the **default decimal type** in Java.

Whenever you need decimal numbers, prefer `double` unless you have a specific reason to use `float`.

---

# Why Not Use `double` for Money?

You might think:

> "Money has decimals, so `double` is perfect."

Actually, **no**.

Example:

```java
System.out.println(0.1 + 0.2);
```

Output:

```text
0.30000000000000004
```

This happens because floating-point numbers are stored in **binary**, and many decimal fractions cannot be represented exactly.

Professional Java applications use `BigDecimal` for financial calculations.

You'll learn about it in a later module.

---

# `char`

A `char` stores **a single Unicode character**.

Size:

```text
16 bits
```

Examples:

```java
char grade = 'A';
char symbol = '$';
char letter = 'J';
```

Notice:

Characters use **single quotes**.

Correct:

```java
char letter = 'A';
```

Incorrect:

```java
char letter = "A";
```

Double quotes create a `String`, not a `char`.

---

# Unicode

Java uses **Unicode**, allowing it to represent characters from many languages.

Examples:

```java
char japanese = '日';
char greek = 'Ω';
char emoji = '❤';
```

This makes Java suitable for international applications.

---

# `boolean`

A `boolean` stores only two possible values:

```text
true
false
```

Example:

```java
boolean isStudent = true;
```

Common uses:

* Login status
* Permissions
* Validation
* Comparisons
* Conditions

You'll use `boolean` extensively when learning control flow in the next module.

---

# Summary Table

| Type      |                         Size | Example       |
| --------- | ---------------------------: | ------------- |
| `byte`    |                       1 byte | `100`         |
| `short`   |                      2 bytes | `30000`       |
| `int`     |                      4 bytes | `500000`      |
| `long`    |                      8 bytes | `5000000000L` |
| `float`   |                      4 bytes | `19.99F`      |
| `double`  |                      8 bytes | `19.99`       |
| `char`    |                      2 bytes | `'A'`         |
| `boolean` | JVM-dependent representation | `true`        |

> Although a `boolean` conceptually represents a single true/false value, the Java Language Specification does **not** define its exact memory size. The JVM implementation decides how it is stored internally.

---

# Choosing the Right Type

A good rule of thumb:

| Situation           | Recommended Type |
| ------------------- | ---------------- |
| Whole numbers       | `int`            |
| Very large integers | `long`           |
| Decimal numbers     | `double`         |
| One character       | `char`           |
| True/False values   | `boolean`        |

You'll rarely need `byte`, `short`, or `float` in everyday application development.

---

# Common Beginner Mistakes

### Forgetting `L`

Incorrect:

```java
long distance = 5000000000;
```

Correct:

```java
long distance = 5000000000L;
```

---

### Forgetting `F`

Incorrect:

```java
float value = 3.14;
```

Correct:

```java
float value = 3.14F;
```

---

### Mixing `char` and `String`

Incorrect:

```java
char letter = "A";
```

Correct:

```java
char letter = 'A';
```

---

### Using `double` for Financial Values

Possible:

```java
double balance = 10.10;
```

Professional applications instead use `BigDecimal` to avoid rounding errors.

---

# Best Practices

* Use `int` for most integer values.
* Use `double` for most decimal values.
* Use `long` only when values exceed the `int` range.
* Use meaningful variable names.
* Avoid optimizing memory prematurely by choosing smaller types unless necessary.

---

# Guided Exercise

Create a program called `PrimitiveTypesDemo.java`.

Declare one variable of each primitive type:

* `byte`
* `short`
* `int`
* `long`
* `float`
* `double`
* `char`
* `boolean`

Assign a value to each one and print them to the console with descriptive labels.

Example output:

```text
Byte: 100
Short: 2000
Int: 500000
Long: 5000000000
Float: 3.14
Double: 3.1415926535
Char: J
Boolean: true
```

---

# Independent Exercises

## Easy

Create a program that stores:

* Your age (`int`)
* Your height (`double`)
* The first letter of your name (`char`)

Print all three values.

---

## Medium

Create a program representing a car.

Store:

* Model (`String` — we'll discuss this type in detail later)
* Year (`int`)
* Price (`double`)
* Automatic transmission (`boolean`)

Print the information neatly.

> For now, just use `String` as shown without worrying about why it isn't a primitive type. We'll study it in depth later.

---

## Hard

Create a program called `GameCharacter.java`.

Store at least:

* Name (`String`)
* Level (`int`)
* Health points (`int`)
* Attack damage (`double`)
* Rank (`char`)
* IsAlive (`boolean`)

Print a formatted character sheet.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

1. Why do data types exist?
2. How many primitive data types does Java have?
3. Which type is the default for whole numbers?
4. Which type is the default for decimal numbers?
5. When should you use `long` instead of `int`?
6. Why must a `long` literal end with `L` in some cases?
7. Why must a `float` literal end with `F`?
8. What is the difference between `char` and `String`?
9. Why is `double` not recommended for financial calculations?
10. Which primitive type stores only `true` or `false`?

---

# Chapter Summary

In this chapter, you learned:

* Why Java needs data types.
* The difference between integer, decimal, character, and logical types.
* The purpose and characteristics of all eight primitive data types.
* Which types are commonly used in professional development.
* Common mistakes involving `long`, `float`, and `char`.
* Why `BigDecimal` is preferred for money instead of `double`.

---

## Progress Checkpoint

Before moving on to **Chapter 4 — Literals and Numeric Representations**, make sure you can:

* Identify all eight primitive data types.
* Choose an appropriate type for different kinds of data.
* Explain the difference between `int`, `long`, `float`, and `double`.
* Distinguish `char` from `String`.
* Understand why Java uses different data types instead of storing everything the same way.
