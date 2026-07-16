# Chapter 44 — Collection Comparison & Design Decisions

Throughout this module, we learned many collection types:

```text id="u8m3q5"
List
Set
Queue
Deque
Map
```

and their implementations:

```text id="p4m8x2"
ArrayList
LinkedList
HashSet
LinkedHashSet
TreeSet
PriorityQueue
ArrayDeque
HashMap
LinkedHashMap
TreeMap
```

Now we will stop focusing on individual classes and learn the most important skill:

> Choosing the correct collection for a real problem.

A professional Java developer does not memorize collections.

They analyze requirements.

---

# The Decision Process

Before choosing a collection, ask:

---

## Question 1

Do I need:

```text id="q7m3x9"
key → value relationship?
```

Example:

```text id="x5m8q2"
ID → Product
Name → Contact
```

If yes:

Use:

```java id="m4q8x1"
Map
```

---

## Question 2

Do I only need a group of objects?

Example:

```text id="v6m2q8"
Students
Products
Books
```

Then:

Use:

```text id="r8m3x5"
Collection
```

---

## Question 3

Do duplicates matter?

Example:

```text id="k5q9m2"
Can two students have same ID?
```

---

If duplicates are allowed:

```text id="z7m3x8"
List
```

---

If duplicates are forbidden:

```text id="p4m8x2"
Set
```

---

## Question 4

Does order matter?

Possible orders:

---

Insertion order:

```text id="n8m3q5"
LinkedHash
```

---

Sorted order:

```text id="w5q2m9"
Tree
```

---

No order:

```text id="x3m8q6"
Hash
```

---

# List Comparison

Main implementations:

```text id="m7q3x9"
ArrayList
LinkedList
```

---

# ArrayList

Internal:

```text id="c5m8q2"
Dynamic array
```

Example:

```text id="j8m3x5"
[ A ][ B ][ C ]
```

---

## Advantages

Excellent:

* Random access.
* Iteration.
* Searching by index.

Example:

```java id="p9m3x7"
list.get(100);
```

---

## Complexity

| Operation     | Complexity   |
| ------------- | ------------ |
| get(index)    | O(1)         |
| add(end)      | O(1) average |
| remove middle | O(n)         |
| search        | O(n)         |

---

## Use When

Most applications.

Examples:

* Products.
* Students.
* Books.

---

# LinkedList

Internal:

```text id="x8m2q5"
Node → Node → Node
```

Each node stores:

```text id="r5m8x2"
value

previous

next
```

---

## Advantages

Fast insert/remove at ends.

---

## Complexity

| Operation    | Complexity |
| ------------ | ---------- |
| add first    | O(1)       |
| remove first | O(1)       |
| get(index)   | O(n)       |
| search       | O(n)       |

---

## Use When

Frequent:

* Insertions.
* Removals.

Especially at beginning/end.

---

# ArrayList vs LinkedList

| Feature       | ArrayList | LinkedList |
| ------------- | --------- | ---------- |
| Internal      | Array     | Nodes      |
| get(index)    | ⭐⭐⭐       | ⭐          |
| add end       | ⭐⭐⭐       | ⭐⭐⭐        |
| remove middle | ⭐         | ⭐⭐         |
| Memory        | Less      | More       |
| Common choice | Yes       | Rare       |

---

# Professional Default

Most of the time:

```java id="m4x8q2"
ArrayList
```

is the correct choice.

---

# Set Comparison

Implementations:

```text id="q7m3x9"
HashSet
LinkedHashSet
TreeSet
```

---

# HashSet

Internal:

```text id="v5m8q2"
Hash table
```

---

Characteristics:

* No duplicates.
* No guaranteed order.

---

Performance:

| Operation | Complexity |
| --------- | ---------- |
| add       | O(1)       |
| remove    | O(1)       |
| contains  | O(1)       |

---

Use:

When uniqueness matters.

Example:

```text id="p8m3q5"
Unique usernames
Unique categories
```

---

# LinkedHashSet

Internal:

```text id="z6m2x8"
Hash table
+
Linked list
```

---

Adds:

```text id="w7q3m9"
Insertion order
```

---

Use:

Unique values + predictable order.

Example:

```text id="n5m8q2"
Recent searches
```

---

# TreeSet

Internal:

```text id="x4m8q3"
Tree structure
```

---

Adds:

```text id="k7m3q9"
Sorted order
```

---

Performance:

```text id="m5q8x2"
O(log n)
```

---

Use:

Sorted unique data.

Example:

```text id="p9m2x6"
Ranking
Alphabetical lists
```

---

# Set Comparison

| Feature              | HashSet | LinkedHashSet | TreeSet |
| -------------------- | ------- | ------------- | ------- |
| Duplicate prevention | Yes     | Yes           | Yes     |
| Order                | None    | Insert        | Sorted  |
| Speed                | Fastest | Fast          | Slower  |
| Structure            | Hash    | Hash + List   | Tree    |

---

# Map Comparison

Implementations:

```text id="r8m3q5"
HashMap
LinkedHashMap
TreeMap
```

---

# HashMap

Default choice.

Characteristics:

* Fast lookup.
* No order.

Example:

```text id="x5m8q2"
User ID → User
```

---

Performance:

```text id="m7q3x9"
get()
put()

O(1)
```

---

# LinkedHashMap

Adds:

```text id="q4m8x1"
Insertion order
```

Example:

```text id="v6m2q8"
User history
```

---

# TreeMap

Adds:

```text id="p5m9x3"
Sorted keys
```

Example:

```text id="z8m3q5"
A-Z contacts
```

---

# Map Comparison

| Feature  | HashMap | LinkedHashMap | TreeMap |
| -------- | ------- | ------------- | ------- |
| Speed    | ⭐⭐⭐     | ⭐⭐⭐           | ⭐⭐      |
| Order    | No      | Insert        | Sorted  |
| Memory   | Low     | Medium        | Medium  |
| Internal | Hash    | Hash + List   | Tree    |

---

# Queue Comparison

---

# LinkedList Queue

FIFO:

```text id="x7m3q9"
First In First Out
```

Example:

```text id="m8q2x5"
Printer jobs
```

---

# PriorityQueue

Order:

```text id="p4m8x1"
Priority
```

Example:

```text id="z5m2q8"
Emergency tasks
```

---

# Deque

Implementation:

```java id="q7m3x9"
ArrayDeque
```

Allows:

```text id="v5m8q2"
First
Last
```

operations.

---

# Real Scenario Decisions

---

# Scenario 1

Store students.

Requirements:

* Duplicates allowed.
* Maintain registration order.

Choice:

```java id="m4x8q2"
ArrayList<Student>
```

---

# Scenario 2

Store unique email addresses.

Requirements:

* No duplicates.

Choice:

```java id="x8m3q5"
HashSet<String>
```

---

# Scenario 3

Store contacts alphabetically.

Requirements:

* Search by name.
* Display A-Z.

Choice:

```java id="r7m3q9"
TreeMap<String, Contact>
```

---

# Scenario 4

Process support tickets.

Requirements:

* Highest priority first.

Choice:

```java id="p5m8x2"
PriorityQueue<Task>
```

---

# Scenario 5

Store product inventory.

Requirements:

* Search by ID.

Choice:

```java id="z6m3q8"
HashMap<Integer, Product>
```

---

# The Golden Rules

Remember:

---

## Need indexes?

```text id="w5q2m9"
List
```

---

## Need uniqueness?

```text id="k8m3x5"
Set
```

---

## Need key/value?

```text id="n7m3q9"
Map
```

---

## Need processing order?

```text id="x4m8q2"
Queue
```

---

# Final Project Preparation

Our Library Management System will need:

---

Books:

Need search and organization.

Possible:

```java id="m5q8x2"
Map<String, Book>
```

---

Users:

Need unique registration.

Possible:

```java id="v8m3q5"
Set<User>
```

---

Borrowing history:

Need order.

Possible:

```java id="p7m3x9"
List<BorrowRecord>
```

---

Waiting queue:

Need FIFO.

Possible:

```java id="z4m8q2"
Queue<User>
```

---

Reports:

Need sorting.

Use:

```text id="r6m3x8"
Comparable
Comparator
```

---

# Exercise Task

For each problem choose a collection:

---

### 1.

A game stores player rankings:

```text id="c5m8q2"
Need sorted scores
```

---

### 2.

A website stores user sessions:

```text id="x8m3q5"
Search by session ID
```

---

### 3.

A playlist stores songs:

```text id="q7m3x9"
Order matters
Duplicates allowed
```

---

### 4.

A hospital receives emergency patients:

```text id="m4x8q2"
Highest priority first
```

---

### 5.

A dictionary stores words:

```text id="p5m9x3"
Unique words
Alphabetical order
```

---

# ✔️ Next Step

In **Chapter 45 — Final Project: Library Management System (Planning Phase)** we will begin the final project.

We will define:

* Requirements.
* Domain classes.
* Package structure.
* Which collections each part will use.
* Development roadmap.

We will build it progressively, without providing the complete solution upfront.
