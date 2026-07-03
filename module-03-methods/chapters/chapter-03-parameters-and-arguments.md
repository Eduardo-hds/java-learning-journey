# Chapter 03 — Parameters and Arguments

## Overview

In the previous chapter, every method looked something like this:

```java
public static void sayHello() {
    System.out.println("Hello!");
}
```

This method always does the **exact same thing**. No matter how many times you call it, the output never changes.

But what if you wanted to greet different people?

```text
Hello, Eduardo!
Hello, Alice!
Hello, John!
```

Would you create a separate method for each person?

```java
sayHelloEduardo();
sayHelloAlice();
sayHelloJohn();
```

Of course not.

Instead, we make our methods **flexible** by allowing them to receive information. This is where **parameters** and **arguments** come in.

By the end of this chapter, you'll be able to write methods that accept data and reuse them in many different situations.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Understand what parameters are.
* Understand what arguments are.
* Distinguish between parameters and arguments.
* Create methods with one or more parameters.
* Call methods with different values.
* Understand parameter order.
* Know how primitive values are passed to methods.

---

# What Is a Parameter?

A **parameter** is a variable declared in a method's header.

It acts as a placeholder for the value that will be provided when the method is called.

Example:

```java
public static void greet(String name) {
    System.out.println("Hello, " + name + "!");
}
```

Here:

```java
String name
```

is the **parameter**.

It doesn't have a value until someone calls the method.

---

# What Is an Argument?

An **argument** is the actual value passed to a method.

Example:

```java
greet("Eduardo");
```

In this call:

* `"Eduardo"` is the **argument**.
* `name` is the **parameter**.

Think of it like filling out a form:

```text
Parameter → Blank field

Name: __________
```

When someone writes:

```text
Eduardo
```

that value is the **argument**.

---

# Parameters vs Arguments

| Parameter                | Argument                       |
| ------------------------ | ------------------------------ |
| Declared in the method   | Passed when calling the method |
| Acts like a variable     | Is the actual value            |
| Exists inside the method | Exists in the method call      |

Example:

```java
public static void greet(String name) {
    System.out.println("Hello, " + name);
}

public static void main(String[] args) {

    greet("Eduardo");

}
```

* Parameter → `String name`
* Argument → `"Eduardo"`

---

# One Parameter

Example:

```java
public static void printNumber(int number) {

    System.out.println(number);

}
```

Calling it:

```java
printNumber(10);
printNumber(25);
printNumber(100);
```

Output:

```text
10
25
100
```

Notice that the method never changes—only the argument changes.

---

# Multiple Parameters

Methods can receive more than one value.

Example:

```java
public static void introduce(String name, int age) {

    System.out.println(name + " is " + age + " years old.");

}
```

Calling it:

```java
introduce("Alice", 20);
introduce("Bob", 31);
```

Output:

```text
Alice is 20 years old.
Bob is 31 years old.
```

---

# Parameter Order Matters

Java matches arguments **by position**, not by name.

Correct:

```java
introduce("Alice", 20);
```

Parameter mapping:

```text
name → "Alice"
age  → 20
```

Incorrect:

```java
introduce(20, "Alice");
```

This produces a compilation error because Java expected:

```text
String
int
```

but received:

```text
int
String
```

---

# Different Data Types

Parameters can use any data type you've learned.

```java
public static void showAge(int age)
```

```java
public static void showPrice(double price)
```

```java
public static void showLetter(char letter)
```

```java
public static void isAdult(boolean adult)
```

```java
public static void greet(String name)
```

Each parameter has its own type.

---

# Using Multiple Types Together

Example:

```java
public static void registerStudent(String name, int age, double grade) {

    System.out.println(name);
    System.out.println(age);
    System.out.println(grade);

}
```

Call:

```java
registerStudent("Emma", 19, 8.7);
```

Output:

```text
Emma
19
8.7
```

---

# Passing Variables

Arguments don't have to be literal values.

You can pass variables too.

```java
public static void greet(String name) {

    System.out.println("Hello, " + name);

}
```

```java
public static void main(String[] args) {

    String student = "Eduardo";

    greet(student);

}
```

Output:

```text
Hello, Eduardo
```

The variable's value is passed to the parameter.

---

# Passing Primitive Values

When you pass a primitive value (`int`, `double`, `char`, `boolean`, etc.), Java passes a **copy** of the value.

Example:

```java
public static void increase(int number) {

    number++;

    System.out.println(number);

}
```

```java
public static void main(String[] args) {

    int value = 10;

    increase(value);

    System.out.println(value);

}
```

Output:

```text
11
10
```

Why?

Execution:

```text
value = 10

↓

increase(value)

↓

number = 10
```

`number` receives **its own copy**.

Changing `number` does **not** change `value`.

This behavior is called **pass-by-value**, and it's how Java passes primitive types.

> **Note:** We'll revisit parameter passing when we start working with objects in later modules.

---

# Common Beginner Mistakes

### Forgetting a parameter

```java
public static void greet() {

}
```

Calling:

```java
greet("Eduardo");
```

Compilation error.

The method doesn't expect any arguments.

---

### Missing an argument

```java
public static void sum(int a, int b)
```

Calling:

```java
sum(5);
```

Compilation error.

Both parameters must receive values.

---

### Wrong data type

```java
showAge("Twenty");
```

Expected:

```java
int
```

Received:

```java
String
```

Compilation error.

---

### Wrong parameter order

```java
registerStudent(20, "Alice", 9.5);
```

Expected:

```text
String
int
double
```

Received:

```text
int
String
double
```

---

# Best Practices

✔ Use descriptive parameter names.

Good:

```java
calculateArea(double radius)
```

Instead of:

```java
calculateArea(double x)
```

unless the meaning is obvious.

---

✔ Keep the number of parameters reasonable.

If a method has ten parameters, it's often trying to do too much.

---

✔ Keep parameter order logical.

Example:

```java
name, age, salary
```

is easier to understand than:

```java
salary, name, age
```

---

# Summary

In this chapter, you learned:

* What parameters are.
* What arguments are.
* The difference between parameters and arguments.
* How to create methods with one or more parameters.
* That parameter order matters.
* That primitive values are passed by value (a copy).

---

# Practice Exercises

Create the following methods:

### 1. Greeting

```java
greet(String name)
```

Example:

```text
Hello, Eduardo!
```

---

### 2. Square

```java
printSquare(int number)
```

Example:

Input:

```text
5
```

Output:

```text
Square: 25
```

---

### 3. Student Information

```java
showStudent(String name, int age, double grade)
```

Example:

```text
Name: Alice
Age: 20
Grade: 9.5
```

---

### 4. Rectangle

Create a method:

```java
printRectangleInfo(double width, double height)
```

Display:

```text
Width: ...
Height: ...
Area: ...
```

*(For now, calculate the area directly inside the method. In the next chapter, you'll learn how to return values instead of just printing them.)*

---

## Mini Challenge

Create a method:

```java
drawBox(char symbol, int size)
```

Example:

```text
*****
*****
*****
*****
*****
```

Calling:

```java
drawBox('*', 5);
```

This challenge combines everything you've learned so far: methods, parameters, loops, and clean code.

---

Once you've completed these exercises, continue to **Chapter 04 — Return Values**, where you'll learn how methods can send results back instead of only printing them.
