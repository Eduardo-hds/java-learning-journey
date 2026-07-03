# Chapter 1 — Your First Java Program

## Overview

Every application, from a simple calculator to a banking system, starts as a program written in a programming language.

In this chapter, you'll learn what a Java program actually is, how Java executes it, and how to write your very first console application. More importantly, you'll understand **what happens behind the scenes** when you press the **Run** button in IntelliJ IDEA.

By the end of this chapter, you will know how a Java program is structured and why every part of that structure exists.

---

# What Is a Program?

A **program** is simply a sequence of instructions that tells a computer what to do.

Think of it like a recipe:

- A recipe tells a cook what steps to follow.
- A program tells the CPU what steps to execute.

The computer cannot "guess" what you want. It only follows instructions exactly as they are written.

For example:

```
1. Display "Hello"
2. Wait for the user
3. End the program
```

This is already a very simple program.

---

# What Is Source Code?

Humans don't write programs in machine language (0s and 1s). Instead, we write them in a **high-level programming language**, such as Java.

The text we write is called **source code**.

Example:

```java
System.out.println("Hello, World!");
```

This is readable by humans, but not directly by the CPU.

---

# From Source Code to Running Program

One of the biggest strengths of Java is that it uses an intermediate step before reaching machine code.

The process looks like this:

```
Source Code (.java)
        │
        ▼
Java Compiler (javac)
        │
        ▼
Bytecode (.class)
        │
        ▼
Java Virtual Machine (JVM)
        │
        ▼
Machine Instructions
        │
        ▼
CPU Executes
```

Let's understand each step.

---

## Step 1 — Writing the Source Code

You create a file ending with:

```
.java
```

Example:

```
HelloWorld.java
```

This file contains your Java code.

---

## Step 2 — Compilation

The Java compiler (`javac`) reads your source code.

Its job is to:

- Check syntax errors
- Check type errors
- Convert Java into **Bytecode**

Output:

```
HelloWorld.class
```

Notice:

The compiler **does not create machine code**.

Instead, it creates **Bytecode**.

---

## Step 3 — Bytecode

Bytecode is a special instruction language understood by the JVM.

This is what makes Java portable.

Instead of compiling separately for Windows, Linux, and macOS, Java compiles once into Bytecode.

---

## Step 4 — JVM (Java Virtual Machine)

The JVM reads the Bytecode and translates it into machine instructions for the operating system you're using.

Because every operating system has its own JVM implementation, the same `.class` file can run on different platforms without changing the source code.

This is the origin of Java's famous slogan:

> **"Write Once, Run Anywhere."**

---

# The Structure of a Java Program

Create a new file called:

```text
HelloWorld.java
```

Write the following code:

```java
public class HelloWorld {

    public static void main(String[] args) {

        System.out.println("Hello, World!");

    }

}
```

At first glance, it may seem like a lot of code just to display one message. Don't worry—we'll break it down piece by piece.

---

## `public class HelloWorld`

```java
public class HelloWorld {
```

A **class** is a blueprint that groups related code together.

For now, you can think of it as the **container** that holds your program.

The class name must match the file name.

Correct:

```text
HelloWorld.java
```

```java
public class HelloWorld
```

Incorrect:

```text
Program.java
```

```java
public class HelloWorld
```

This would cause a compilation error.

---

## Curly Braces `{}`

Curly braces define blocks of code.

Everything inside the class belongs to that class.

Example:

```java
public class HelloWorld {

}
```

The same applies to methods.

---

## The `main()` Method

```java
public static void main(String[] args)
```

This is the **entry point** of every Java application.

When you run a Java program, the JVM looks specifically for this method.

If it cannot find it, the program cannot start.

For now, memorize this structure. In later modules, we'll explain every keyword (`public`, `static`, `void`, and `String[]`) in detail.

---

## `System.out.println()`

```java
System.out.println("Hello, World!");
```

This instruction prints text to the console.

Breaking it down:

- `System` → a built-in Java class.
- `out` → the standard output stream (usually the terminal).
- `println()` → prints a line and moves the cursor to the next line.

Example:

```java
System.out.println("Java");
System.out.println("Bootcamp");
```

Output:

```text
Java
Bootcamp
```

---

## `print()` vs `println()`

### `println()`

```java
System.out.println("Java");
System.out.println("Bootcamp");
```

Output:

```text
Java
Bootcamp
```

Each call ends with a new line.

---

### `print()`

```java
System.out.print("Java");
System.out.print("Bootcamp");
```

Output:

```text
JavaBootcamp
```

No line break is added.

---

### Mixing Both

```java
System.out.print("Java ");
System.out.println("Bootcamp");
```

Output:

```text
Java Bootcamp
```

---

# How Execution Flows

Execution always starts inside `main()`.

```java
public static void main(String[] args) {

    System.out.println("First");

    System.out.println("Second");

    System.out.println("Third");

}
```

Output:

```text
First
Second
Third
```

Java executes instructions **from top to bottom**, one line at a time.

---

# Common Beginner Mistakes

### Forgetting the semicolon

```java
System.out.println("Hello")
```

Incorrect.

Correct:

```java
System.out.println("Hello");
```

---

### Mismatched file and class names

```text
Program.java
```

```java
public class HelloWorld
```

This causes a compilation error.

---

### Incorrect capitalization

Java is **case-sensitive**.

Correct:

```java
System.out.println();
```

Incorrect:

```java
system.out.println();
```

`System` and `system` are different identifiers.

---

### Using double quotes incorrectly

Correct:

```java
System.out.println("Hello");
```

Incorrect:

```java
System.out.println(Hello);
```

Text literals must be enclosed in double quotes.

---

# Best Practices

- Give classes meaningful names.
- Match the file name with the class name.
- Use proper indentation.
- Keep your code clean and readable.
- Don't worry about memorizing every keyword yet—focus on understanding the program's overall structure.

---

# Guided Exercise

Create a program named `AboutMe.java`.

It should display:

```text
Name: Your Name
Age: Your Age
Favorite Language: Java
```

Example:

```text
Name: Eduardo
Age: 25
Favorite Language: Java
```

Use only `System.out.println()`.

---

# Independent Exercises

## Easy

Create a program that prints:

```text
Welcome to Java!
```

---

## Medium

Create a program that prints the following exactly:

```text
*****
*   *
*   *
*****
```

---

## Hard

Create a program called `Motivation.java` that prints a motivational message using **both** `print()` and `println()` to control the formatting of the output.

> **Do not ask for the solution until you've attempted it.**

---

# Quiz

Try to answer without looking back at the chapter.

1. What is a computer program?
2. What is source code?
3. What is the role of the Java compiler?
4. What is Bytecode?
5. What is the JVM responsible for?
6. Why is Java considered platform-independent?
7. What is the purpose of the `main()` method?
8. What is the difference between `print()` and `println()`?
9. Why must the class name match the file name?
10. What does it mean that Java is case-sensitive?

---

# Chapter Summary

In this chapter, you learned:

- What a computer program is.
- What source code is and why it exists.
- How Java transforms source code into Bytecode.
- The role of the JVM in executing Java programs.
- The structure of a basic Java application.
- The purpose of the `main()` method.
- The difference between `print()` and `println()`.
- Common beginner mistakes and best practices for writing your first Java programs.

---

## Progress Checkpoint

Before moving on to **Chapter 2 — Variables**, make sure you can:

- Explain the journey from `.java` source code to a running program.
- Create a Java class with the correct structure.
- Write and run a simple console application.
- Use `System.out.print()` and `System.out.println()` correctly.
- Identify the purpose of the `main()` method.
