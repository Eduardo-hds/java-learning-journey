# Chapter 10 — Comparing Set Implementations

We have now studied the three main `Set` implementations:

* `HashSet`
* `LinkedHashSet`
* `TreeSet`

Each one solves a similar problem:

> Store unique elements.

But each one makes different design decisions.

The important skill is not memorizing classes.

The important skill is answering:

> "What behavior does my application need?"

---

# Learning Objectives

By the end of this chapter, you should be able to:

* Compare all `Set` implementations.
* Choose the correct implementation for a scenario.
* Understand the trade-offs between speed, memory, and ordering.
* Avoid common collection selection mistakes.

---

# The Three Main Questions

Before choosing a `Set`, ask:

## Question 1

Do I need sorting?

If yes:

```java
TreeSet
```

---

## Question 2

Do I need insertion order?

If yes:

```java
LinkedHashSet
```

---

## Question 3

Do I only need uniqueness?

If yes:

```java
HashSet
```

---

# Quick Decision Diagram

```text
                 Need a Set?
                    |
                    |
          Do you need sorted data?
                    |
          -----------------------
          |                     |
         Yes                    No
          |                     |
      TreeSet          Need insertion order?
                              |
                    -------------------
                    |                 |
                   Yes                No
                    |                 |
             LinkedHashSet       HashSet
```

---

# HashSet Review

## Purpose

Fast unique storage.

Example:

```java
Set<String> users = new HashSet<>();
```

---

## Internal Structure

Conceptually:

```text
Hash Table

Bucket
 |
 +-- Object
```

---

## Characteristics

| Feature         | Result      |
| --------------- | ----------- |
| Duplicates      | Not allowed |
| Order           | None        |
| Sorting         | None        |
| Access by index | No          |

---

## Performance

Average:

| Operation | Complexity |
| --------- | ---------- |
| add       | O(1)       |
| remove    | O(1)       |
| contains  | O(1)       |

---

## Best Use Cases

### Checking membership

Example:

```java
Set<String> bannedUsers = new HashSet<>();

if(bannedUsers.contains(username)){
    blockUser();
}
```

---

### Removing duplicates

Example:

Input:

```text
Java
Java
Spring
Java
```

Result:

```text
Java
Spring
```

---

### Large collections where order does not matter

---

# LinkedHashSet Review

## Purpose

Unique elements + insertion order.

Example:

```java
Set<String> history = new LinkedHashSet<>();
```

---

## Internal Structure

Conceptually:

```text
Hash Table

+

Linked List
```

Example:

```text
Bucket

A

B

C


Insertion:

A <-> B <-> C
```

---

## Characteristics

| Feature         | Result          |
| --------------- | --------------- |
| Duplicates      | Not allowed     |
| Order           | Insertion order |
| Sorting         | None            |
| Access by index | No              |

---

## Performance

Average:

| Operation | Complexity |
| --------- | ---------- |
| add       | O(1)       |
| remove    | O(1)       |
| contains  | O(1)       |

Slightly slower than HashSet.

---

## Best Use Cases

### Unique history

Example:

Recently searched terms:

```text
Java
Spring
SQL
```

Need:

* no duplicates,
* same order user entered.

---

### Predictable reports

Example:

Generating:

```text
1. Sales
2. Inventory
3. Customers
```

---

# TreeSet Review

## Purpose

Unique elements + sorted order.

Example:

```java
Set<Integer> ranking = new TreeSet<>();
```

---

## Internal Structure

Conceptually:

```text
Balanced Tree

        50

      /    \

    20      80
```

---

## Characteristics

| Feature         | Result      |
| --------------- | ----------- |
| Duplicates      | Not allowed |
| Order           | Sorted      |
| Sorting         | Automatic   |
| Access by index | No          |

---

## Performance

| Operation | Complexity |
| --------- | ---------- |
| add       | O(log n)   |
| remove    | O(log n)   |
| contains  | O(log n)   |

---

## Best Use Cases

### Ranking

Example:

```text
1000
800
500
200
```

---

### Sorted reports

Example:

Employees ordered by salary.

---

### Range queries

Example:

Find values:

```text
between 100 and 500
```

---

# Complete Comparison Table

| Feature            | HashSet    | LinkedHashSet      | TreeSet  |
| ------------------ | ---------- | ------------------ | -------- |
| Unique values      | ✅          | ✅                  | ✅        |
| Insertion order    | ❌          | ✅                  | ❌        |
| Sorted order       | ❌          | ❌                  | ✅        |
| Index access       | ❌          | ❌                  | ❌        |
| Internal structure | Hash table | Hash + linked list | Tree     |
| add performance    | O(1) avg   | O(1) avg           | O(log n) |
| Memory usage       | Lowest     | Medium             | Highest  |
| Complexity         | Lowest     | Medium             | Higher   |

---

# Scenario Analysis

Now let's apply decision-making.

---

# Scenario 1 — Registered Emails

Requirement:

* Emails must be unique.
* Order does not matter.

Example:

```text
john@email.com
mary@email.com
alex@email.com
```

Choice:

```java
HashSet<String>
```

Why?

* Fast lookup.
* No need for order.

---

# Scenario 2 — User Permissions

Example:

```text
READ
WRITE
DELETE
```

Requirement:

* No duplicates.
* Display permissions in configuration order.

Choice:

```java
LinkedHashSet<String>
```

Why?

Keeps order.

---

# Scenario 3 — Game Ranking

Example:

```text
9000 points
7000 points
5000 points
```

Requirement:

* No duplicates.
* Always sorted.

Choice:

```java
TreeSet<Player>
```

with:

```java
Comparator
```

---

# Scenario 4 — Remove Duplicate Words

Input:

```text
Java Java Spring SQL Java
```

Requirement:

Only unique words.

Choice:

```java
HashSet<String>
```

---

# Scenario 5 — Recently Viewed Products

Requirement:

* Product cannot repeat.
* Show in order viewed.

Choice:

```java
LinkedHashSet<Product>
```

---

# Scenario 6 — Sorted Employee Names

Requirement:

Display:

```text
Ana
Bruno
Carlos
```

Automatically.

Choice:

```java
TreeSet<String>
```

---

# Memory Trade-Off

There is a pattern:

More features require more memory.

---

## HashSet

Stores:

```text
Value
Hash information
```

Lowest overhead.

---

## LinkedHashSet

Adds:

```text
Previous reference
Next reference
```

for order.

---

## TreeSet

Adds:

```text
Tree references
Balancing information
```

for sorting.

---

# Performance Trade-Off

The pattern:

```
More behavior
      ↓
More internal work
      ↓
More memory and complexity
```

Example:

Fastest:

```text
HashSet
```

Then:

```text
LinkedHashSet
```

Then:

```text
TreeSet
```

---

# Common Mistakes

## Mistake 1 — Always choosing HashSet

Example:

You need:

```text
A
B
C
```

in insertion order.

HashSet fails the requirement.

---

## Mistake 2 — Always choosing TreeSet

Sorting has a cost.

If you only need uniqueness:

TreeSet is unnecessary.

---

## Mistake 3 — Thinking LinkedHashSet sorts

It does not.

Example:

Inserted:

```text
Z
A
M
```

Output:

```text
Z
A
M
```

not:

```text
A
M
Z
```

---

## Mistake 4 — Forgetting equals/hashCode

For:

```java
Set<MyObject>
```

always consider:

* equality,
* hashing.

---

# Practical Rule Used in Professional Java

When choosing a Set:

Start with:

```java
HashSet
```

Ask:

> Do I need order?

If yes:

```java
LinkedHashSet
```

Ask:

> Do I need sorting?

If yes:

```java
TreeSet
```

---

# Chapter Summary

You learned:

* `HashSet` focuses on speed.
* `LinkedHashSet` focuses on predictable iteration.
* `TreeSet` focuses on automatic sorting.
* Every feature has a cost.
* The correct collection depends on the requirement.

The main principle:

> Choose collections based on behavior requirements, not because one implementation is "better".

---

# ✔️ Next Step

In **Chapter 11 — Queue Interface**, we will move to another branch of the Collections Framework.

You will learn how Java represents processing lines, FIFO behavior, task scheduling concepts, and why queues are different from lists and sets.
