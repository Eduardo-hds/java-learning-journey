# Chapter 20 — Iterators

Until now, we have learned how to store and manipulate data using:

* `List`
* `Set`
* `Queue`
* `Map`

But eventually we need to **traverse** these collections.

Examples:

* Display all users.
* Search elements.
* Remove invalid objects.
* Process stored data.

The first approach many beginners use is:

```java
for(int i = 0; i < list.size(); i++){

}
```

This works for lists, but it does not work for all collections.

A `Set`, for example, does not have indexes.

Java solves this problem with:

```java
Iterator
```

---

# Learning Objectives

By the end of this chapter, you should understand:

* What an Iterator is.
* Why Iterators exist.
* How iteration works internally.
* The `Iterator` interface.
* Safe removal during iteration.
* Difference between Iterator and enhanced for-loop.
* `ListIterator`.

---

# What is an Iterator?

An `Iterator` is an object responsible for moving through elements of a collection.

Conceptually:

```text id="y93m6h"
Collection

[A][B][C][D]

        |
        v

    Iterator
```

The iterator remembers:

> "Where am I currently in this collection?"

---

# Why Does Iterator Exist?

Different collections have different structures.

---

## ArrayList

Internally:

```text id="e7fz5m"
[0][1][2][3]
```

You can use indexes:

```java id="4rq5e4"
list.get(2);
```

---

## HashSet

Internally:

```text id="9h1l3a"
Bucket
  |
 Element
```

There is no:

```java id="b7s9av"
set.get(2);
```

---

The collection should not expose its internal structure.

Instead:

```text id="1tq8g7"
Collection
     |
 Iterator
     |
 Element by element
```

---

# Iterator Interface

The interface:

```java id="y41u9h"
java.util.Iterator
```

Main methods:

| Method    | Purpose                          |
| --------- | -------------------------------- |
| hasNext() | Checks if another element exists |
| next()    | Returns next element             |
| remove()  | Removes current element          |

---

# Creating an Iterator

Example:

```java id="q4d7oz"
List<String> names =
        new ArrayList<>();

names.add("Alice");
names.add("Bob");
names.add("Carlos");


Iterator<String> iterator =
        names.iterator();
```

---

# Checking Elements

Use:

```java id="z0n7my"
hasNext()
```

Example:

```java id="9u6m5y"
while(iterator.hasNext()){

}
```

Meaning:

> "Is there another element?"

---

# Getting Elements

Use:

```java id="2f5f8r"
next()
```

Example:

```java id="9p3d9y"
String name = iterator.next();
```

Returns:

```text id="q3m6t1"
Alice
```

---

# Complete Example

```java id="h9d4qs"
List<String> names =
        new ArrayList<>();

names.add("Alice");
names.add("Bob");
names.add("Carlos");


Iterator<String> iterator =
        names.iterator();


while(iterator.hasNext()){

    String name = iterator.next();

    System.out.println(name);

}
```

Output:

```text id="z5v6x2"
Alice
Bob
Carlos
```

---

# How Iterator Works Internally

Conceptually:

Initial:

```text id="e4c8uz"
Iterator

|
v

[A][B][C]
 ^
```

After:

```java id="18m5k8"
next()
```

Moves forward:

```text id="0xjzqf"
[A][B][C]
    ^
```

Again:

```text id="l2k7yb"
[A][B][C]
        ^
```

---

# Iterator Does Not Copy the Collection

Important:

The iterator does not create:

```text id="m8oj6x"
New Array
```

It works over the existing collection.

Advantages:

* Less memory.
* Efficient traversal.

---

# Enhanced For Loop and Iterator

This:

```java id="l9x2yq"
for(String name : names){

    System.out.println(name);

}
```

looks different.

But internally Java uses:

```java id="1v8r7x"
Iterator
```

Conceptually:

```java
Iterator<String> iterator =
        names.iterator();

while(iterator.hasNext()){

    String name = iterator.next();

}
```

---

# Why Does Enhanced For Exist?

Because it is cleaner.

Instead of:

```java id="c1m8uj"
Iterator<String> iterator =
        list.iterator();

while(iterator.hasNext()){

}
```

you write:

```java id="8bq5qk"
for(String item : list){

}
```

---

# The Problem: Modifying Collections While Iterating

A very common mistake.

Example:

```java id="9x7qkt"
List<Integer> numbers =
        new ArrayList<>();

numbers.add(10);
numbers.add(20);
numbers.add(30);


for(Integer number : numbers){

    if(number == 20){

        numbers.remove(number);

    }

}
```

This can cause:

```text id="4z2b4n"
ConcurrentModificationException
```

---

# Why Does This Happen?

The collection detects:

> "Someone changed the structure while I was iterating."

The iterator becomes invalid.

---

# The Correct Way

Use:

```java id="1kqv1w"
Iterator.remove()
```

Example:

```java id="t2q5s9"
Iterator<Integer> iterator =
        numbers.iterator();


while(iterator.hasNext()){

    Integer number =
            iterator.next();


    if(number == 20){

        iterator.remove();

    }

}
```

---

# Why Iterator.remove() Works

Because the iterator controls the modification.

Instead of:

```text id="z5u1cf"
Collection changed externally
```

we have:

```text id="9p7n6u"
Iterator requested removal
```

The iterator updates its internal state.

---

# Iterator vs For Loop

Comparison:

| Feature          | For loop | Iterator |
| ---------------- | -------- | -------- |
| Index access     | Yes      | No       |
| Works with Set   | No       | Yes      |
| Safe removal     | No       | Yes      |
| Simple traversal | Yes      | Yes      |

---

# ListIterator

`Iterator` only moves forward.

Example:

```text id="mlz0ik"
A → B → C
```

It can do:

```text id="xv1y0a"
A
B
C
```

But not backwards.

For lists, Java provides:

```java id="5u5v4j"
ListIterator
```

---

# What is ListIterator?

A more powerful iterator specifically for:

```text id="1w1w8a"
List
```

It supports:

* Forward movement.
* Backward movement.
* Adding elements.
* Updating elements.

---

# Creating ListIterator

Example:

```java id="2z0x3v"
List<String> names =
        new ArrayList<>();

ListIterator<String> iterator =
        names.listIterator();
```

---

# Forward Navigation

```java id="5e0h5r"
iterator.hasNext();

iterator.next();
```

---

# Backward Navigation

```java id="4l9v6h"
iterator.hasPrevious();

iterator.previous();
```

---

# Example

List:

```text id="s7p6q3"
A
B
C
```

Move forward:

```text id="s8c9m4"
A
B
C
```

Move backward:

```text id="o9j2fj"
C
B
A
```

---

# Updating Elements

ListIterator:

```java id="f7y2y5"
iterator.set("New Value");
```

Example:

Before:

```text id="j1r7tq"
Java
```

After:

```text id="w0w8lz"
Spring
```

---

# Adding Elements

```java id="j0h7c8"
iterator.add("Python");
```

Adds during iteration.

---

# Iterator with Different Collections

---

## ArrayList

Iterator:

```text id="z3b8ny"
Index movement
```

---

## HashSet

Iterator:

```text id="aq4h8u"
Bucket traversal
```

---

## HashMap

Use:

```java id="oq2p6c"
entrySet().iterator()
```

Example:

```java id="v3m4w6"
Iterator<Map.Entry<Integer,String>> iterator =
        map.entrySet().iterator();
```

---

# Time Complexity

Iterator traversal:

```text id="9u6m5n"
O(n)
```

Because every element must be visited.

---

Removal complexity depends on collection.

Example:

ArrayList:

Removing during iteration:

```text id="xq7b4s"
O(n)
```

because elements shift.

---

# Advantages of Iterator

## 1. Works with Any Collection

Unified traversal.

---

## 2. Safe Removal

Avoids modification errors.

---

## 3. Hides Internal Structure

The collection decides traversal.

---

# Disadvantages of Iterator

## 1. More Verbose

Compared with:

```java
for(String s : list)
```

---

## 2. Forward Only

Unless using:

```java
ListIterator
```

---

# When Should You Use Iterator?

Use when:

✅ Removing elements while traversing.

Example:

```java
iterator.remove();
```

---

✅ Working with unknown collection types.

---

✅ Need manual control.

---

# When Should You NOT Use Iterator?

Avoid when:

❌ Simple reading only.

Use:

```java
for-each
```

---

❌ Need index access.

Use:

```java
for(int i = 0; i < list.size(); i++)
```

---

# Common Mistakes

## Mistake 1 — Calling next() without hasNext()

Wrong:

```java id="0t4p4w"
iterator.next();
```

when empty.

Result:

```text id="5x2f5m"
NoSuchElementException
```

---

## Mistake 2 — Removing directly

Wrong:

```java
list.remove(item);
```

during iteration.

---

## Mistake 3 — Using ListIterator on non-List collections

`ListIterator` works only with:

```text id="0m2b6w"
List
```

---

# Chapter Summary

You learned:

* Iterator provides a standard way to traverse collections.
* It hides internal implementation details.
* `hasNext()` checks availability.
* `next()` moves forward.
* `remove()` safely removes elements.
* `ListIterator` adds backward movement and modification features.
* Enhanced for-loop uses Iterator internally.

The key idea:

> Iterator separates the way we traverse data from the way the collection stores data.

---

# ✔️ Next Step

In **Chapter 21 — Sorting Collections: Comparable**, we will start learning how Java decides the ordering of objects. You will learn how objects define their natural order and how this connects with sorting collections like `List`, `TreeSet`, and `TreeMap`.
