# Chapter 08 — LinkedHashSet

In the previous chapter, we learned about `HashSet`.

`HashSet` solved one important problem:

> "I need unique elements."

However, it introduced a limitation:

> "I don't care about order."

But what happens when we need **both**?

Example:

* A list of recently visited pages.
* A list of unique users in the order they joined.
* A history of unique searches.
* A list of permissions where display order matters.

For these cases, Java provides:

```java
LinkedHashSet
```

---

# Learning Objectives

By the end of this chapter, you should understand:

* What `LinkedHashSet` is.
* Why it exists.
* How it differs from `HashSet`.
* How insertion order is maintained.
* Internal implementation concept.
* Performance characteristics.
* Memory trade-offs.
* When to use and avoid `LinkedHashSet`.

---

# What is LinkedHashSet?

`LinkedHashSet` is a `Set` implementation that:

* prevents duplicates,
* preserves insertion order,
* uses hashing internally.

Example:

```java
Set<String> names = new LinkedHashSet<>();

names.add("Alice");
names.add("Bob");
names.add("Charlie");
```

Iteration:

```text
Alice
Bob
Charlie
```

The insertion order is preserved.

---

# Why Does LinkedHashSet Exist?

Let's compare two requirements.

---

## Requirement 1

Store unique usernames.

Order does not matter.

Example:

```text
john
mary
alex
```

Best choice:

```java
HashSet
```

---

## Requirement 2

Store unique usernames, but display them in registration order.

Example:

```text
1. john
2. mary
3. alex
```

Now `HashSet` is not enough.

Because:

```java
HashSet
```

does not guarantee iteration order.

We need:

```java
LinkedHashSet
```

---

# Internal Implementation

`LinkedHashSet` combines two concepts:

1. Hash table
2. Linked list

Conceptually:

```text
             Hash Table

Bucket 0
   |
   +--> Alice


Bucket 1
   |
   +--> Charlie


Bucket 2
   |
   +--> Bob



Insertion order:

Alice <-> Bob <-> Charlie
```

The hash structure provides:

* fast lookup.

The linked structure provides:

* predictable iteration order.

---

# HashSet vs LinkedHashSet Internally

## HashSet

Only hash structure:

```text
Bucket
 |
 +--> Object
```

Purpose:

Fast lookup.

---

## LinkedHashSet

Hash structure + linked ordering:

```text
Bucket
 |
 +--> Object


Object <-> Object <-> Object
```

Purpose:

Fast lookup + ordered traversal.

---

# Creating LinkedHashSet

Recommended style:

```java
Set<String> names = new LinkedHashSet<>();
```

Notice:

Variable type:

```java
Set
```

Implementation:

```java
LinkedHashSet
```

We keep programming against the interface.

---

# Basic Operations

The API is almost identical to `HashSet`.

---

## Adding Elements

```java
names.add("Alice");
names.add("Bob");
names.add("Charlie");
```

Result:

```text
Alice
Bob
Charlie
```

---

## Adding Duplicate

```java
names.add("Alice");
```

Nothing happens.

Result:

```text
Alice
Bob
Charlie
```

Uniqueness is still enforced.

---

## Removing

```java
names.remove("Bob");
```

Result:

```text
Alice
Charlie
```

---

## Checking Existence

```java
names.contains("Alice");
```

Result:

```text
true
```

---

# Iteration Behavior

This is the main difference.

Example:

```java
Set<String> names = new LinkedHashSet<>();

names.add("Carlos");
names.add("Ana");
names.add("Bruno");

for(String name : names){
    System.out.println(name);
}
```

Output:

```text
Carlos
Ana
Bruno
```

The order is guaranteed.

---

# LinkedHashSet Does NOT Sort

A common misunderstanding:

> "It keeps order, so it sorts."

Wrong.

It preserves:

```text
insertion order
```

Example:

```java
set.add("Zebra");
set.add("Apple");
set.add("Monkey");
```

Output:

```text
Zebra
Apple
Monkey
```

Not:

```text
Apple
Monkey
Zebra
```

For sorted data, use:

```java
TreeSet
```

---

# Time Complexity

Because it uses hashing:

| Operation | Complexity   |
| --------- | ------------ |
| add       | O(1) average |
| remove    | O(1) average |
| contains  | O(1) average |
| size      | O(1)         |

Similar to `HashSet`.

---

# Performance Comparison

## HashSet

Fastest.

Why?

It only manages hashing.

---

## LinkedHashSet

Slightly slower.

Why?

It must maintain additional links.

---

Example:

```text
HashSet

Object


LinkedHashSet

Object
 |
next
 |
previous
```

Extra management creates overhead.

---

# Memory Considerations

`LinkedHashSet` uses more memory than `HashSet`.

Why?

Each element needs additional links.

Conceptually:

HashSet:

```text
Object
```

LinkedHashSet:

```text
Previous reference
Object
Next reference
```

The extra memory pays for predictable ordering.

---

# HashSet vs LinkedHashSet

| Feature              | HashSet         | LinkedHashSet   |
| -------------------- | --------------- | --------------- |
| Duplicate prevention | Yes             | Yes             |
| Uses hashing         | Yes             | Yes             |
| Insertion order      | ❌               | ✅               |
| Sorted               | ❌               | ❌               |
| Performance          | Slightly faster | Slightly slower |
| Memory usage         | Lower           | Higher          |

---

# When Should You Use LinkedHashSet?

Use it when:

## 1. You need uniqueness

Example:

```text
Unique customers
Unique tags
Unique permissions
```

---

## 2. You need insertion order

Example:

A registration system:

```text
First registered
Second registered
Third registered
```

---

## 3. You want predictable output

Example:

Generating reports:

```text
Category A
Category B
Category C
```

---

# When Should You NOT Use LinkedHashSet?

Avoid it when:

## You don't care about order

Use:

```java
HashSet
```

because it uses less memory.

---

## You need sorted elements

Use:

```java
TreeSet
```

Example:

```text
A
B
C
D
```

---

## You need duplicates

Use:

```java
List
```

---

# Practical Example — Recently Used Tags

Imagine a blogging system.

Users add tags:

```text
Java
Spring
Database
Java
```

Requirements:

* No duplicate tags.
* Display tags in the order they were added.

Perfect:

```java
Set<String> tags = new LinkedHashSet<>();

tags.add("Java");
tags.add("Spring");
tags.add("Database");
tags.add("Java");
```

Result:

```text
Java
Spring
Database
```

The duplicate Java is ignored, but the order remains.

---

# Common Mistakes

## Mistake 1 — Thinking LinkedHashSet is sorted

Wrong:

```text
Insertion order ≠ Sorted order
```

---

## Mistake 2 — Using LinkedHashSet by default

It is tempting because it gives predictable output.

But if ordering is unnecessary:

```java
HashSet
```

is usually better.

---

## Mistake 3 — Expecting index access

This does not exist:

```java
set.get(0);
```

A Set has no indexes.

---

# Chapter Summary

In this chapter, you learned:

* `LinkedHashSet` maintains uniqueness like `HashSet`.
* It also preserves insertion order.
* Internally it combines hashing with linked ordering.
* It uses more memory than `HashSet`.
* It is slightly slower because it maintains additional structure.
* It is useful when both uniqueness and predictable iteration order matter.

The key idea:

> LinkedHashSet is the compromise between HashSet's speed and ordered output.

---

# ✔️ Next Step

In **Chapter 09 — TreeSet**, we will study the sorted `Set` implementation. You will learn how Java maintains elements in order, how trees work conceptually, how `Comparable` and `Comparator` connect with collections, and why `TreeSet` trades some performance for automatic sorting.
