# Chapter 11 — Java Naming Conventions

## Overview

Imagine opening two Java projects.

The first contains variables like:

```java
int a;
int b;
int x1;
```

The second contains:

```java
int customerAge;
int productPrice;
int totalOrders;
```

Both programs may work exactly the same, but one is dramatically easier to understand.

Professional developers spend much more time **reading code** than writing it. That's why the Java community follows a set of naming conventions that make code consistent across projects.

In this chapter, you'll learn how to name variables, methods, classes, constants, and packages according to Java's official conventions.

---

# Why Naming Conventions Matter

A computer doesn't care whether a variable is named:

```java
int x;
```

or

```java
int customerAge;
```

Both compile and run correctly.

Humans, however, do care.

Good names make code:

* Easier to read
* Easier to maintain
* Easier to debug
* Easier to review
* Easier to collaborate on

Professional codebases may contain **millions of lines of code**. Consistent naming helps developers navigate them efficiently.

---

# Identifiers

An **identifier** is any name you give to a programming element.

Examples include:

* Variables
* Methods
* Classes
* Interfaces
* Packages
* Constants

Java imposes rules on valid identifiers.

---

# Naming Rules

Identifiers:

* May contain letters
* May contain digits
* May contain `_`
* May contain `$`
* Cannot begin with a digit
* Cannot contain spaces
* Cannot be Java keywords

Valid:

```java
age
userName
price2
_total
$value
```

Invalid:

```text
2age
user name
class
int
```

Although `$` is allowed, it is almost never used in normal Java code and is generally reserved for generated code or special frameworks.

---

# Variable Naming

Variables use **camelCase**.

Example:

```java
int customerAge;
double accountBalance;
boolean isLoggedIn;
```

Rule:

* First word starts with a lowercase letter.
* Each additional word begins with an uppercase letter.

Examples:

```java
firstName
lastName
studentGrade
productPrice
```

---

# Method Naming

Methods also use **camelCase**.

Examples:

```java
calculateTotal()
printInvoice()
findCustomer()
saveFile()
```

Good method names usually begin with a **verb**, because methods perform actions.

Good:

```java
calculateArea()
```

Poor:

```java
area()
```

The first clearly describes what the method does.

---

# Class Naming

Classes use **PascalCase** (also called UpperCamelCase).

Rule:

Every word begins with an uppercase letter.

Examples:

```java
Customer
BankAccount
ProductService
RectangleCalculator
```

Avoid:

```java
customer
bank_account
productservice
```

Classes usually represent **things** (nouns), not actions.

---

# Constant Naming

Constants use **UPPER_SNAKE_CASE**.

Examples:

```java
MAX_SPEED
PI
DEFAULT_TIMEOUT
SALES_TAX
SECONDS_PER_DAY
```

This immediately tells readers:

> "This value should not change."

---

# Package Naming

Package names are always lowercase.

Examples:

```text
com.company.project

com.myapp.service

org.example.utils
```

Multiple words are separated by dots (`.`), not underscores.

Avoid:

```text
MyPackage

UserService

MY_APP
```

---

# Boolean Naming

Boolean variables should read like questions.

Good:

```java
boolean isActive;
boolean hasPermission;
boolean canVote;
boolean wasUpdated;
```

Poor:

```java
boolean active;
boolean permission;
boolean vote;
```

Reading:

```java
if (isActive)
```

is much more natural than:

```java
if (active)
```

---

# Meaningful Names

Compare these examples.

Poor:

```java
double x;
```

Better:

```java
double salary;
```

Even better:

```java
double monthlySalary;
```

A good identifier answers:

> "What does this represent?"

without requiring additional comments.

---

# Avoid Abbreviations

Poor:

```java
int qty;
```

Better:

```java
int quantity;
```

Another example:

Poor:

```java
int numStd;
```

Better:

```java
int studentCount;
```

Exceptions exist for universally understood abbreviations:

```java
URL
HTML
PDF
ID
CPU
RAM
```

These are widely accepted in professional code.

---

# Avoid Single-Letter Variables

Bad:

```java
int a;
int b;
int c;
```

Good:

```java
int width;
int height;
int area;
```

The only common exceptions are very small scopes, such as loop counters you'll encounter later:

```java
for (int i = 0; i < 10; i++)
```

Using `i`, `j`, or `k` for simple loop indexes is a well-established convention.

---

# Avoid Misleading Names

Poor:

```java
double age;
```

Age is typically an integer.

Better:

```java
int age;
```

Another example:

```java
String totalPrice;
```

A price should usually be numeric, not text.

Good names should reflect both the purpose **and** the type of data being stored.

---

# Consistency Is Important

Imagine seeing this:

```java
int customerAge;
double ProductPrice;
boolean ISACTIVE;
```

Every identifier follows a different style.

Professional projects aim for consistency.

A consistent style makes large codebases feel predictable and easier to navigate.

---

# Common Beginner Mistakes

## Using Snake Case for Variables

Incorrect:

```java
int customer_age;
```

Correct:

```java
int customerAge;
```

---

## Using camelCase for Classes

Incorrect:

```java
public class customerAccount
```

Correct:

```java
public class CustomerAccount
```

---

## Using camelCase for Constants

Incorrect:

```java
final double salesTax = 0.18;
```

Correct:

```java
final double SALES_TAX = 0.18;
```

---

## Choosing Generic Names

Poor:

```java
double value;
```

Better:

```java
double monthlyIncome;
```

Specific names reduce ambiguity and improve readability.

---

# Best Practices

* Use meaningful names.
* Follow Java's standard conventions.
* Prefer full words over unclear abbreviations.
* Name methods using verbs.
* Name classes using nouns.
* Keep naming consistent throughout the project.
* Write code that explains itself.

---

# Guided Exercise

Create a program called `NamingExamples.java`.

Declare:

* Five variables using `camelCase`.
* Three constants using `UPPER_SNAKE_CASE`.
* One class using `PascalCase`.

Add comments explaining why each name follows Java conventions.

---

# Independent Exercises

## Easy

Create variables representing:

* Student name
* Student age
* Student grade

Choose clear, professional names.

---

## Medium

Imagine you're creating a banking application.

Choose appropriate names for:

* Balance
* Account number
* Customer name
* Interest rate
* Whether the account is active

Follow Java conventions.

---

## Hard

Design the identifiers for a small e-commerce system.

Without writing the full program, create:

* 10 variable names
* 5 method names
* 5 class names
* 5 constants
* 3 package names

Ensure every identifier follows Java naming conventions and clearly communicates its purpose.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

1. Why are naming conventions important?
2. What is an identifier?
3. Which convention is used for variables?
4. Which convention is used for classes?
5. Which convention is used for constants?
6. Why should method names usually begin with verbs?
7. Why are meaningful names better than short names?
8. When are single-letter variable names acceptable?
9. Why should boolean variables read like questions?
10. What is the naming convention for Java packages?

---

# Chapter Summary

In this chapter, you learned:

* What identifiers are.
* Java's official naming conventions for variables, methods, classes, constants, and packages.
* The importance of meaningful and consistent names.
* Why self-documenting code is preferable to excessive comments.
* Common naming mistakes made by beginners.
* Best practices used in professional Java development.

---

## Progress Checkpoint

Before moving on to **Chapter 12 — Basic Debugging**, make sure you can:

* Apply `camelCase` to variables and methods.
* Apply `PascalCase` to classes.
* Apply `UPPER_SNAKE_CASE` to constants.
* Name boolean variables naturally (e.g., `isActive`, `hasPermission`).
* Create meaningful, descriptive identifiers.
* Explain why consistent naming improves code quality and maintainability.
