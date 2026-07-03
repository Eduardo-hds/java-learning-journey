# Chapter 02 — Declaring and Invoking Methods

## Overview

In the previous chapter, you learned **why methods exist**. Now it's time to create your own.

By the end of this chapter, you'll be able to:

* Declare methods.
* Invoke (call) methods.
* Understand the anatomy of a method.
* Understand what a **method signature** is.
* Follow the execution flow when methods call each other.

This is the first time you'll write code **outside** the `main()` method.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Declare a static method.
* Call a method from `main()`.
* Explain each part of a method declaration.
* Understand the execution flow between methods.
* Recognize a method signature.

---

# Declaring a Method

A method declaration tells Java:

* the method's name;
* whether it returns a value;
* what information it receives (if any);
* what code it executes.

A simple method looks like this:

```java
public static void sayHello() {
    System.out.println("Hello!");
}
```

Let's break it down.

```java
public static void sayHello() {
    System.out.println("Hello!");
}
```

| Part       | Meaning                                                                                        |
| ---------- | ---------------------------------------------------------------------------------------------- |
| `public`   | The method can be accessed from anywhere in the program. (We'll study access modifiers later.) |
| `static`   | The method belongs to the class itself, allowing `main()` to call it directly.                 |
| `void`     | The method does not return a value.                                                            |
| `sayHello` | The method's name.                                                                             |
| `()`       | The parameter list. It's empty for now.                                                        |
| `{}`       | The method body—the code that runs when the method is called.                                  |

> **For this module, always use `public static`.** We'll learn why in detail when we study Object-Oriented Programming.

---

# Where Do Methods Go?

A common beginner mistake is placing a method **inside** `main()`.

❌ Incorrect:

```java
public class Main {

    public static void main(String[] args) {

        public static void sayHello() {
            System.out.println("Hello");
        }

    }
}
```

Java **does not allow methods inside other methods**.

---

The correct structure is:

```java
public class Main {

    public static void main(String[] args) {

    }

    public static void sayHello() {
        System.out.println("Hello");
    }
}
```

Notice that both methods belong directly to the class.

---

# Invoking (Calling) a Method

Declaring a method does **not** execute it.

To execute it, you must call it.

Example:

```java
public class Main {

    public static void main(String[] args) {

        sayHello();

    }

    public static void sayHello() {

        System.out.println("Hello!");

    }
}
```

Output:

```text
Hello!
```

---

# The Execution Flow

Consider this program:

```java
public class Main {

    public static void main(String[] args) {

        System.out.println("Start");

        sayHello();

        System.out.println("End");

    }

    public static void sayHello() {

        System.out.println("Hello!");

    }

}
```

What happens?

Step 1:

```text
main()

Start
```

---

Step 2:

```text
main()

↓

sayHello()
```

---

Step 3:

```text
sayHello()

Hello!
```

---

Step 4:

After `sayHello()` finishes, Java returns to the exact point where it was called.

```text
main()

End
```

Final output:

```text
Start
Hello!
End
```

This "jump to the method and return" behavior is fundamental to understanding program execution.

---

# Calling a Method Multiple Times

One of the greatest benefits of methods is reuse.

```java
public class Main {

    public static void main(String[] args) {

        sayHello();
        sayHello();
        sayHello();

    }

    public static void sayHello() {

        System.out.println("Hello!");

    }

}
```

Output:

```text
Hello!
Hello!
Hello!
```

The method was written **once** but executed **three times**.

---

# Methods Can Call Other Methods

Methods aren't limited to being called only from `main()`.

Example:

```java
public class Main {

    public static void main(String[] args) {

        startProgram();

    }

    public static void startProgram() {

        System.out.println("Program started.");

        showMenu();

    }

    public static void showMenu() {

        System.out.println("1 - Calculator");
        System.out.println("2 - Exit");

    }

}
```

Execution flow:

```text
main()
    │
    ▼
startProgram()
    │
    ▼
showMenu()
```

This is how large applications are organized: each method delegates work to another when appropriate.

---

# Method Names

Method names should describe **what the method does**.

Good examples:

```text
printMenu()
showTitle()
calculateAverage()
readNumber()
isPrime()
convertTemperature()
```

Poor examples:

```text
doIt()
run()
test()
method1()
abc()
```

A well-named method often makes code understandable without reading its implementation.

---

# What Is a Method Signature?

The **method signature** uniquely identifies a method for the compiler.

It consists of:

* the method name;
* the parameter list (number, order, and types of parameters).

Example:

```java
sum(int a, int b)
```

The signature is:

```text
sum(int, int)
```

Another example:

```java
printMessage(String text)
```

Signature:

```text
printMessage(String)
```

Notice that the return type (`void`, `int`, `double`, etc.) is **not** part of the method signature.

We'll see why this matters when we study **method overloading** later in this module.

---

# Common Beginner Mistakes

### Forgetting to call the method

```java
public static void sayHello() {
    System.out.println("Hello!");
}
```

Nothing happens because the method was never called.

---

### Calling a method that doesn't exist

```java
sayHi();
```

If `sayHi()` hasn't been declared, the program won't compile.

---

### Misspelling the method name

```java
sayhello();
```

Java is **case-sensitive**.

These are different names:

```java
sayHello()
```

```java
sayhello()
```

---

### Declaring a method inside another method

This is illegal in Java and results in a compilation error.

---

# Best Practices

✔ Give methods descriptive names.

✔ Keep each method focused on a single task.

✔ Avoid duplicating code—reuse methods instead.

✔ Place methods outside `main()` but inside the class.

✔ Keep `main()` simple by delegating work to other methods.

---

# Summary

In this chapter, you learned:

* How to declare a method.
* How to call a method.
* That declaring a method does not execute it.
* How execution jumps to a method and then returns.
* That methods can call other methods.
* What a method signature is.
* The importance of clear, descriptive method names.

---

# Practice Exercises

Create a program that includes the following methods:

1. `printSeparator()`

   * Prints a line of dashes.

2. `showTitle()`

   * Prints:

   ```
   Java Bootcamp
   ```

3. `showMenu()`

   * Prints:

   ```
   1 - Start
   2 - Settings
   3 - Exit
   ```

Then, inside `main()`, call the methods in this order:

```text
printSeparator()
showTitle()
printSeparator()
showMenu()
printSeparator()
```

### Expected Output

```text
--------------------
Java Bootcamp
--------------------
1 - Start
2 - Settings
3 - Exit
--------------------
```

> **Challenge:** After completing the exercise, create a new method called `startApplication()` that calls `printSeparator()`, `showTitle()`, and `showMenu()`. Then make `main()` call only `startApplication()`. This is your first step toward writing clean, modular programs.

When you've finished the exercise, move to **Chapter 03 — Parameters and Arguments**.
