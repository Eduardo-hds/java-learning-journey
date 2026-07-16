# Chapter 45 — Final Project: Library Management System (Planning Phase)

We have completed the core concepts of the Collections Framework.

Now we will apply everything learned in a complete application.

The final project for this module will be:

# 📚 Library Management System

A console-based application that manages:

* Books.
* Users.
* Borrowing operations.
* Queues.
* Reports.
* Searching.
* Sorting.

The objective is not only to make the program work.

The objective is to practice **choosing the correct collection for each problem**.

---

# Project Objective

Build a system capable of:

## Books

The system must:

* Register books.
* Search books.
* Display books.
* Prevent duplicate books.

---

## Users

The system must:

* Register users.
* Prevent duplicate registrations.
* Search users.

---

## Borrowing

The system must:

* Borrow books.
* Return books.
* Keep borrowing history.

---

## Queue

The system must:

* Manage users waiting for unavailable books.

---

## Reports

The system must:

* Sort books.
* Sort users.
* Generate reports.

---

# First Step: Analyze Requirements

Before writing code, we decide:

> Which collection solves each problem?

This is the most important skill from this module.

---

# Domain Objects

Our model package:

```text
src/
│
├── Main.java
│
├── model/
│
│    ├── Book.java
│    ├── User.java
│    ├── BorrowRecord.java
│    └── Task.java
│
├── service/
│
│    ├── LibraryService.java
│    ├── UserService.java
│    ├── BookService.java
│    └── ReportService.java
│
└── util/
```

---

# Entity 1 — Book

A book needs:

```text id="m5q8x2"
id
title
author
category
available
```

Example:

```text
Book:

ID: 101
Title: Clean Code
Author: Robert Martin
Category: Programming
Available: true
```

---

# Choosing Collection For Books

Question:

How will we search?

Possible:

```text id="x8m3q5"
Search by ID
Search by title
Search by author
```

---

## Option 1 — List

```java
List<Book>
```

Problem:

Searching:

```java
findBook(101)
```

requires:

```text
loop through all books
```

Complexity:

```text
O(n)
```

---

## Option 2 — Map

```java
Map<Integer, Book>
```

Structure:

```text
101 → Clean Code
102 → Java Effective
103 → Algorithms
```

Search:

```java
books.get(101)
```

Average:

```text
O(1)
```

---

Decision:

```java
Map<Integer, Book>
```

---

# Entity 2 — User

A user:

```text
id
name
email
```

Example:

```text
User:

ID: 10
Name: Eduardo
Email: user@email.com
```

---

# Prevent Duplicate Users

Question:

Can two users have the same ID?

No.

---

Possible:

```java
Set<User>
```

because:

```text
No duplicates
```

---

But we also need:

```text
Search by ID
```

Better:

```java
Map<Integer, User>
```

---

Decision:

```java
Map<Integer, User>
```

---

# Entity 3 — Borrowing History

A user may borrow multiple books.

Example:

```text
History:

Book A
Book B
Book C
```

Order matters.

We need:

* First borrowed.
* Last borrowed.

---

Decision:

```java
List<BorrowRecord>
```

---

# Entity 4 — Waiting Queue

Scenario:

Book unavailable.

Example:

```text
Clean Code

Maria waiting
John waiting
Carlos waiting
```

When returned:

First person receives it.

---

FIFO:

```text
First In First Out
```

---

Decision:

```java
Queue<User>
```

---

# Entity 5 — Reports

Reports need sorting.

Examples:

Books:

```text
A-Z
```

Users:

```text
Name
```

---

Use:

```text
Comparable
Comparator
```

---

# Final Collection Architecture

Our system:

```text
Library Management System


Books

Map<Integer, Book>



Users

Map<Integer, User>



Borrow History

List<BorrowRecord>



Waiting Queue

Queue<User>



Reports

Comparable + Comparator
```

---

# Service Responsibilities

Important design rule:

> Main should not contain business logic.

---

Wrong:

```java
public class Main {

    create book;
    validate user;
    borrow book;

}
```

---

Correct:

```text
Main

  |
  v

Services

  |
  v

Collections
```

---

# BookService

Responsible for:

```text
Add book

Remove book

Search book

List books
```

Uses:

```java
Map<Integer, Book>
```

---

# UserService

Responsible for:

```text
Register user

Remove user

Search user
```

Uses:

```java
Map<Integer, User>
```

---

# LibraryService

Responsible for:

```text
Borrow book

Return book

Queue management
```

Uses:

```java
Queue<User>
```

---

# ReportService

Responsible for:

```text
Generate reports

Sort collections
```

Uses:

```text
Comparator
Comparable
```

---

# Development Roadmap

We will build the project in stages.

---

# Phase 1 — Domain Models

Create:

```text
Book.java

User.java

BorrowRecord.java
```

Learn:

* Object design.
* equals/hashCode.
* Comparable preparation.

---

# Phase 2 — Book Management

Implement:

```text
BookService
```

Features:

* Add books.
* Search books.
* Remove books.

Collection:

```java
Map<Integer, Book>
```

---

# Phase 3 — User Management

Implement:

```text
UserService
```

Features:

* Register users.
* Search users.

Collection:

```java
Map<Integer, User>
```

---

# Phase 4 — Borrow System

Implement:

* Borrow.
* Return.
* History.

Collections:

```java
List
Queue
```

---

# Phase 5 — Reports

Implement:

Sorting:

* Books by title.
* Books by author.
* Users by name.

Using:

```java
Comparable
Comparator
```

---

# Phase 6 — Improvements

Add:

* Validation.
* Better menu.
* Exception handling review.
* Clean organization.

---

# Initial Project Structure

Final:

```text
src/
│
├── Main.java
│
├── model/
│   ├── Book.java
│   ├── User.java
│   └── BorrowRecord.java
│
├── service/
│   ├── BookService.java
│   ├── UserService.java
│   ├── LibraryService.java
│   └── ReportService.java
│
└── util/
    ├── BookComparator.java
    └── UserComparator.java
```

---

# Important Lessons From This Project

This project combines:

✅ List
✅ Set
✅ Map
✅ Queue
✅ Comparable
✅ Comparator
✅ Iterator
✅ Collections utilities

---

# Exercise Task

Before coding, answer:

Choose the collection:

---

## 1.

Store books by ISBN:

```text
Need fast lookup
```

Answer:

?

---

## 2.

Store borrowing history:

```text
Order matters
```

Answer:

?

---

## 3.

Store waiting users:

```text
First person gets the book
```

Answer:

?

---

## 4.

Store unique categories:

```text
No duplicates
```

Answer:

?

---

## 5.

Store contacts alphabetically:

```text
Search by name + sorted
```

Answer:

?

---

# ✔️ Next Step

In **Chapter 46 — Final Project: Creating Domain Models** we will start implementation.

We will create:

* `Book`
* `User`
* `BorrowRecord`

and discuss:

* Why objects stored in collections need `equals()` and `hashCode()`.
* How collections compare objects internally.
* Preparing models for `Set`, `Map`, and sorting.
