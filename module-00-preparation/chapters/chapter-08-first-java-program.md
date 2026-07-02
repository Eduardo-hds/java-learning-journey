# Chapter 8 — Your First Java Program

## Overview

After learning about the Java platform, its architecture, development environment, project organization, and naming conventions, it is finally time to write our first Java program.

Although the program itself is simple, every line introduces fundamental concepts that will be used throughout the rest of the Bootcamp.

The goal of this chapter is not only to make the program work, but to understand exactly what happens when a Java application starts.

---

## Objectives

By the end of this chapter, I will understand:

- How to create a Java class
- What the `main` method is
- Why the `main` method is required
- How Java applications start
- How to compile and execute a Java program
- How to print information to the console
- The basic structure of every Java application

---

## Creating the First Class

Every Java application starts with a class.

Let's create a file named:

```text
Main.java
```

Inside it, write:

```java
public class Main {

    public static void main(String[] args) {

        System.out.println("Hello, Java!");

    }

}
```

This is the simplest complete Java application.

---

## Understanding the Class

```java
public class Main {
}
```

### `public`

The keyword `public` makes the class accessible from anywhere in the project.

---

### `class`

A class is a blueprint for creating objects.

Everything in Java is organized inside classes.

---

### `Main`

This is the name of the class.

Because the class is `public`, the file must also be named:

```text
Main.java
```

---

## Understanding the `main` Method

```java
public static void main(String[] args)
```

This is the entry point of every Java application.

When the JVM starts a program, it looks specifically for this method.

If it cannot find it, the application cannot start.

---

### `public`

Allows the JVM to access the method.

---

### `static`

The JVM calls the method without creating an object first.

This topic will be explored in depth later in the Bootcamp.

---

### `void`

Indicates that the method does not return a value.

---

### `main`

This is the method name recognized by the JVM as the application's starting point.

Changing this name prevents the program from starting.

---

### `String[] args`

This parameter receives command-line arguments.

Example:

```text
java Main hello world
```

The array would contain:

```text
args[0] = "hello"
args[1] = "world"
```

We will study arrays later in the Bootcamp.

---

## Printing to the Console

```java
System.out.println("Hello, Java!");
```

This statement prints text to the console.

Breaking it down:

### `System`

Represents the Java system class.

---

### `out`

Represents the standard output stream.

---

### `println()`

Prints the given value followed by a new line.

Example output:

```text
Hello, Java!
```

---

## Program Execution Flow

When you run the program, the following happens:

1. The source code (`Main.java`) is compiled.
2. The compiler generates `Main.class`.
3. The JVM loads the class.
4. The JVM searches for the `main()` method.
5. The `main()` method begins execution.
6. `System.out.println()` prints the message.
7. The program finishes.

---

## Compiling Manually

Using the terminal:

Compile:

```bash
javac Main.java
```

Execute:

```bash
java Main
```

Output:

```text
Hello, Java!
```

Although IntelliJ performs these steps automatically, understanding them is essential.

---

## Common Mistakes

### File name does not match the class

Incorrect:

```text
App.java
```

```java
public class Main {
}
```

---

### Missing the `main` Method

Without the `main()` method, the JVM does not know where to begin execution.

---

### Typing Errors

Examples:

- `System.Out.Println()`
- `system.out.println()`
- `Println()`

Java is case-sensitive, meaning uppercase and lowercase letters matter.

---

## Best Practices

- Use meaningful class names.
- Keep one public class per file.
- Follow Java naming conventions.
- Understand each keyword instead of memorizing the syntax.
- Let the IDE help detect syntax errors.

---

## Curiosity

The famous `"Hello, World!"` tradition dates back to the early days of programming and became popular through the book _The C Programming Language_ by Brian Kernighan and Dennis Ritchie.

Today, almost every programming language introduces beginners with a similar first program.

---

## Key Concepts Summary

- Every Java application starts inside a class.
- Execution begins in the `main()` method.
- The JVM searches for `public static void main(String[] args)`.
- `System.out.println()` prints information to the console.
- Java programs are compiled before being executed.

---

## Key Idea of this Chapter

Writing the first Java program is more than displaying a message.

It introduces the execution model that every Java application follows, from source code to JVM execution.

---

## Summary

- Java programs are organized into classes.
- The `main()` method is the application's entry point.
- The JVM starts execution from the `main()` method.
- `System.out.println()` writes output to the console.
- Understanding this structure is essential before learning the Java language itself.

---

## Next Step

**Chapter 9 — Using the Debugger**

In the next chapter, we will learn how to use IntelliJ IDEA's debugger to execute code step by step, inspect variables, and understand how Java programs run internally.
