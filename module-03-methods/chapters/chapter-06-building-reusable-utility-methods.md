# Chapter 06 — Building Reusable Utility Methods

## Overview

So far, you've learned how to:

* Create methods.
* Pass information using parameters.
* Return values.
* Understand variable scope.

Now it's time to combine these skills to write **reusable utility methods**.

A utility method is a small, focused method that performs one specific task and can be reused throughout your program.

This chapter is less about learning new Java syntax and more about learning **how to think like a programmer**.

Instead of asking:

> "How do I solve this problem?"

You'll start asking:

> "What small methods can I create to solve this problem?"

This shift in thinking is one of the biggest steps toward writing professional code.

---

# Learning Objectives

After completing this chapter, you will be able to:

* Identify repeated code.
* Extract repeated logic into reusable methods.
* Separate responsibilities between methods.
* Design helper methods with clear purposes.
* Build a larger application from small methods.

---

# What Is a Utility Method?

A utility method is simply a method that performs a useful task and can be called whenever needed.

Examples:

```java
printSeparator();
```

```java
showTitle();
```

```java
calculateArea(width, height);
```

```java
isPrime(number);
```

```java
convertCelsiusToFahrenheit(celsius);
```

Each method has one clear responsibility.

---

# Recognizing Duplicate Code

Imagine this program:

```java
System.out.println("====================");
System.out.println("Temperature Converter");
System.out.println("====================");

// ...

System.out.println("====================");
System.out.println("Temperature Converter");
System.out.println("====================");
```

The same three lines appear twice.

Whenever you notice yourself copying and pasting code, ask:

> "Could this become a method?"

Usually, the answer is **yes**.

---

# Extracting a Method

Instead of duplicating the title:

```java
public static void showTitle() {

    System.out.println("====================");
    System.out.println("Temperature Converter");
    System.out.println("====================");

}
```

Now you simply write:

```java
showTitle();
```

If the title ever changes, you update only one method.

---

# One Responsibility per Method

Imagine a method like this:

```java
public static void doEverything() {

    // show menu
    // read input
    // convert temperature
    // print result
    // save file

}
```

Can you immediately understand its purpose?

Not really.

Now compare:

```text
showTitle()

showMenu()

readTemperature()

convertTemperature()

printResult()
```

Each method has one clear job.

This is known as the **Single Responsibility Principle (SRP)**.

Although SRP is formally introduced in Object-Oriented Programming, the habit starts now.

---

# Designing Small Methods

Suppose you're building a temperature converter.

Instead of writing one huge method, divide it into smaller pieces.

```text
main()
│
├── showTitle()
├── showMenu()
├── readTemperature()
├── convertTemperature()
└── printResult()
```

Each method becomes easier to understand, test, and reuse.

---

# Beginning Exercise 2 — Temperature Converter

We'll now start the second core exercise of this module.

Our converter will eventually support:

* Celsius → Fahrenheit
* Fahrenheit → Celsius
* Celsius → Kelvin
* Kelvin → Celsius

We'll build it gradually.

---

## Step 1 — Celsius to Fahrenheit

The formula is:

```text
F = (C × 9 / 5) + 32
```

Create this method:

```java
public static double celsiusToFahrenheit(double celsius) {

    return (celsius * 9 / 5) + 32;

}
```

Using it:

```java
double fahrenheit = celsiusToFahrenheit(25);

System.out.println(fahrenheit);
```

Output:

```text
77.0
```

Notice that the method **calculates** the conversion but doesn't print anything.

---

## Step 2 — Fahrenheit to Celsius

Formula:

```text
C = (F - 32) × 5 / 9
```

Method:

```java
public static double fahrenheitToCelsius(double fahrenheit) {

    return (fahrenheit - 32) * 5 / 9;

}
```

---

## Step 3 — Celsius to Kelvin

Formula:

```text
K = C + 273.15
```

Method:

```java
public static double celsiusToKelvin(double celsius) {

    return celsius + 273.15;

}
```

---

## Step 4 — Kelvin to Celsius

Formula:

```text
C = K - 273.15
```

Method:

```java
public static double kelvinToCelsius(double kelvin) {

    return kelvin - 273.15;

}
```

---

# Why Return Instead of Print?

Compare these two approaches.

### Version A

```java
public static void celsiusToFahrenheit(double celsius) {

    System.out.println((celsius * 9 / 5) + 32);

}
```

You can only display the result.

---

### Version B

```java
public static double celsiusToFahrenheit(double celsius) {

    return (celsius * 9 / 5) + 32;

}
```

Now you can:

```java
double value = celsiusToFahrenheit(25);
```

or

```java
System.out.println(celsiusToFahrenheit(25));
```

or

```java
double doubled = celsiusToFahrenheit(25) * 2;
```

Returning values makes methods much more flexible.

---

# Reusing Methods

Imagine your application grows.

You need to convert temperatures in:

* a menu;
* a report;
* a statistics screen.

Because your conversion logic is inside methods, every part of the program can reuse the same code.

This avoids duplication and reduces bugs.

---

# Good Method Design

Ask yourself these questions whenever you create a method:

* Does it perform only one task?
* Is its name descriptive?
* Does it need parameters?
* Should it return a value?
* Can it be reused elsewhere?

If the answer is "yes," you're probably designing a good method.

---

# Common Beginner Mistakes

### Mixing calculation and display

```java
public static double calculateArea(double width, double height) {

    System.out.println(width * height);

    return width * height;

}
```

The method both prints and returns the result.

Choose one responsibility whenever possible.

---

### Giving methods vague names

```java
process();
```

What does it process?

Instead, write:

```java
convertTemperature();
```

The name explains the method's purpose.

---

### Creating overly large methods

A method with 100 lines usually indicates that it should be split into smaller methods.

---

# Best Practices

✔ One method = one responsibility.

✔ Return values instead of printing whenever the result might be reused.

✔ Use descriptive names.

✔ Keep methods short and focused.

✔ Avoid duplicate code by extracting repeated logic into methods.

---

# Exercise 2 — Temperature Converter

Implement the following methods:

```java
public static double celsiusToFahrenheit(double celsius)
```

```java
public static double fahrenheitToCelsius(double fahrenheit)
```

```java
public static double celsiusToKelvin(double celsius)
```

```java
public static double kelvinToCelsius(double kelvin)
```

Then create a simple `main()` method that demonstrates each conversion with example values.

Example output:

```text
25°C = 77.0°F
77°F = 25.0°C
25°C = 298.15 K
298.15 K = 25.0°C
```

---

# Mini Challenge

Create these additional utility methods:

```java
public static void printSeparator()
```

```java
public static void showConverterTitle()
```

```java
public static void printConversion(String label, double value)
```

Your `main()` should become something like:

```text
showConverterTitle()

↓

printSeparator()

↓

perform conversions

↓

printConversion(...)
```

Notice how `main()` begins to read almost like plain English.

This is a hallmark of well-structured programs.

---

# Summary

In this chapter, you learned:

* What utility methods are.
* How to recognize duplicated code.
* How to extract repeated logic into reusable methods.
* The importance of giving each method a single responsibility.
* How to build a temperature converter using reusable methods.
* Why returning values is generally more flexible than printing them.
* How to organize larger console applications by composing many small methods.

---

## What's Next?

In **Chapter 07 — Number Analysis with Methods**, you'll continue building reusable logic by creating methods that answer questions about numbers, such as:

* Is the number even or odd?
* Is it positive, negative, or zero?
* Is it prime?

These methods will return **boolean** and other values, reinforcing the idea that methods should provide information rather than just display it.
