# Final Project — Text Processing Toolkit

## Project Objective

Congratulations!

You have completed all the theoretical chapters and guided exercises of **Module 11 — Strings**.

Now it's time to integrate everything you've learned into a single application.

This project is intentionally larger than the previous exercises. Instead of learning new APIs, your goal is to **apply** the knowledge you've already acquired while practicing software organization and clean architecture.

Just like in a real-world project, **you will build it incrementally**. We will not write the entire application in one go.

---

# Learning Goals

By completing this project, you will reinforce:

* Working with immutable Strings
* Proper use of the String Pool concepts
* Choosing between `String` and `StringBuilder`
* Splitting responsibilities into classes
* Reusing existing code
* Building reusable services
* Designing simple object-oriented applications
* Organizing a Java project into packages

---

# Functional Requirements

The application must provide the following features:

### 1. Text Formatter

* Remove extra spaces
* Normalize text
* Capitalize words

---

### 2. Password Validator

Validate:

* Minimum length
* Uppercase letters
* Lowercase letters
* Digits
* Special characters

---

### 3. Palindrome Checker

Determine whether:

* Words
* Sentences

are palindromes.

---

### 4. String Comparison

Support:

* `==`
* `equals()`
* `equalsIgnoreCase()`
* `compareTo()`

Explain the result of each comparison.

---

### 5. Text Statistics

Generate:

* Character count
* Word count
* Vowel count
* Consonant count
* Longest word
* Shortest word
* Average word length

---

### 6. Report Generation

Generate formatted reports using:

```java
StringBuilder
```

---

# Project Structure

Continue following the architecture used throughout the Bootcamp.

```text
src/
│
├── Main.java
│
├── model/
│     ├── User.java
│     └── TextStatistics.java
│
├── service/
│     ├── PasswordValidator.java
│     ├── PalindromeChecker.java
│     ├── StringAnalyzer.java
│     ├── StringComparisonService.java
│     ├── TextFormatter.java
│     └── ReportBuilder.java
│
└── util/
```

Notice that:

* `model` stores data
* `service` contains business logic
* `Main` coordinates the application
* `util` remains available for future helper classes

---

# Suggested Development Order

Build the project in small, testable steps.

## Phase 1 — Project Setup

Create the package structure.

Create all empty classes.

Verify the project compiles.

---

## Phase 2 — Text Formatter

Implement:

```text
removeExtraSpaces()

capitalizeWords()

normalizeText()
```

Test independently.

---

## Phase 3 — Password Validator

Reuse your previous implementation.

Improve it if necessary.

---

## Phase 4 — Palindrome Checker

Reuse the solution from the guided exercise.

Ensure it handles sentences correctly.

---

## Phase 5 — String Analyzer

Implement:

* Characters
* Words
* Vowels
* Consonants

Then:

```text
generateStatistics()
```

---

## Phase 6 — String Comparison

Implement every comparison method.

Generate readable comparison reports.

---

## Phase 7 — Report Builder

Generate:

```text
Password Report

Statistics Report

Comparison Report

Palindrome Report
```

Use only:

```java
StringBuilder
```

for report generation.

---

## Phase 8 — Main

Finally, connect everything together.

The `Main` class should remain relatively small.

Its responsibility is to:

* Create objects
* Call services
* Display reports

Not implement business logic.

---

# Suggested Menu

A simple console menu is enough.

```text
==============================

TEXT PROCESSING TOOLKIT

==============================

1 - Format Text

2 - Validate Password

3 - Analyze Text

4 - Compare Strings

5 - Check Palindrome

0 - Exit

Choice:
```

You may implement the menu using a `switch` statement and `Scanner` for user input.

---

# Example Flow

User chooses:

```text
1
```

Program asks:

```text
Enter the text:
```

User types:

```text
   java      bootcamp
```

Output:

```text
Java Bootcamp
```

---

User chooses:

```text
3
```

Program:

```text
Enter text:
```

Output:

```text
Characters : 14

Words : 2

Vowels : 5

Consonants : 8

Average : 6.5
```

---

# Design Guidelines

Keep responsibilities separated.

Good design:

```text
Main

↓

TextFormatter

↓

StringAnalyzer

↓

ReportBuilder

↓

Console
```

Avoid:

```text
Main

↓

Everything
```

If `Main.java` starts growing excessively, ask yourself:

> "Should this code belong in a service instead?"

---

# Common Mistakes to Avoid

### ❌ Putting all logic in `Main`

Keep business logic in service classes.

---

### ❌ Duplicating code

If you've already written a method:

```java
countWords()
```

reuse it instead of writing a new version.

---

### ❌ Using `==` for content comparison

Always ask yourself:

> "Am I comparing references or text?"

---

### ❌ Using String concatenation to build reports

Prefer:

```java
StringBuilder
```

---

### ❌ Mixing responsibilities

For example:

```text
PasswordValidator

↓

prints reports
```

No.

Validators validate.

Report builders create reports.

`Main` displays them.

---

# Suggested Bonus Features (Optional)

If you finish early, try adding one or more of these:

* Count digits
* Count punctuation marks
* Count whitespace characters
* Estimate reading time (e.g., 200 words/minute)
* Display the most frequent character
* Reverse the entire text
* Display unique words in alphabetical order (using topics you'll learn later, if you wish to experiment)

These are **optional** and not required for Module 11.

---

# Success Criteria

By the end of this project, you should be able to:

* Explain why Strings are immutable
* Explain the String Pool
* Know when to use `equals()` vs `==`
* Know when `StringBuilder` is the correct choice
* Design reusable services
* Separate data from behavior
* Build console applications with clean package organization

If you can comfortably build this project without constantly referring back to the lessons, you've achieved the objectives of Module 11.

---

# Module 11 Review

Throughout this module, you learned:

## String Fundamentals

* ✅ What a `String` is
* ✅ Why `String` is a class
* ✅ Immutability
* ✅ String Pool
* ✅ String literals vs `new String()`

---

## String API

* ✅ `length()`
* ✅ `isEmpty()`
* ✅ `isBlank()`
* ✅ `charAt()`
* ✅ `substring()`
* ✅ `contains()`
* ✅ `startsWith()`
* ✅ `endsWith()`
* ✅ `indexOf()`
* ✅ `lastIndexOf()`
* ✅ `replace()`
* ✅ `replaceFirst()`
* ✅ `toUpperCase()`
* ✅ `toLowerCase()`
* ✅ `trim()`
* ✅ `strip()`
* ✅ `repeat()`

---

## String Comparison

* ✅ `==`
* ✅ `equals()`
* ✅ `equalsIgnoreCase()`
* ✅ `compareTo()`

---

## Text Processing

* ✅ `split()`
* ✅ `join()`

---

## Mutable Text

* ✅ `StringBuilder`
* ✅ `append()`
* ✅ `insert()`
* ✅ `delete()`
* ✅ `reverse()`
* ✅ `toString()`

---

## Thread-Safe Alternative

* ✅ `StringBuffer` (conceptual introduction)

---

# Module Completion Report (Bootcamp Central Control)

Copy the following report to your **Bootcamp Central Control** chat after you finish the project.

```text
========================================
BOOTCAMP JAVA — MODULE COMPLETION REPORT
========================================

Module Number:
11

Module Name:
Strings

Status:
Completed

Completion Date:
(Fill when completed)

Final Project:
Text Processing Toolkit

Topics Mastered:

- String Fundamentals
- Immutability
- String Pool
- String API
- String Comparison
- Text Processing
- StringBuilder
- StringBuffer (Introduction)

Exercises Completed:

- Palindrome Checker
- Password Validator
- Word Counter
- Text Formatter
- String Comparison
- StringBuilder Practice
- Text Statistics

Overall Confidence (1–10):
(Your self-assessment)

Notes:
(Add personal observations if desired.)

========================================
```

---

# 🎉 Congratulations!

You have completed **Module 11 — Strings**.

This module is a major milestone because Strings are one of the most frequently used types in Java. The concepts you've learned here—especially **immutability**, **reference vs. content comparison**, and **efficient text construction**—will appear constantly in professional Java development.

