# Chapter 4 — Literals and Numeric Representations

## Overview

So far, you've learned how to declare variables and choose the correct data type.

But where do the values themselves come from?

When you write:

```java
int age = 25;
```

Where does the `25` come from?

That `25` is called a **literal**.

In this chapter, you'll learn what literals are, how Java interprets them, and the different ways numbers and characters can be represented directly in your code.

---

# What Is a Literal?

A **literal** is a value written directly into the source code.

Examples:

```java
10
3.14
'A'
true
"Hello"
```

All of these are literals because their values are explicitly written by the programmer.

Example:

```java
int age = 25;
```

Here:

* `int` → Data type
* `age` → Variable
* `25` → Integer literal

---

# Variables vs Literals

These concepts are often confused.

```java
int age = 25;
```

Breaking it down:

| Part  | Meaning   |
| ----- | --------- |
| `int` | Data type |
| `age` | Variable  |
| `25`  | Literal   |

A variable stores data.

A literal **is** the data.

---

# Integer Literals

The most common literals are integers.

Examples:

```java
10
50
0
-100
999999
```

Using them:

```java
int apples = 10;

System.out.println(apples);
```

---

# Decimal Literals

Numbers with decimal places.

Examples:

```java
3.14
10.5
99.99
0.25
```

Java interprets decimal literals as `double` by default.

Example:

```java
double price = 19.99;
```

If you want a `float`:

```java
float price = 19.99F;
```

The `F` tells Java:

> "Treat this literal as a float."

---

# Character Literals

A character literal represents **exactly one character**.

Examples:

```java
'A'
'B'
'7'
'$'
```

Using them:

```java
char grade = 'A';
```

Remember:

Characters use **single quotes**.

---

# String Literals

Although `String` is **not** a primitive type, it has its own literal syntax.

Examples:

```java
"Java"
"Hello"
"Eduardo"
```

Using them:

```java
String language = "Java";
```

Notice:

Strings use **double quotes**.

A string can contain:

* One character
* Multiple characters
* Even zero characters

Example:

```java
String empty = "";
```

---

# Boolean Literals

Only two values exist:

```java
true
false
```

Example:

```java
boolean loggedIn = true;
```

---

# Null Literal

Java also has a special literal:

```java
null
```

Example:

```java
String name = null;
```

`null` means:

> "This variable currently refers to no object."

Since we haven't studied objects yet, just remember that `null` can only be assigned to **reference types** (such as `String`), not to primitive types.

Example:

```java
int age = null;
```

Compilation error.

We'll explore `null` deeply in later modules.

---

# Numeric Representations

Most programmers write numbers in decimal (base 10).

Java also supports other bases.

---

## Decimal (Base 10)

Default representation.

```java
int number = 42;
```

---

## Binary (Base 2)

Prefix:

```text
0b
```

Example:

```java
int number = 0b101010;
```

Output:

```text
42
```

Explanation:

```text
101010₂ = 42₁₀
```

Binary is useful when working with bits, flags, and low-level programming.

---

## Hexadecimal (Base 16)

Prefix:

```text
0x
```

Example:

```java
int color = 0xFF;
```

Output:

```text
255
```

Hexadecimal is commonly used for:

* Colors
* Memory addresses
* Binary data
* Debugging
* Networking

---

## Octal (Base 8)

Prefix:

```text
0
```

Example:

```java
int value = 052;
```

Output:

```text
42
```

Octal is supported for historical reasons but is rarely used in modern Java code.

Many teams avoid it because a leading `0` can easily cause confusion.

---

# Numeric Separators

Large numbers can be difficult to read.

Instead of:

```java
int population = 1000000000;
```

Java allows underscores:

```java
int population = 1_000_000_000;
```

Same value.

Much easier to read.

You can also write:

```java
long distance = 384_400_000L;
double pi = 3.141_592_653;
```

The underscores are ignored by the compiler.

---

# Scientific Notation

Large or very small decimal numbers can be written using exponential notation.

Example:

```java
double speedOfLight = 3.0e8;
```

Equivalent to:

```text
300000000
```

Another example:

```java
double atomSize = 1.6e-10;
```

Equivalent to:

```text
0.00000000016
```

This notation is common in:

* Physics
* Engineering
* Scientific computing
* Graphics programming

---

# Escape Sequences (String and Character Literals)

Sometimes you need special characters inside a string.

Java provides **escape sequences**.

| Escape | Meaning         |
| ------ | --------------- |
| `\"`   | Double quote    |
| `\'`   | Single quote    |
| `\\`   | Backslash       |
| `\n`   | New line        |
| `\t`   | Tab             |
| `\r`   | Carriage return |

Example:

```java
System.out.println("Hello\nWorld");
```

Output:

```text
Hello
World
```

Another example:

```java
System.out.println("She said: \"Java is awesome!\"");
```

Output:

```text
She said: "Java is awesome!"
```

---

# Common Beginner Mistakes

### Using Double Quotes for Characters

Incorrect:

```java
char letter = "A";
```

Correct:

```java
char letter = 'A';
```

---

### Using Single Quotes for Strings

Incorrect:

```java
String name = 'Eduardo';
```

Correct:

```java
String name = "Eduardo";
```

---

### Forgetting the `F`

Incorrect:

```java
float price = 5.5;
```

Correct:

```java
float price = 5.5F;
```

---

### Misusing Numeric Separators

Incorrect:

```java
int value = _1000;
```

Or:

```java
int value = 1000_;
```

Correct:

```java
int value = 1_000;
```

Underscores cannot appear at the beginning or end of a number.

---

# Best Practices

* Use decimal notation unless another base clearly improves readability.
* Add numeric separators for long numbers.
* Use escape sequences instead of awkward formatting.
* Remember the difference between:

  * Character literals (`'A'`)
  * String literals (`"A"`)

---

# Guided Exercise

Create a program called `LiteralExamples.java`.

Declare variables using:

* Decimal integer literal
* Binary integer literal
* Hexadecimal integer literal
* Decimal literal (`double`)
* Float literal
* Character literal
* String literal
* Boolean literal

Print each variable with a descriptive label.

---

# Independent Exercises

## Easy

Create a program that stores:

* Your favorite number
* Your favorite letter
* Your favorite word

Print all three.

---

## Medium

Create a program demonstrating numeric representations.

Store the value **100** using:

* Decimal
* Binary
* Hexadecimal

Print all three variables and observe that they display the same decimal value.

---

## Hard

Create a program called `FormattingDemo.java`.

Print a formatted message using:

* `\n`
* `\t`
* `\"`
* `\\`

Your output should clearly demonstrate the effect of each escape sequence.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

1. What is a literal?
2. What is the difference between a variable and a literal?
3. What type does Java assume for decimal literals by default?
4. What is the difference between `'A'` and `"A"`?
5. What does the `null` literal represent?
6. How do you write a binary literal in Java?
7. How do you write a hexadecimal literal?
8. Why are numeric separators useful?
9. What does `\n` do inside a string?
10. What is the purpose of escape sequences?

---

# Chapter Summary

In this chapter, you learned:

* What literals are and how they differ from variables.
* The syntax for integer, decimal, character, string, boolean, and `null` literals.
* How Java supports decimal, binary, hexadecimal, and octal numeric representations.
* How to improve readability with numeric separators.
* How scientific notation works.
* How to use escape sequences to format text.

---

## Progress Checkpoint

Before moving on to **Chapter 5 — Type Casting**, make sure you can:

* Explain what a literal is.
* Distinguish variables from literals.
* Write literals in decimal, binary, and hexadecimal.
* Use character and string literals correctly.
* Apply escape sequences to format console output.
* Understand when and why to use numeric separators.
