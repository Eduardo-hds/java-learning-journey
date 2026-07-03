# Chapter 5 — Type Casting

## Overview

Not all values fit into every data type.

Sometimes you need to convert an `int` into a `double`, or a `double` into an `int`. This process is called **type casting**.

Understanding type casting is essential because it affects how data is stored, how calculations are performed, and whether information can be lost during a conversion.

By the end of this chapter, you'll know when Java performs conversions automatically, when you must perform them manually, and what risks are involved.

---

# Why Does Type Casting Exist?

Imagine you have the following code:

```java
int age = 25;
double value = age;
```

Should Java allow this?

Yes, because every integer can be represented exactly as a decimal number.

Now consider the opposite:

```java
double price = 19.99;
int total = price;
```

Should Java allow this automatically?

No.

An `int` cannot store decimal places. Java would have to throw away part of the value, which could lead to bugs.

This is why Java distinguishes between **automatic** and **manual** conversions.

---

# What Is Type Casting?

**Type casting** is the process of converting a value from one data type to another.

There are two categories:

* **Implicit Casting (Widening)**
* **Explicit Casting (Narrowing)**

---

# Implicit Casting (Widening)

A widening conversion happens when Java converts a **smaller type into a larger type**.

Example:

```java
int number = 10;
double value = number;
```

Output:

```text
10.0
```

Java performs this conversion automatically because no information is lost.

---

## Why Is It Called "Widening"?

Imagine pouring water from a small glass into a larger bottle.

Everything fits.

The larger container has enough space to hold the original value.

Example conversions:

```text
byte
   ↓
short
   ↓
int
   ↓
long
   ↓
float
   ↓
double
```

Each step moves to a type capable of representing a wider range of values.

---

# Examples of Implicit Casting

```java
byte a = 10;
int b = a;
```

---

```java
int x = 50;
long y = x;
```

---

```java
long distance = 1000L;
double result = distance;
```

All of these are safe conversions.

---

# Explicit Casting (Narrowing)

A narrowing conversion happens when converting a **larger type into a smaller type**.

Example:

```java
double price = 19.99;

int value = (int) price;
```

Output:

```text
19
```

The decimal part is discarded.

Because information may be lost, Java requires the programmer to explicitly acknowledge the conversion.

---

# Why Is It Called "Narrowing"?

Imagine pouring water from a large bottle into a much smaller glass.

Not everything fits.

Some information may be lost.

---

# Syntax

```java
(targetType) value
```

Example:

```java
double number = 9.8;

int integer = (int) number;
```

---

# Truncation

One common misconception is that Java rounds decimal values during casting.

It does **not**.

Example:

```java
double value = 9.99;

int result = (int) value;
```

Output:

```text
9
```

Another example:

```java
double value = 1.999;

int result = (int) value;
```

Output:

```text
1
```

Java simply removes the fractional part.

---

# Overflow

Casting can also produce unexpected results when the destination type cannot represent the original value.

Example:

```java
int number = 130;

byte result = (byte) number;
```

Output:

```text
-126
```

Why?

A `byte` can only store values from:

```text
-128 to 127
```

The value wraps around because it exceeds the available range.

This behavior is called **overflow**.

---

# Character and Integer Conversion

Characters are internally represented using **Unicode code points**.

Example:

```java
char letter = 'A';

int code = letter;

System.out.println(code);
```

Output:

```text
65
```

The reverse also works:

```java
int code = 66;

char letter = (char) code;

System.out.println(letter);
```

Output:

```text
B
```

---

# Arithmetic Promotions

Java automatically promotes smaller integer types during arithmetic operations.

Example:

```java
byte a = 10;
byte b = 20;

int sum = a + b;
```

Notice:

Even though both operands are `byte`, the result is an `int`.

This is a design choice that simplifies arithmetic processing for the JVM.

---

# Mixed-Type Expressions

When different numeric types appear in the same expression, Java promotes them to the widest type involved.

Example:

```java
int a = 5;
double b = 2.5;

double result = a + b;
```

Output:

```text
7.5
```

The `int` is automatically promoted to `double`.

---

# Casting Does Not Change the Original Variable

Example:

```java
double value = 8.9;

int number = (int) value;
```

After execution:

```text
value   = 8.9
number  = 8
```

The original variable remains unchanged.

---

# Common Beginner Mistakes

### Forgetting Explicit Cast

Incorrect:

```java
double price = 19.99;

int value = price;
```

Compilation error.

Correct:

```java
int value = (int) price;
```

---

### Expecting Rounding

Incorrect expectation:

```java
(double) 9.99 → 10
```

Actual result:

```text
9
```

Casting truncates; it does not round.

---

### Ignoring Overflow

```java
byte value = (byte) 200;
```

This compiles, but the resulting value is **not** `200`.

Always ensure the destination type can represent the value you're converting.

---

# Best Practices

* Prefer implicit casting whenever possible.
* Use explicit casting only when necessary.
* Be aware of potential data loss.
* Never assume casting performs rounding.
* Choose appropriate data types to minimize unnecessary conversions.

---

# Guided Exercise

Create a program called `CastingDemo.java`.

Demonstrate the following:

1. Convert an `int` to a `double` using implicit casting.
2. Convert a `double` to an `int` using explicit casting.
3. Convert a `char` to its Unicode value.
4. Convert an integer Unicode value back into a `char`.

Print the result of each conversion with descriptive labels.

---

# Independent Exercises

## Easy

Create a program that:

* Stores an `int`
* Assigns it to a `double`
* Prints both variables

Observe the automatic conversion.

---

## Medium

Create a program that:

* Stores a decimal number (`double`)
* Converts it to an `int`
* Prints both values

Explain (in comments) why the decimal part disappeared.

---

## Hard

Create a program called `CastingPlayground.java`.

Demonstrate:

* Widening conversion
* Narrowing conversion
* Character-to-integer conversion
* Integer-to-character conversion
* Overflow using `byte`

Print every result and describe what happened using comments.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

1. What is type casting?
2. What is the difference between widening and narrowing?
3. Why can widening conversions happen automatically?
4. Why does narrowing require explicit casting?
5. What happens to the decimal part when casting from `double` to `int`?
6. Does casting perform rounding?
7. What is overflow?
8. Why does `char` convert to an integer?
9. What happens when arithmetic is performed on two `byte` values?
10. Does casting modify the original variable?

---

# Chapter Summary

In this chapter, you learned:

* What type casting is and why it exists.
* The difference between implicit (widening) and explicit (narrowing) conversions.
* How Java handles automatic promotions.
* Why casting from `double` to `int` removes the fractional part instead of rounding.
* What overflow is and why it can produce unexpected values.
* How characters and integers are related through Unicode.

---

## Progress Checkpoint

Before moving on to **Chapter 6 — Constants**, make sure you can:

* Explain the purpose of type casting.
* Distinguish between widening and narrowing conversions.
* Perform explicit casts correctly.
* Predict when information will be lost during a conversion.
* Understand overflow and arithmetic promotion.
* Convert between `char` and `int` using Unicode.
