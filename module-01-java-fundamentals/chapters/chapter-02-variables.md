# Chapter 2 — Variables

## Overview

Imagine trying to write a calculator without being able to remember any numbers.

Or a game that couldn't remember the player's score.

Or a banking system that couldn't remember a customer's balance.

That would be impossible.

Programs need a way to **store information while they are running**. This is exactly why variables exist.

In this chapter, you'll learn what variables are, how Java stores them in memory, how to declare and initialize them, and how to use them effectively in professional code.

---

# Why Do Variables Exist?

A program constantly works with information:

* A person's name
* An account balance
* The result of a calculation
* A product price
* A player's score

These values often need to change while the program runs.

Instead of writing the value directly everywhere, we store it in a **variable**.

Think of a variable as a **labeled box**:

```text
+------------------+
|      age         |
+------------------+
|       25         |
+------------------+
```

The label is the **variable name**, and the content is its **value**.

If the value changes, the label stays the same.

---

# What Is a Variable?

A **variable** is a named location in memory that stores a value.

Breaking this definition down:

* **Named** → It has an identifier (such as `age` or `price`).
* **Location in memory** → Java reserves space in your computer's RAM.
* **Stores a value** → That space contains data.

When your program runs, Java keeps track of these memory locations so you don't have to.

---

# How Variables Work Internally

Suppose you write:

```java
int age = 25;
```

Behind the scenes, Java does something conceptually like this:

```text
Variable Name        Memory             Value
----------------------------------------------
age            ───► 0x7AFB20            25
```

You never work directly with memory addresses. Java manages them for you, making programming safer and easier.

> **Important:** The memory address shown above is only an illustration. Java hides these implementation details from developers.

---

# Declaring a Variable

Before using a variable, you must declare it.

General syntax:

```java
dataType variableName;
```

Example:

```java
int age;
```

At this point:

* The variable exists.
* Memory has been reserved.
* No value has been assigned yet.

---

# Initializing a Variable

Initialization means giving a variable its first value.

```java
int age = 25;
```

This combines declaration and initialization in a single line.

You can also do it in two steps:

```java
int age;

age = 25;
```

Both approaches are valid.

---

# Assigning a New Value

Variables can change during program execution.

```java
int score = 100;

score = 150;

score = 200;
```

Final value:

```text
200
```

Each assignment **replaces** the previous value.

The old value is discarded.

---

# Reading a Variable

A variable can be used anywhere its value is needed.

```java
int age = 25;

System.out.println(age);
```

Output:

```text
25
```

Notice that:

```java
System.out.println(age);
```

prints the value stored in the variable, **not** the word `"age"`.

Compare:

```java
System.out.println(age);
System.out.println("age");
```

Output:

```text
25
age
```

The first uses the variable. The second prints a string literal.

---

# Declaring Multiple Variables

Java allows multiple variables of the same type to be declared on one line.

```java
int x, y, z;
```

Or initialized together:

```java
int x = 10, y = 20, z = 30;
```

Although valid, professional code often prefers one variable per line for readability:

```java
int x = 10;
int y = 20;
int z = 30;
```

---

# Variable Lifetime (Scope Preview)

Variables don't live forever.

For example:

```java
public class Main {

    public static void main(String[] args) {

        int age = 25;

        System.out.println(age);

    }

}
```

Here, `age` exists only inside the `main()` method.

When the method finishes, the variable is removed from memory.

We'll study **scope** in depth later in the Bootcamp.

---

# Variable Naming Rules

Variable names:

* Can contain letters
* Can contain digits (but not as the first character)
* Can contain `_` and `$`
* Cannot contain spaces
* Cannot be Java keywords

Valid:

```java
age
userName
price2
_total
```

Invalid:

```text
2age
user name
class
int
```

---

# Java Naming Conventions

Java follows **camelCase** for variables.

Good:

```java
firstName
lastName
accountBalance
productPrice
```

Poor:

```java
FIRSTNAME
first_name
firstnamevalue
MyVariable
```

Professional developers follow conventions because they make code easier to read and maintain.

---

# Meaningful Names

Always choose names that describe the purpose of the variable.

Poor:

```java
int a;
```

Better:

```java
int age;
```

Even better:

```java
int customerAge;
```

The goal is that someone reading your code understands it without needing extra comments.

---

# Best Practices

* Use meaningful names.
* Prefer one declaration per line.
* Initialize variables before using them.
* Follow camelCase.
* Avoid abbreviations unless they are widely understood.

---

# Common Beginner Mistakes

### Using a Variable Before Initialization

```java
int age;

System.out.println(age);
```

This causes a compilation error because Java prevents you from reading an uninitialized local variable.

Correct:

```java
int age = 25;

System.out.println(age);
```

---

### Confusing Strings with Variables

Incorrect:

```java
int age = 25;

System.out.println("age");
```

Output:

```text
age
```

Correct:

```java
System.out.println(age);
```

Output:

```text
25
```

---

### Choosing Bad Names

Poor:

```java
int x;
int y;
int z;
```

Better:

```java
int width;
int height;
int area;
```

Clear names reduce bugs and improve collaboration.

---

# Guided Exercise

Create a program called `StudentInfo.java`.

Declare variables for:

* Student name
* Age
* Favorite programming language
* Graduation year

Print the information in a readable format.

Example output:

```text
Student Information
-------------------
Name: Eduardo
Age: 25
Favorite Language: Java
Graduation Year: 2028
```

---

# Independent Exercises

## Easy

Create a program that stores your:

* Name
* City
* Favorite color

Print all three values using variables.

---

## Medium

Create a program that stores:

* Product name
* Price
* Quantity

Print the information in a formatted way.

---

## Hard

Create a program called `CharacterProfile.java`.

Store at least **eight** pieces of information about a fictional character (name, age, profession, city, favorite weapon, etc.) using variables, then print a well-formatted profile to the console.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

1. What is a variable?
2. Why do programs need variables?
3. Where are variables stored while a program is running?
4. What is the difference between declaration and initialization?
5. Can a variable's value change after it has been created?
6. What happens to the old value when a new value is assigned?
7. Why is `System.out.println(age);` different from `System.out.println("age");`?
8. What naming convention is commonly used for Java variables?
9. Why should variable names be meaningful?
10. What happens if you try to use a local variable before initializing it?

---

# Chapter Summary

In this chapter, you learned:

* Why variables are essential in programming.
* How Java stores variables in memory conceptually.
* How to declare, initialize, read, and update variables.
* The difference between variable names and string literals.
* Java's naming rules and `camelCase` convention.
* Best practices for writing clean and maintainable code.
* Common mistakes beginners make when working with variables.

---

## Progress Checkpoint

Before moving on to **Chapter 3 — Primitive Data Types**, make sure you can:

* Explain what a variable is and why it exists.
* Declare and initialize variables correctly.
* Reassign new values to variables.
* Print variable values to the console.
* Follow Java naming conventions.
* Choose meaningful variable names for your programs.
