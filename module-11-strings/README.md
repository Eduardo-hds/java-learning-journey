# Bootcamp Java — Module 11: Strings

# Module Introduction

Strings are one of the most frequently used concepts in Java applications.

Almost every real-world program manipulates text:

* user names
* passwords
* messages
* files paths
* database data
* API responses
* configuration values
* search systems
* reports

Because strings are so common, Java treats them as a special and highly optimized object.

However, many beginners make mistakes because they think of a String as simply "a sequence of characters".

In Java, Strings involve:

* objects
* memory management
* immutability
* optimization through the String Pool
* performance considerations
* specialized APIs

Understanding Strings deeply is essential before moving into advanced Java topics.

---

# Module 11 Structure

This module will be divided into the following chapters:

---

# Chapter 01 — Understanding Strings Internally

## Goals

Understand what Strings are and why Java designed them differently.

Topics:

* What is a String
* Why String is a class
* Primitive types vs objects
* Internal representation of text
* String immutability
* Why Strings cannot be changed
* Benefits of immutable objects
* Security implications
* Memory efficiency
* Performance considerations

---

# Chapter 02 — Creating Strings and the String Pool

## Goals

Understand how Java stores String objects.

Topics:

* String literals
* Using `new String()`
* String Pool concept
* Heap memory vs String Pool
* Object reuse
* Memory optimization
* `intern()`
* Common mistakes when creating Strings

---

# Chapter 03 — Basic String Inspection

## Goals

Learn how to analyze text.

Topics:

* `length()`
* `isEmpty()`
* `isBlank()`
* `charAt()`

Practice:

* character analysis
* text validation
* basic string inspection

---

# Chapter 04 — Extracting and Searching Text

## Goals

Manipulate portions of strings.

Topics:

* `substring()`
* `contains()`
* `startsWith()`
* `endsWith()`
* `indexOf()`
* `lastIndexOf()`

Practice:

* search systems
* text filtering
* extracting information

---

# Chapter 05 — Transforming Strings

## Goals

Learn how to modify text.

Topics:

* `replace()`
* `replaceFirst()`
* `toUpperCase()`
* `toLowerCase()`
* `trim()`
* `strip()`
* `repeat()`

Concepts:

* Why modifications create new Strings
* Performance implications
* Avoiding unnecessary objects

---

# Chapter 06 — Comparing Strings Correctly

## Goals

Understand String comparison.

Topics:

* `==`
* `equals()`
* `equalsIgnoreCase()`
* `compareTo()`

Deep concepts:

* Reference comparison
* Value comparison
* String Pool influence
* Why beginners misuse `==`

Practice:

* comparing usernames
* sorting text
* validating input

---

# Chapter 07 — Splitting and Joining Text

## Goals

Break and combine text efficiently.

Topics:

* `split()`
* `join()`

Practice:

* CSV-like text
* processing sentences
* rebuilding messages

---

# Chapter 08 — StringBuilder and Mutable Text

## Goals

Understand efficient text construction.

Topics:

* Problem with repeated String concatenation
* Immutable vs mutable objects
* StringBuilder purpose
* Internal behavior

Methods:

* `append()`
* `insert()`
* `delete()`
* `reverse()`
* `toString()`

Practice:

* building reports
* generating large texts

---

# Chapter 09 — StringBuffer and Thread Safety

## Goals

Understand the historical alternative.

Topics:

* StringBuilder vs StringBuffer
* Synchronization
* Thread safety concept
* When StringBuffer matters

---

# Chapter 10 — Practical Exercises

Build real applications:

## Exercise 1 — Palindrome Checker

Skills:

* iteration
* comparison
* String manipulation

---

## Exercise 2 — Password Validator

Validation rules:

* minimum length
* uppercase
* lowercase
* numbers
* special characters

Concepts:

* character analysis
* defensive programming

---

## Exercise 3 — Word Counter

Generate:

* total words
* total characters
* vowels
* consonants

---

## Exercise 4 — Text Formatter

Implement:

* capitalize words
* remove extra spaces
* normalize text

---

## Exercise 5 — String Comparison Lab

Analyze:

```java
==
equals()
equalsIgnoreCase()
compareTo()
```

Understand the differences.

---

## Exercise 6 — StringBuilder Performance

Compare:

```java
String text = "";

text += "hello";
```

against:

```java
StringBuilder builder = new StringBuilder();

builder.append("hello");
```

---

## Exercise 7 — Text Statistics Generator

Generate:

```
Text Report

Characters: 150
Words: 25
Average word length: 5.8
Longest word: programming
Shortest word: a
```

---

# Chapter 11 — Final Project

# Text Processing Toolkit

A complete console application for text analysis.

The project will contain:

```
src/
 ├── Main.java
 │
 ├── model/
 │    └── User.java
 │
 ├── service/
 │    ├── TextFormatter.java
 │    ├── PasswordValidator.java
 │    └── StringAnalyzer.java
 │
 └── util/
```

---

## Features

### Text Formatting

Examples:

Input:

```
   hello     JAVA world
```

Output:

```
Hello Java World
```

---

### Password Validation

Example:

```
Password: Java123
```

Result:

```
Invalid password

Missing:
- special character
```

---

### Word Statistics

Generate:

```
Text Statistics

Characters:
Words:
Vowels:
Consonants:
Longest word:
Shortest word:
```

---

### Search Operations

Examples:

```
Find:
"java"

Occurrences:
5
```

---

### String Comparison System

Demonstrate:

```
String A:
java

String B:
JAVA


equals:
false

equalsIgnoreCase:
true
```

---

### Efficient Text Generation

Use:

```
StringBuilder
```

to generate reports.

---

# Project Development Strategy

The final project will be developed progressively.

We will NOT create everything at once.

Development order:

---

## Phase 1

Create project structure.

Create:

```
model
service
util
```

packages.

---

## Phase 2

Implement text analysis.

Create:

```
StringAnalyzer.java
```

---

## Phase 3

Implement formatting.

Create:

```
TextFormatter.java
```

---

## Phase 4

Implement password validation.

Create:

```
PasswordValidator.java
```

---

## Phase 5

Integrate everything in:

```
Main.java
```

---

## Phase 6

Improve performance using:

```
StringBuilder
```

---

# Important Rule Before Starting Methods

Before learning:

```java
length()
substring()
replace()
split()
```

we must first understand the most important String concept:

# Why are Strings immutable?

This is the foundation of the entire String API.

If this concept is misunderstood, many later topics become confusing.

We need to understand:

* why this code does not modify the original String:

```java
String name = "Java";

name.toUpperCase();

System.out.println(name);
```

Output:

```
Java
```

not:

```
JAVA
```

because Strings cannot change after creation.

---

# Next Step

Proceed to:

# Chapter 01 — Understanding Strings Internally

We will start by understanding **what a String really is inside Java, why it is a class, and why immutability exists.**
