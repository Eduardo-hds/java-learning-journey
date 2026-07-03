# Chapter 05 — Variable Scope

## Overview

As your programs grow and you begin creating more methods, you'll notice something interesting:

Sometimes a variable is available where you expect it...

...and sometimes Java says:

```text
cannot find symbol
```

or

```text
variable cannot be resolved
```

This happens because **every variable has a scope**.

The **scope** of a variable determines **where it can be accessed** in your program.

Understanding scope is essential because it prevents accidental mistakes and keeps methods independent from one another.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what variable scope is.
* Identify local variables.
* Understand method scope.
* Explain the lifetime of variables.
* Recognize common scope-related errors.
* Write methods without relying on variables from other methods.

---

# What Is Scope?

**Scope** is the region of the program where a variable exists and can be used.

Think of a variable as a person working in an office.

A person in the Accounting department cannot simply walk into the Server Room and start working there.

Each person has an assigned area.

Variables work the same way.

A variable only exists inside the area where it was declared.

---

# Local Variables

A **local variable** is declared inside a method or inside a block (`if`, `for`, `while`, etc.).

Example:

```java
public static void greet() {

    String name = "Eduardo";

    System.out.println(name);

}
```

Here:

```java
String name = "Eduardo";
```

is a **local variable**.

It only exists inside the `greet()` method.

---

# Variables Belong to Their Method

Example:

```java
public class Main {

    public static void main(String[] args) {

        greet();

    }

    public static void greet() {

        String name = "Eduardo";

        System.out.println(name);

    }

}
```

Output:

```text
Eduardo
```

Everything works because `name` is used inside the same method where it was declared.

---

# Variables Cannot Escape Their Method

Consider this example:

```java
public class Main {

    public static void main(String[] args) {

        greet();

        System.out.println(name);

    }

    public static void greet() {

        String name = "Eduardo";

    }

}
```

Compilation error:

```text
cannot find symbol
```

Why?

Because:

```text
name
```

only exists inside:

```text
greet()
```

`main()` has no idea that variable ever existed.

---

# Visualizing Method Scope

Imagine each method as its own room.

```text
+----------------------+
| main()               |
|                      |
|                      |
+----------------------+

+----------------------+
| greet()              |
|                      |
| name                 |
+----------------------+
```

The variable `name` lives inside the `greet()` room.

It cannot be accessed from `main()`.

---

# Scope Inside Blocks

Scope is not limited to methods.

Blocks created with `{}` also define scope.

Example:

```java
public static void checkNumber(int number) {

    if (number > 0) {

        String message = "Positive";

        System.out.println(message);

    }

}
```

`message` only exists inside the `if` block.

Trying to use it afterward:

```java
System.out.println(message);
```

causes a compilation error.

---

# Scope in Loops

Variables declared inside loops behave the same way.

```java
for (int i = 1; i <= 5; i++) {

    System.out.println(i);

}
```

The variable:

```java
i
```

only exists inside the loop.

Trying to use it later:

```java
System.out.println(i);
```

results in:

```text
cannot find symbol
```

---

# Lifetime of Variables

Scope tells us **where** a variable exists.

**Lifetime** tells us **how long** it exists.

Example:

```java
public static void printNumber() {

    int number = 10;

    System.out.println(number);

}
```

Execution:

```text
Method starts

↓

number is created

↓

number is used

↓

Method ends

↓

number is destroyed
```

Once the method finishes, the variable disappears from memory.

The next time the method is called, Java creates a brand-new variable.

---

# Each Method Call Gets Its Own Variables

Example:

```java
public static void counter() {

    int value = 1;

    System.out.println(value);

}
```

Calling:

```java
counter();
counter();
counter();
```

Output:

```text
1
1
1
```

Each call creates a completely new `value`.

The previous one no longer exists.

---

# Variables with the Same Name

Different methods may have variables with the same name.

Example:

```java
public static void methodA() {

    int number = 10;

}
```

```java
public static void methodB() {

    int number = 20;

}
```

This is perfectly valid.

Why?

Because each variable lives in a different scope.

They are unrelated.

---

# Nested Scope

Variables declared outside a block are visible inside that block.

Example:

```java
public static void example() {

    int number = 10;

    if (number > 0) {

        System.out.println(number);

    }

}
```

Output:

```text
10
```

The `if` block can access variables declared before it.

---

But the opposite is not true.

```java
if (true) {

    int number = 10;

}

System.out.println(number);
```

Compilation error.

Variables declared inside a block stay inside that block.

---

# Shadowing (Preview)

Consider:

```java
public static void printNumber(int number) {

    System.out.println(number);

}
```

The parameter:

```java
number
```

is already a local variable.

Trying this:

```java
public static void printNumber(int number) {

    int number = 10;

}
```

produces a compilation error because two local variables cannot have the same name within the same scope.

Later, when we study classes and objects, you'll learn about **variable shadowing** in more detail.

---

# Why Scope Is Important

Imagine if every variable were visible everywhere.

Programs would quickly become chaotic.

Methods could accidentally modify each other's data.

Scope prevents this.

Each method manages its own variables, making programs easier to understand and maintain.

---

# Common Beginner Mistakes

### Trying to use a variable from another method

```java
public static void methodA() {

    int age = 20;

}
```

```java
public static void methodB() {

    System.out.println(age);

}
```

Compilation error.

---

### Using a variable outside an `if`

```java
if (true) {

    int x = 5;

}

System.out.println(x);
```

Compilation error.

---

### Using the loop variable after the loop

```java
for (int i = 0; i < 5; i++) {

}
```

```java
System.out.println(i);
```

Compilation error.

---

# Best Practices

✔ Declare variables as close as possible to where they are used.

Instead of:

```java
int result;

// many unrelated lines...

result = add(5, 8);
```

Prefer:

```java
int result = add(5, 8);
```

---

✔ Keep variables inside the smallest scope possible.

Smaller scopes make code easier to read and reduce mistakes.

---

✔ Don't rely on variables from other methods.

Instead, pass information using **parameters** and receive results using **return values**.

This keeps methods independent and reusable.

---

# Summary

In this chapter, you learned:

* Scope defines where a variable can be accessed.
* Local variables exist only inside the method or block where they are declared.
* Variables are created when execution enters their scope and destroyed when it leaves.
* Different methods can have variables with the same name.
* Inner blocks can access variables from outer blocks, but not the other way around.
* Methods should communicate using parameters and return values, not by sharing local variables.

---

# Practice Exercises

### Exercise 1 — Scope Observation

Create this method:

```java
public static void greet() {

    String name = "Eduardo";

    System.out.println(name);

}
```

Then try to print `name` inside `main()`.

Observe the compilation error and explain why it happens.

---

### Exercise 2 — Loop Scope

Create a `for` loop:

```java
for (int i = 1; i <= 5; i++) {

    System.out.println(i);

}
```

Then try to print `i` after the loop.

What error do you get?

---

### Exercise 3 — Independent Methods

Create two methods:

```java
public static void methodA()
```

and

```java
public static void methodB()
```

Each should declare its own variable named:

```java
int number
```

Assign different values and print them.

Observe that the variables do not interfere with each other.

---

### Mini Challenge

Create a program with these methods:

```java
showMenu()
```

```java
readOption()
```

```java
processOption(int option)
```

Each method must declare only the variables it actually needs.

Avoid making variables live longer than necessary.

This exercise reinforces writing **small, self-contained methods**, a habit that will become increasingly important as the bootcamp progresses.

---

## What's Next?

In **Chapter 06 — Building Reusable Utility Methods**, you'll start applying everything you've learned so far to create practical helper methods and begin the **Temperature Converter** project, where methods will eliminate duplicated code and make your program much more organized.
