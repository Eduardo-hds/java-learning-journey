# Chapter 7 — Operators

## Overview

A program that can only store data isn't very useful.

Programs need to **perform calculations**, **compare values**, **make decisions**, and **update variables**. Operators are the tools that allow Java to do all of these things.

In this chapter, you'll learn what operators are, why they exist, how Java evaluates them, and the different categories of operators you'll use every day as a Java developer.

---

# What Is an Operator?

An **operator** is a symbol that tells Java to perform an operation on one or more values.

Example:

```java
int sum = 10 + 5;
```

Here:

* `10` → Operand
* `5` → Operand
* `+` → Operator

The operator tells Java to add the two operands together.

---

# Types of Operators

Java has several categories of operators.

In this chapter, we'll study:

* Arithmetic Operators
* Assignment Operators
* Increment and Decrement Operators
* Comparison (Relational) Operators
* Logical Operators
* Operator Precedence
* Short-Circuit Evaluation

---

# Arithmetic Operators

These operators perform mathematical calculations.

| Operator | Meaning            |
| -------- | ------------------ |
| `+`      | Addition           |
| `-`      | Subtraction        |
| `*`      | Multiplication     |
| `/`      | Division           |
| `%`      | Remainder (Modulo) |

---

## Addition (`+`)

```java
int result = 10 + 5;

System.out.println(result);
```

Output:

```text
15
```

---

## Subtraction (`-`)

```java
int result = 20 - 8;
```

Output:

```text
12
```

---

## Multiplication (`*`)

```java
int result = 6 * 4;
```

Output:

```text
24
```

---

## Division (`/`)

```java
int result = 10 / 2;
```

Output:

```text
5
```

But pay attention:

```java
int result = 7 / 2;

System.out.println(result);
```

Output:

```text
3
```

Why?

Both operands are integers, so Java performs **integer division**, discarding the fractional part.

To obtain a decimal result:

```java
double result = 7.0 / 2;
```

Output:

```text
3.5
```

---

## Modulo (`%`)

The modulo operator returns the **remainder** of a division.

Example:

```java
int result = 10 % 3;
```

Output:

```text
1
```

Because:

```text
10 ÷ 3 = 3 remainder 1
```

Common uses:

* Checking if a number is even or odd.
* Repeating patterns.
* Cycling through indexes.
* Game loops.

Example:

```java
int number = 8;

System.out.println(number % 2);
```

Output:

```text
0
```

A remainder of `0` means the number is even.

---

# Assignment Operator (`=`)

The assignment operator stores a value inside a variable.

Example:

```java
int age = 25;
```

Here:

```text
25 → age
```

Notice:

The `=` operator **does not mean "equals" in mathematics**.

It means:

> "Assign the value on the right to the variable on the left."

---

# Compound Assignment Operators

Java provides shortcuts for updating variables.

Instead of:

```java
score = score + 10;
```

You can write:

```java
score += 10;
```

Other examples:

```java
score -= 5;
score *= 2;
score /= 4;
score %= 3;
```

These operators make code shorter and easier to read.

---

# Increment Operator (`++`)

The increment operator increases a value by one.

Instead of:

```java
count = count + 1;
```

You write:

```java
count++;
```

Example:

```java
int count = 5;

count++;

System.out.println(count);
```

Output:

```text
6
```

---

# Decrement Operator (`--`)

Works the same way, but subtracts one.

```java
int lives = 3;

lives--;

System.out.println(lives);
```

Output:

```text
2
```

---

# Prefix vs Postfix Increment

There are two forms:

```java
++count;
```

and

```java
count++;
```

Most of the time, when used alone, they produce the same result.

Example:

```java
count++;
```

and

```java
++count;
```

Both increase the variable by one.

The difference appears when the increment is used inside another expression.

Example:

```java
int x = 5;

System.out.println(x++);
System.out.println(x);
```

Output:

```text
5
6
```

Now compare:

```java
int x = 5;

System.out.println(++x);
System.out.println(x);
```

Output:

```text
6
6
```

Rule:

* `x++` → Use the current value, then increment.
* `++x` → Increment first, then use the new value.

As a beginner, it's best to avoid using `++` inside complex expressions to keep your code clear.

---

# Comparison (Relational) Operators

These operators compare two values.

The result is always a `boolean`.

| Operator | Meaning                  |
| -------- | ------------------------ |
| `==`     | Equal to                 |
| `!=`     | Not equal to             |
| `>`      | Greater than             |
| `<`      | Less than                |
| `>=`     | Greater than or equal to |
| `<=`     | Less than or equal to    |

Example:

```java
int age = 20;

System.out.println(age >= 18);
```

Output:

```text
true
```

---

# Equality vs Assignment

A common beginner mistake:

Assignment:

```java
age = 20;
```

Comparison:

```java
age == 20
```

One stores a value.

The other checks whether two values are equal.

---

# Logical Operators

Logical operators combine boolean expressions.

| Operator | Meaning     |   |            |
| -------- | ----------- | - | ---------- |
| `&&`     | Logical AND |   |            |
| `        |             | ` | Logical OR |
| `!`      | Logical NOT |   |            |

---

## AND (`&&`)

Both conditions must be true.

Example:

```java
boolean hasPassword = true;
boolean hasFingerprint = true;

System.out.println(hasPassword && hasFingerprint);
```

Output:

```text
true
```

---

## OR (`||`)

Only one condition needs to be true.

Example:

```java
boolean isWeekend = false;
boolean isHoliday = true;

System.out.println(isWeekend || isHoliday);
```

Output:

```text
true
```

---

## NOT (`!`)

Reverses a boolean value.

Example:

```java
boolean loggedIn = false;

System.out.println(!loggedIn);
```

Output:

```text
true
```

---

# Operator Precedence

Java follows precedence rules, similar to mathematics.

Example:

```java
int result = 10 + 5 * 2;
```

Output:

```text
20
```

Multiplication happens first.

Equivalent to:

```java
10 + (5 * 2)
```

Use parentheses whenever they improve readability.

Example:

```java
int result = (10 + 5) * 2;
```

Output:

```text
30
```

---

# Short-Circuit Evaluation

Logical operators can stop evaluating early.

Example:

```java
boolean result = false && expensiveOperation();
```

Since the left side is already `false`, Java knows the entire expression must be `false`.

Therefore:

```java
expensiveOperation()
```

is **never executed**.

Similarly:

```java
true || expensiveOperation();
```

The second expression is skipped because the result is already known.

Short-circuit evaluation improves performance and prevents certain runtime errors.

---

# Common Beginner Mistakes

### Confusing `=` and `==`

Incorrect:

```java
System.out.println(age = 18);
```

Correct:

```java
System.out.println(age == 18);
```

---

### Integer Division

Unexpected:

```java
System.out.println(5 / 2);
```

Output:

```text
2
```

If you want:

```text
2.5
```

Use:

```java
System.out.println(5.0 / 2);
```

---

### Forgetting Modulo

Many beginners repeatedly subtract or divide manually to determine whether a number is even.

Instead:

```java
number % 2 == 0
```

is simpler and more efficient.

---

### Overusing `++` Inside Expressions

Avoid code like:

```java
int result = x++ + ++y;
```

Although valid, it reduces readability and can lead to confusion.

---

# Best Practices

* Use parentheses to make expressions clear.
* Avoid clever one-line expressions that sacrifice readability.
* Prefer `+=`, `-=`, etc., when updating variables.
* Use `%` for remainder-based logic.
* Keep increment/decrement operations simple and isolated.

---

# Guided Exercise

Create a program called `OperatorsDemo.java`.

Demonstrate:

* Addition
* Subtraction
* Multiplication
* Integer division
* Decimal division
* Modulo
* Compound assignment (`+=`)
* Increment
* Decrement
* Comparison operators
* Logical operators

Print the result of each operation with descriptive labels.

---

# Independent Exercises

## Easy

Create a program that stores two integers.

Print:

* Sum
* Difference
* Product
* Quotient
* Remainder

---

## Medium

Create a program that stores a student's grade.

Print:

* Whether the grade is greater than or equal to 60.
* Whether the grade is between 60 and 100 using logical operators.

---

## Hard

Create a program called `OperatorPlayground.java`.

Demonstrate every operator covered in this chapter.

For each example:

* Print the expression.
* Print the result.
* Add comments explaining what happened.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

1. What is an operator?
2. What is the difference between `=` and `==`?
3. What does the modulo operator (`%`) return?
4. Why does `7 / 2` produce `3` instead of `3.5`?
5. What is the difference between `&&` and `||`?
6. What does the `!` operator do?
7. What is the difference between `x++` and `++x`?
8. Why are parentheses useful in expressions?
9. What is short-circuit evaluation?
10. Why are compound assignment operators useful?

---

# Chapter Summary

In this chapter, you learned:

* What operators are and why they exist.
* How arithmetic, assignment, comparison, and logical operators work.
* The difference between integer and decimal division.
* How increment and decrement operators behave.
* How Java evaluates expressions using operator precedence.
* What short-circuit evaluation is and why it matters.
* Best practices for writing clear and maintainable expressions.

---

## Progress Checkpoint

Before moving on to **Chapter 8 — Expressions and Evaluation**, make sure you can:

* Use all basic arithmetic operators correctly.
* Distinguish assignment (`=`) from equality (`==`).
* Use comparison and logical operators to build boolean expressions.
* Explain integer division and the modulo operator.
* Understand the difference between prefix and postfix increment.
* Read and predict the result of expressions based on operator precedence.
