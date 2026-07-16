# Bootcamp Java — Module 13: Collections Framework

Welcome to **Module 13**.

This module marks an important transition in your Java journey.

Until now, you've mostly worked with **single objects** or **fixed-size arrays**. Real-world applications, however, constantly deal with **dynamic groups of objects**:

* Lists of customers
* Products in inventory
* Books in a library
* Messages
* Orders
* Tasks
* Employees
* Cache entries

Managing these efficiently is exactly why the **Java Collections Framework (JCF)** exists.

Unlike previous modules, this one is heavily focused on **design decisions**. Throughout the module, you'll repeatedly answer questions like:

> "Why would I choose this collection instead of another?"

rather than simply:

> "How do I use this class?"

---

# Module Roadmap

## Part I — Foundations

### Chapter 00 — Arrays vs Collections

* Problems with arrays
* Fixed size limitations
* Why collections were created
* Dynamic data structures
* Real-world motivation

---

### Chapter 01 — Collections Framework Overview

* What is the Collections Framework
* Why it exists
* Framework philosophy
* Benefits
* Collections hierarchy
* Interfaces vs implementations
* Collection vs Collections
* Iterable interface

---

## Part II — Lists

### Chapter 02 — The List Interface

* Ordered collections
* Index-based access
* Duplicate elements
* Common operations

---

### Chapter 03 — ArrayList

* Internal dynamic array
* Capacity vs size
* Resizing
* Performance
* Memory considerations
* CRUD operations
* Iteration

---

### Chapter 04 — LinkedList

* Doubly linked list
* Nodes
* References
* Insertions
* Removals
* Sequential access

---

### Chapter 05 — ArrayList vs LinkedList

* Internal comparison
* Complexity analysis
* Real-world examples
* Memory usage
* Which one to choose

---

## Part III — Sets

### Chapter 06 — Set Interface

* Uniqueness
* Duplicate prevention
* Equality concepts

---

### Chapter 07 — HashSet

* Hash tables
* Hashing concept
* hashCode()
* equals()
* Performance

---

### Chapter 08 — LinkedHashSet

* Preserving insertion order
* Internal structure
* When ordering matters

---

### Chapter 09 — TreeSet

* Binary search trees
* Natural ordering
* Comparable integration
* Comparator integration
* Sorted collections

---

### Chapter 10 — Comparing Set Implementations

* HashSet
* LinkedHashSet
* TreeSet

Performance comparison

Memory comparison

Ordering comparison

---

## Part IV — Queues

### Chapter 11 — Queue Interface

* FIFO concept
* Queue operations
* Real-world examples

---

### Chapter 12 — PriorityQueue

* Priority ordering
* Heap concept
* Internal behavior
* Practical applications

---

### Chapter 13 — Deque and ArrayDeque

* Double-ended queues
* Queue behavior
* Stack behavior
* Why Stack is considered legacy

---

## Part V — Maps

### Chapter 14 — Map Interface

* Keys
* Values
* Associations
* Why Map does not extend Collection

---

### Chapter 15 — HashMap

* Hash table internals
* Buckets
* Hash collisions
* put()
* get()
* remove()
* containsKey()

---

### Chapter 16 — LinkedHashMap

* Preserving insertion order
* Internal linked structure

---

### Chapter 17 — TreeMap

* Sorted keys
* Tree structure
* NavigableMap basics

---

### Chapter 18 — Comparing Map Implementations

* HashMap
* LinkedHashMap
* TreeMap

Performance

Ordering

Memory

Use cases

---

## Part VI — Iteration

### Chapter 19 — Iterator

* Iterator interface
* Safe traversal
* remove()
* ConcurrentModificationException

---

### Chapter 20 — ListIterator

* Bidirectional iteration
* Updating during iteration
* Differences from Iterator

---

## Part VII — Sorting

### Chapter 21 — Comparable

* Natural ordering
* compareTo()

---

### Chapter 22 — Comparator

* Multiple sorting strategies
* Lambda preview (without Streams)
* Reusable comparators

---

### Chapter 23 — Sorting Collections

* Collections.sort()
* List.sort()
* Stability
* Practical examples

---

## Part VIII — Collections Utility Class

### Chapter 24 — Collections Utility Methods

* reverse()
* shuffle()
* max()
* min()
* frequency()
* binarySearch() *(optional overview)*
* unmodifiableList()

---

## Part IX — Practice Projects

### Chapter 25 — Student Management

Using ArrayList

---

### Chapter 26 — Product Inventory

Using HashMap

---

### Chapter 27 — Unique Word Counter

Using Set

---

### Chapter 28 — Task Queue

Using Queue

---

### Chapter 29 — Contact Manager

Using Map

---

### Chapter 30 — Sorting Practice

Comparable

Comparator

Multiple sorting strategies

---

### Chapter 31 — Collection Comparison Challenge

Solve the same problem using:

* ArrayList
* LinkedList

Analyze:

* readability
* performance
* maintainability

---

## Part X — Final Project

### Chapter 32 — Library Management System

Build the project incrementally throughout the module.

Features include:

### Book Management

* Register books
* Remove books
* Search books
* List books

---

### User Management

* Register users
* Prevent duplicate registrations
* Search users

---

### Borrow System

* Borrow books
* Return books
* Queue waiting users for unavailable books

---

### Reports

* Books by author
* Books by title
* Borrowed books
* Available books
* Sorted reports

---

### Required Collections

The project must use:

* List
* Set
* Map
* Queue

---

### Required Concepts

* Comparable
* Comparator
* Iterator
* Collections utility methods
* Package organization
* Service layer
* Model layer

---

# Exercises Throughout the Module

We'll progressively build:

* Student Management
* Product Inventory
* Unique Word Counter
* Task Queue
* Contact Manager
* Sorting Practice
* Collection Comparison
* Library Management System

Each chapter introduces concepts that are immediately applied in one of these projects.

---

# Skills You'll Have After This Module

By the end of Module 13, you will be able to:

* Choose the appropriate collection for a given problem.
* Explain the trade-offs between different collection implementations.
* Understand the high-level internal structure of the main collections.
* Analyze conceptual time complexity (Big-O) for common operations.
* Work confidently with lists, sets, queues, deques, and maps.
* Sort objects using both `Comparable` and `Comparator`.
* Safely iterate and modify collections with `Iterator` and `ListIterator`.
* Use the `Collections` utility class effectively.
* Structure larger applications that rely on multiple collection types.
* Design applications based on the strengths of each collection rather than using `ArrayList` by default.

---

# Final Project Preview

Throughout this module, you'll progressively build a **Library Management System**, not all at once.

The project will evolve chapter by chapter as new concepts are introduced:

* **Models (`model/`)**: `Book`, `User`, `Loan`
* **Services (`service/`)**: `LibraryService`, `UserService`, `LoanService`, `ReportService`
* **Entry Point**: `Main.java`
* **Utilities (`util/`)**: helper classes as needed

By the end of the module, the application will demonstrate the practical use of every major collection covered, following the same layered architecture established in previous modules.

---

## ✔️ Next Step

We will begin with **Chapter 00 — Arrays vs Collections**, where we'll compare fixed-size arrays with dynamic collections, understand the limitations of arrays, and build the motivation for the Java Collections Framework before exploring its hierarchy in Chapter 01.
