# Chapter 56 — Module Review: Map, Queue, Iterators and Performance Comparison

In the previous chapter, we reviewed:

* Collections hierarchy.
* Arrays vs Collections.
* List.
* Set.

Now we complete the Collections Framework review with:

* Map.
* Queue.
* Deque.
* Iterators.
* Complete decision guide.

---

# Map Overview

Unlike:

```java
Collection
```

a Map does not store individual elements.

It stores:

```text id="x8m3q5"
Key → Value
```

---

Example:

```text id="m4q8x2"

101 → Clean Code

102 → Effective Java

103 → Algorithms
```

---

# Why Map Exists

Imagine searching books.

Without Map:

```java id="q7m3x9"
List<Book>
```

Search:

```text id="p5m8x2"
Check book 1

Check book 2

Check book 3

...
```

Complexity:

```text id="z8m3q5"
O(n)
```

---

With Map:

```java id="x7m3q9"
books.get(101);
```

Direct lookup.

---

# Map Characteristics

A Map has:

## Keys

Identify the element.

Example:

```text id="m6q2x8"
Book ID
```

---

## Values

The stored object.

Example:

```text id="v4m9q2"
Book
```

---

Keys:

* Must be unique.
* One key maps to one value.

---

# HashMap

The most commonly used Map.

Internal structure:

```text id="p5m8x2"
Hash Table
```

---

Conceptually:

```text id="x8m3q5"

hash(key)

    ↓

bucket

    ↓

entry

    ↓

value

```

---

Example:

```java id="q7m3x9"
map.put(
    101,
    book
);
```

---

Java calculates:

```text id="m4x8q2"
101.hashCode()
```

---

Then finds:

```text id="z7m3q9"
storage location
```

---

# HashMap and equals/hashCode

HashMap depends on:

```java id="p5m8x2"
hashCode()

equals()
```

---

Example:

```java id="x7m3q9"
map.get(key);
```

Process:

1. Calculate hash.
2. Find bucket.
3. Compare keys using equals.

---

This is why keys must correctly implement:

```java id="m6q2x8"
equals()

hashCode()
```

---

# HashMap Performance

| Operation | Complexity   |
| --------- | ------------ |
| put       | O(1) average |
| get       | O(1) average |
| remove    | O(1) average |
| search    | O(1) average |

---

# When To Use HashMap

Use when:

✅ Need fast lookup.

Examples:

```text id="v4m9q2"
User by ID

Product by code

Configuration values

Cache
```

---

# When NOT To Use HashMap

Avoid when:

❌ You need sorted keys.

Use:

```java id="z8m3q5"
TreeMap
```

---

❌ You need insertion order.

Use:

```java id="x7m3q9"
LinkedHashMap
```

---

# LinkedHashMap

A HashMap with ordering.

Maintains:

```text id="m4x8q2"
Insertion order
```

---

Example:

Insert:

```text id="p5m8x2"
3

1

2
```

---

Iteration:

```text id="z7m3q9"
3

1

2
```

---

Useful for:

* Recent items.
* Ordered configurations.
* Simple caches.

---

# TreeMap

Stores keys sorted.

Internal structure:

```text id="x8m3q5"
Balanced Tree
```

---

Example:

Insert:

```text id="q7m3x9"
30

10

20
```

---

Result:

```text id="m4q8x2"
10

20

30
```

---

Performance:

| Operation | Complexity |
| --------- | ---------- |
| put       | O(log n)   |
| get       | O(log n)   |
| remove    | O(log n)   |

---

# HashMap vs LinkedHashMap vs TreeMap

| Feature   | HashMap    | LinkedHashMap      | TreeMap  |
| --------- | ---------- | ------------------ | -------- |
| Speed     | Fastest    | Slightly slower    | Slower   |
| Order     | None       | Insertion          | Sorted   |
| Structure | Hash table | Hash + linked list | Tree     |
| Lookup    | O(1)       | O(1)               | O(log n) |

---

# Queue

A Queue represents:

> A structure where elements are processed in order.

Usually:

```text id="p5m8x2"
FIFO
```

---

FIFO:

First In:

```text id="x7m3q9"
Maria
```

First Out:

```text id="m4q8x2"
Maria
```

---

Example:

```text id="z7m3q9"

Waiting line:

Maria

John

Carlos

```

---

# Queue Interface

Common methods:

| Method  | Purpose      |
| ------- | ------------ |
| offer() | Add          |
| poll()  | Remove first |
| peek()  | View first   |

---

Example:

```java id="x8m3q5"
queue.offer(user);

User u =
    queue.poll();
```

---

# PriorityQueue

Important difference:

Not a normal FIFO queue.

---

It processes based on priority.

Example:

Emergency room:

```text id="q7m3x9"

Critical

Normal

Low

```

---

The first inserted element is not necessarily the first removed.

---

Internal structure:

```text id="m4q8x2"
Heap
```

---

Performance:

| Operation | Complexity |
| --------- | ---------- |
| add       | O(log n)   |
| remove    | O(log n)   |
| peek      | O(1)       |

---

# Deque

Deque means:

```text id="z7m3q9"
Double Ended Queue
```

---

Allows operations:

Beginning:

```text id="x8m3q5"
addFirst()

removeFirst()
```

---

End:

```text id="q7m3x9"
addLast()

removeLast()
```

---

Implementation:

```java id="m4q8x2"
ArrayDeque
```

---

# Queue vs Stack

A Stack:

```text id="p5m8x2"
LIFO
```

Last In:

```text id="x7m3q9"
A

B

C
```

Remove:

```text id="m4q8x2"
C
```

---

Deque can behave like:

Queue:

```text id="z7m3q9"
FIFO
```

or:

Stack:

```text id="x8m3q5"
LIFO
```

---

# Iterators

Collections need a way to traverse elements.

That is:

```java id="q7m3x9"
Iterator
```

---

Example:

```java id="m4q8x2"
Iterator<Book> iterator =
        books.iterator();
```

---

Methods:

```java id="z7m3q9"
hasNext()

next()

remove()
```

---

# Why Iterator Exists?

Because collections have different internal structures.

Example:

ArrayList:

```text id="x8m3q5"
indexes
```

---

HashSet:

```text id="q7m3x9"
hash buckets
```

---

The user should not care.

Iterator hides the implementation.

---

# Removing During Iteration

Problem:

Wrong:

```java id="m4q8x2"
for(Book book : books){

    books.remove(book);

}
```

---

Can cause:

```text id="z7m3q9"
ConcurrentModificationException
```

---

Correct:

```java id="x8m3q5"
Iterator<Book> iterator =
        books.iterator();


while(iterator.hasNext()){

    Book book =
        iterator.next();


    if(condition){

        iterator.remove();

    }

}
```

---

# ListIterator

Special iterator for Lists.

Allows:

* Forward movement.
* Backward movement.
* Adding.
* Replacing.

---

Example:

```java id="q7m3x9"
ListIterator<Book> iterator =
        books.listIterator();
```

---

Useful for:

Complex List modifications.

---

# Complete Collection Decision Guide

## Need indexed access?

Use:

```text id="m4q8x2"
ArrayList
```

---

## Need unique values?

Use:

```text id="z7m3q9"
HashSet
```

---

## Need unique + insertion order?

Use:

```text id="x8m3q5"
LinkedHashSet
```

---

## Need unique + sorted?

Use:

```text id="q7m3x9"
TreeSet
```

---

## Need lookup by key?

Use:

```text id="m4q8x2"
HashMap
```

---

## Need key order?

Insertion:

```text id="z7m3q9"
LinkedHashMap
```

Sorted:

```text id="x8m3q5"
TreeMap
```

---

## Need FIFO processing?

Use:

```text id="q7m3x9"
Queue
```

---

## Need both ends?

Use:

```text id="m4q8x2"
Deque
```

---

# Final Performance Summary

| Collection | Access | Search   | Insert    |
| ---------- | ------ | -------- | --------- |
| ArrayList  | O(1)   | O(n)     | O(1) end  |
| LinkedList | O(n)   | O(n)     | O(1) ends |
| HashSet    | -      | O(1)     | O(1)      |
| TreeSet    | -      | O(log n) | O(log n)  |
| HashMap    | -      | O(1)     | O(1)      |
| TreeMap    | -      | O(log n) | O(log n)  |
| Queue      | -      | -        | O(1)      |

---

# Final Module Knowledge Check

Before completing Module 13, you should be able to answer:

### 1.

Why is ArrayList usually preferred over LinkedList?

### 2.

Why does HashMap require equals() and hashCode()?

### 3.

When would TreeMap be preferred over HashMap?

### 4.

Why does Set not allow duplicates?

### 5.

Why use Queue instead of List for waiting systems?

### 6.

What is the difference between Comparable and Comparator?

---

# ✔️ Next Step

In **Chapter 57 — Module 13 Final Assessment and Completion Report Preparation** we will:

* Review all module objectives.
* Evaluate your Collections Framework understanding.
* Review the final project.
* Generate the standardized Module Completion Report for the Bootcamp Central Control chat.
