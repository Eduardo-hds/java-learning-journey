# Chapter 9 — Working with User Input

## Overview

Until now, every program you've written has produced the same output every time it ran.

For example:

```java
System.out.println("Hello, World!");
```

No matter who runs the program or how many times it's executed, the output is always the same.

Real-world applications don't work this way.

A calculator asks for numbers.

A login screen asks for a username and password.

A banking system asks for an account number.

Games ask for the player's name.

To build interactive applications, a program must be able to **receive information from the user**.

In this chapter, you'll learn how Java reads input from the keyboard using the `Scanner` class.

---

# What Is User Input?

**User input** is any information entered into a program while it is running.

Examples:

* Name
* Age
* Salary
* Product price
* Menu option
* Password

Instead of hardcoding values:

```java
String name = "Eduardo";
```

The program can ask the user:

```text
Enter your name:
```

The value is then provided when the program is running.

---

# What Is Scanner?

Java includes a class called **`Scanner`** that can read data from different sources.

Examples:

* Keyboard
* Files
* Strings
* Network streams

In this chapter, we'll use it to read data from the **keyboard**.

---

# Importing Scanner

Before using `Scanner`, we need to import it.

```java
import java.util.Scanner;
```

Why?

Because the `Scanner` class belongs to the package:

```text
java.util
```

The `import` statement tells Java where to find the class.

---

# Creating a Scanner Object

To read from the keyboard:

```java
Scanner scanner = new Scanner(System.in);
```

Let's break it down.

```java
Scanner
```

The type of the variable.

---

```java
scanner
```

The variable name.

---

```java
new Scanner(...)
```

Creates a new `Scanner` object.

You'll study objects in detail in the Object-Oriented Programming module.

For now, think of it as creating a tool that can read user input.

---

```java
System.in
```

Represents the **standard input stream**, which is usually the keyboard.

---

# Your First Input Program

```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your name: ");

        String name = scanner.nextLine();

        System.out.println("Hello, " + name + "!");

        scanner.close();

    }

}
```

Example:

```text
Enter your name: Eduardo
Hello, Eduardo!
```

---

# Why Call `close()`?

```java
scanner.close();
```

This releases the system resources used by the `Scanner`.

In small programs, forgetting to close it usually won't cause noticeable problems.

However, in professional applications, it's considered good practice to close resources when you're finished using them.

---

# Reading Different Data Types

## Reading a String

```java
String name = scanner.nextLine();
```

Reads an entire line of text.

Example input:

```text
John Smith
```

The entire line is stored.

---

## Reading an Integer

```java
int age = scanner.nextInt();
```

Example:

```text
Enter your age: 25
```

The variable receives:

```text
25
```

---

## Reading a Double

```java
double salary = scanner.nextDouble();
```

Example:

```text
3500.75
```

---

## Reading a Boolean

```java
boolean student = scanner.nextBoolean();
```

Valid inputs:

```text
true
false
```

Anything else causes an exception.

---

# The Difference Between `next()` and `nextLine()`

This is one of the most common beginner mistakes.

---

## `next()`

Reads only **one word**.

Example:

Input:

```text
John Smith
```

Code:

```java
String name = scanner.next();
```

Result:

```text
John
```

Everything after the space remains in the input buffer.

---

## `nextLine()`

Reads the **entire line**.

Example:

Input:

```text
John Smith
```

Code:

```java
String name = scanner.nextLine();
```

Result:

```text
John Smith
```

---

# The "Skipped Input" Problem

Consider:

```java
int age = scanner.nextInt();

String name = scanner.nextLine();
```

Many beginners expect:

```text
Age: 25

Name: Eduardo
```

Instead:

```text
Age: 25

Name:
```

The program appears to skip the name.

Why?

---

# Understanding the Input Buffer

When the user types:

```text
25↵
```

Java actually receives:

```text
2
5
\n
```

The `nextInt()` method reads only:

```text
25
```

The newline character (`\n`) remains in the input buffer.

Then:

```java
nextLine()
```

Immediately reads that leftover newline, producing an empty string.

---

# The Solution

Consume the remaining newline before calling `nextLine()`.

```java
int age = scanner.nextInt();

scanner.nextLine();

String name = scanner.nextLine();
```

Now the program works correctly.

This is one of the most frequently encountered issues when using `Scanner`.

---

# Input Validation (Preview)

Suppose the program expects an integer:

```java
int age = scanner.nextInt();
```

But the user types:

```text
twenty
```

Java throws an exception because it cannot convert the text into an integer.

Later in the Bootcamp, you'll learn how to validate input and handle these errors gracefully using exception handling.

---

# String Concatenation

When displaying input:

```java
System.out.println("Hello, " + name);
```

The `+` operator joins strings together.

This is called **concatenation**.

Example:

```java
String first = "Java";

String second = "Bootcamp";

System.out.println(first + " " + second);
```

Output:

```text
Java Bootcamp
```

---

# Common Beginner Mistakes

## Forgetting the Import

Incorrect:

```java
Scanner scanner = new Scanner(System.in);
```

Without:

```java
import java.util.Scanner;
```

Compilation error.

---

## Forgetting `close()`

Although simple programs still work, closing resources is considered a professional habit.

```java
scanner.close();
```

---

## Confusing `next()` and `nextLine()`

Remember:

```text
next()      → One word

nextLine()  → Entire line
```

---

## Mixing `nextInt()` and `nextLine()`

Always remember the leftover newline.

Example:

```java
scanner.nextInt();

scanner.nextLine();
```

before reading a complete line.

---

# Best Practices

* Import `Scanner` only when needed.
* Close the `Scanner` when finished.
* Prefer `nextLine()` when reading full names or sentences.
* Be aware of the newline issue after numeric input.
* Write clear prompts so users know what to enter.

---

# Guided Exercise

Create a program called `UserProfile.java`.

Ask the user for:

* Full name
* Age
* Height
* Favorite programming language

Display the information in a neatly formatted profile.

Remember to handle the newline after reading the age if necessary.

---

# Independent Exercises

## Easy

Ask the user for:

* Name
* Favorite color

Display:

```text
Hello, Eduardo!

Your favorite color is blue.
```

---

## Medium

Create a simple rectangle calculator.

Ask for:

* Width
* Height

Display:

* Area
* Perimeter

---

## Hard

Create a program called `EmployeeRegistration.java`.

Ask the user for:

* Full name
* Age
* Salary
* Department
* Is the employee full-time? (`true` or `false`)

Print a formatted employee summary.

Be careful when mixing numeric and text input.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

1. What is user input?
2. What is the purpose of the `Scanner` class?
3. Why must `Scanner` be imported?
4. What does `System.in` represent?
5. What is the difference between `next()` and `nextLine()`?
6. Why does `nextLine()` sometimes appear to be skipped?
7. How do you fix the skipped-input problem?
8. Why should `scanner.close()` be called?
9. What happens if `nextInt()` receives text instead of a number?
10. What is string concatenation?

---

# Chapter Summary

In this chapter, you learned:

* Why user input is essential for interactive applications.
* How to import and create a `Scanner`.
* How to read strings, integers, doubles, and booleans.
* The difference between `next()` and `nextLine()`.
* Why the skipped-input problem occurs and how to solve it.
* The importance of closing resources.
* How to combine text and variables using string concatenation.

---

## Progress Checkpoint

Before moving on to **Chapter 10 — Comments and Documentation**, make sure you can:

* Import and create a `Scanner`.
* Read different types of user input.
* Explain the difference between `next()` and `nextLine()`.
* Solve the newline-buffer problem after reading numeric values.
* Close the `Scanner` correctly.
* Build simple interactive console applications that respond to user input.
