# Chapter 8 — Expressions and Evaluation

## Overview

By now, you've learned about variables, data types, literals, constants, and operators.

However, writing code isn't just about knowing individual operators—it's about understanding how Java **combines** them into complete expressions and how those expressions are evaluated.

Many programming bugs occur not because the programmer doesn't know an operator, but because they misunderstand **the order in which Java evaluates an expression**.

In this chapter, you'll learn what expressions and statements are, how Java evaluates them, how operator precedence affects results, and why writing clear expressions is a hallmark of professional code.

---

# What Is an Expression?

An **expression** is any combination of:

* Literals
* Variables
* Operators
* Method calls

that produces a **single value**.

Example:

```java
10 + 5
```

Produces:

```text
15
```

Another example:

```java
age + 2
```

If:

```java
int age = 20;
```

Then the expression evaluates to:

```text
22
```

An expression always has a result.

---

# What Is a Statement?

A **statement** is a complete instruction that Java executes.

Example:

```java
int age = 20;
```

This is a statement.

It tells Java:

1. Create a variable.
2. Store the value `20`.

Another example:

```java
System.out.println(age);
```

This is also a statement.

Every statement performs an action.

---

# Expression vs Statement

Consider:

```java
10 + 5
```

This is only an expression.

It computes a value but doesn't do anything with it.

Now:

```java
int result = 10 + 5;
```

The expression:

```java
10 + 5
```

is part of the statement.

The statement stores the result.

---

# How Java Evaluates Expressions

Java evaluates expressions step by step.

Example:

```java
int result = 10 + 5 * 2;
```

Evaluation:

```text
5 * 2
```

↓

```text
10
```

↓

```text
10 + 10
```

↓

```text
20
```

The final value assigned to `result` is:

```text
20
```

---

# Operator Precedence

Every operator has a priority.

Higher-priority operators execute first.

Simplified precedence:

| Priority | Operators            |   |   |
| -------- | -------------------- | - | - |
| Highest  | `()`                 |   |   |
|          | `++`, `--`, `!`      |   |   |
|          | `*`, `/`, `%`        |   |   |
|          | `+`, `-`             |   |   |
|          | `<`, `<=`, `>`, `>=` |   |   |
|          | `==`, `!=`           |   |   |
|          | `&&`                 |   |   |
| Lowest   | `                    |   | ` |

Example:

```java
int value = 5 + 4 * 3;
```

Result:

```text
17
```

Because multiplication happens first.

---

# Parentheses

Parentheses override precedence.

Example:

```java
int value = (5 + 4) * 3;
```

Evaluation:

```text
5 + 4 = 9

9 × 3 = 27
```

Result:

```text
27
```

Even when parentheses are not required, using them can improve readability.

Professional developers often add parentheses to make their intent obvious.

---

# Left-to-Right Evaluation

Operators with the same precedence are usually evaluated from left to right.

Example:

```java
int value = 20 - 5 - 3;
```

Evaluation:

```text
20 - 5 = 15

15 - 3 = 12
```

Result:

```text
12
```

Not:

```text
20 - (5 - 3)
```

Which would produce:

```text
18
```

---

# Assignment Is Also an Expression

This may surprise you:

```java
x = 10
```

is itself an expression.

Its value is the value assigned.

Example:

```java
int x;
int y;

y = x = 10;
```

After execution:

```text
x = 10
y = 10
```

Although valid, this style is uncommon in professional Java because it reduces readability.

---

# Side Effects

A **side effect** is any operation that changes the program's state.

Example:

```java
count++;
```

The expression returns a value **and** changes the variable.

Another example:

```java
score += 50;
```

The variable now holds a different value.

Expressions without side effects simply compute values.

Example:

```java
10 + 5
```

Nothing changes in memory.

---

# Reading Complex Expressions

Suppose you see:

```java
int result = (10 + 2) * 5 - 8 / 2;
```

Evaluate step by step:

First:

```text
10 + 2 = 12
```

Then:

```text
12 × 5 = 60
```

Then:

```text
8 ÷ 2 = 4
```

Finally:

```text
60 - 4 = 56
```

Result:

```text
56
```

Breaking expressions into smaller parts makes them easier to understand and debug.

---

# Readability Over Cleverness

Compare these two examples.

Example 1:

```java
int finalPrice = price - discount + tax;
```

Example 2:

```java
double discountedPrice = price - discount;
double finalPrice = discountedPrice + tax;
```

Both may produce the same result.

The second version is easier to read, maintain, and debug.

Professional developers prioritize **clarity** over writing fewer lines of code.

---

# Common Beginner Mistakes

## Ignoring Precedence

Unexpected:

```java
int result = 5 + 3 * 2;
```

Result:

```text
11
```

Not:

```text
16
```

---

## Writing Overly Complex Expressions

Hard to read:

```java
int value = a + b * c - d / e + f % g;
```

Better:

```java
int multiplication = b * c;
int division = d / e;
int remainder = f % g;

int value = a + multiplication - division + remainder;
```

---

## Assuming Expressions Execute Simultaneously

Java evaluates expressions in a defined order.

It never performs all operations at once.

Understanding that order is essential for predicting results.

---

# Best Practices

* Use parentheses to clarify intent.
* Break long expressions into smaller variables.
* Favor readability over compact code.
* Avoid unnecessary side effects inside expressions.
* Write code that another developer can understand quickly.

---

# Guided Exercise

Create a program called `ExpressionDemo.java`.

Declare several variables and evaluate the following:

```java
10 + 5 * 2

(10 + 5) * 2

20 - 5 - 3

100 / 4 + 8 * 2
```

Print each expression and its result.

---

# Independent Exercises

## Easy

Create variables:

```text
a = 10

b = 20
```

Evaluate:

* `a + b`
* `a * b`
* `b - a`

Print every result.

---

## Medium

Create variables:

```text
price = 200

discount = 25

tax = 15
```

Calculate the final price using multiple expressions.

Then rewrite the calculation using intermediate variables to improve readability.

---

## Hard

Create a program called `ExpressionPlayground.java`.

Write at least **10 different expressions** combining:

* Arithmetic operators
* Comparison operators
* Logical operators
* Parentheses

For each expression:

* Predict the result in a comment before running the program.
* Execute it.
* Compare your prediction with the actual output.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

1. What is an expression?
2. What is a statement?
3. Can an expression exist without being part of a statement?
4. Which operator has higher precedence: `+` or `*`?
5. What is the purpose of parentheses?
6. What is a side effect?
7. Why should long expressions be broken into smaller parts?
8. How are operators with the same precedence usually evaluated?
9. Why is readability more important than writing fewer lines of code?
10. What is the result of:

```java
(8 + 2) * 3 - 4 / 2
```

---

# Chapter Summary

In this chapter, you learned:

* The difference between expressions and statements.
* How Java evaluates expressions step by step.
* The role of operator precedence.
* How parentheses influence evaluation.
* What side effects are.
* Why clean, readable expressions are preferred in professional development.
* Techniques for simplifying complex calculations.

---

## Progress Checkpoint

Before moving on to **Chapter 9 — Working with User Input**, make sure you can:

* Explain the difference between an expression and a statement.
* Predict how Java evaluates arithmetic expressions.
* Apply operator precedence correctly.
* Use parentheses to improve both correctness and readability.
* Identify side effects in expressions.
* Refactor long expressions into simpler, more maintainable code.
