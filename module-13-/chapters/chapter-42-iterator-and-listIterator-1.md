# Chapter 42 — Iterator and ListIterator (Part 1)

Until now, we have used loops to access collection elements:

```java id="m8x2q5"
for(Product product : products){

    System.out.println(product);

}
```

This works for displaying data.

But collections have a deeper mechanism for traversal:

```java id="q5m8x3"
Iterator
```

---

# Why Do Iterators Exist?

A collection internally manages its elements.

Different collections have different structures:

---

## ArrayList

Internally:

```text id="v7m3q9"
[0][1][2][3]
```

---

## LinkedList

Internally:

```text id="x8m2q5"
Node → Node → Node
```

---

## HashSet

Internally:

```text id="n4m8q1"
Hash table
```

---

A common way to navigate all of them would be difficult.

Java created:

```text id="p5m9x2"
Iterator
```

as a common traversal mechanism.

---

# Iterable Interface

Before Iterator, we need to understand:

```java id="r8m3x5"
Iterable
```

---

Hierarchy:

```text id="q7m2x9"
Iterable

   |

Collection

   |

List / Set / Queue
```

---

Meaning:

If a class implements:

```java id="m4x8q2"
Iterable<T>
```

it can provide:

```java id="z6m3p8"
Iterator
```

---

# The Iterator Interface

Package:

```java id="w5q9m2"
java.util.Iterator
```

---

Main methods:

```java id="x3m8q5"
hasNext()

next()

remove()
```

---

# hasNext()

Checks if there is another element.

Example:

```java id="v8m2q6"
iterator.hasNext()
```

Returns:

```text id="k5m9x3"
true
false
```

---

# next()

Returns the next element.

Example:

```java id="p4m8q1"
Product product =
        iterator.next();
```

---

# remove()

Removes the current element safely.

Example:

```java id="m7q3x9"
iterator.remove();
```

---

# Basic Iterator Example

Create:

```java id="h8m3x5"
List<String> names =
        new ArrayList<>();


names.add("John");
names.add("Maria");
names.add("Carlos");
```

---

Create iterator:

```java id="x5m9q2"
Iterator<String> iterator =
        names.iterator();
```

---

Now:

```java id="r6m3q8"
while(iterator.hasNext()){

    String name =
            iterator.next();


    System.out.println(name);

}
```

---

Output:

```text id="z7m2x4"
John
Maria
Carlos
```

---

# What Happens Internally?

Conceptually:

Before:

```text id="q8m3x5"
Iterator

position:
before first element
```

---

First:

```java id="n5m8q2"
next()
```

moves:

```text id="p7x3m9"
John
 ^
```

---

Next:

```text id="v4m8q1"
next()
```

moves:

```text id="w6m2x8"
Maria
 ^
```

---

The iterator remembers:

> Where I currently am.

---

# Why Not Just Use For Loop?

For reading:

```java id="m3x8q5"
for(String name : names)
```

is simpler.

But modification creates problems.

---

# The Common Problem

Imagine:

```java id="z5m2q9"
List<Integer> numbers =
        new ArrayList<>();

numbers.add(1);
numbers.add(2);
numbers.add(3);
numbers.add(4);
```

---

Goal:

Remove even numbers.

---

Attempt:

```java id="x8m3q5"
for(Integer number : numbers){

    if(number % 2 == 0){

        numbers.remove(number);

    }

}
```

---

Problem:

```text id="q7m3x9"
ConcurrentModificationException
```

---

# Why Does This Happen?

The loop is using an internal iterator.

You are modifying the collection directly:

```text id="m5q8x2"
Iterator expects:

1 → 2 → 3 → 4


Collection changes:

1 → 3 → 4
```

---

The iterator detects:

> "The collection changed unexpectedly."

---

# Correct Solution

Use Iterator's own remove method.

---

Example:

```java id="v8m2q4"
Iterator<Integer> iterator =
        numbers.iterator();


while(iterator.hasNext()){


    Integer number =
            iterator.next();


    if(number % 2 == 0){

        iterator.remove();

    }

}
```

---

Result:

Before:

```text id="p5m9x3"
1
2
3
4
```

After:

```text id="r7m2q8"
1
3
```

---

# Why Iterator.remove() Works

Because:

The iterator knows:

* Current position.
* Collection structure.
* Modification state.

It updates both:

```text id="x4m8q2"
Collection

and

Iterator
```

---

# Iterator With Set

Important:

Sets do not have indexes.

This is impossible:

```java id="k7m3x5"
set.get(0)
```

---

But:

```java id="w5q9m2"
Iterator
```

works.

Example:

```java id="m8x3q6"
Set<String> names =
        new HashSet<>();


Iterator<String> iterator =
        names.iterator();
```

---

Same process.

---

# Iterator With Map

Map does not implement Collection directly.

So:

```java id="q6m3x8"
map.iterator()
```

does not exist.

---

Use:

```java id="p4m9x2"
entrySet()
```

Example:

```java id="z8m3q5"
Iterator<Map.Entry<String,Contact>>
iterator =
        contacts.entrySet()
                .iterator();
```

---

Then:

```java id="r5x2m9"
while(iterator.hasNext()){

    Map.Entry<String,Contact> entry =
            iterator.next();

}
```

---

# When To Use Iterator

Use when:

* Removing elements during traversal.
* Working with Set.
* Need explicit traversal control.
* Need compatibility with older Java code.

---

# When NOT To Use

For simple reading:

Prefer:

```java id="x5m8q3"
for-each loop
```

because it is cleaner.

---

# Iterator vs For-Each

| Feature        | For-each  | Iterator |
| -------------- | --------- | -------- |
| Read elements  | Excellent | Good     |
| Remove safely  | No        | Yes      |
| Works with Set | Yes       | Yes      |
| More control   | No        | Yes      |
| Simpler syntax | Yes       | No       |

---

# Exercise Task

Create:

```java id="h7m3x9"
List<Integer> numbers
```

Add:

```text id="m5q8x2"
1
2
3
4
5
6
```

Remove all even numbers using:

1. Normal for loop (observe the problem).
2. Iterator.remove().

Expected result:

```text id="v8m2q5"
1
3
5
```

---

# ✔️ Next Step

In **Chapter 43 — Iterator and ListIterator (Part 2)** we will learn:

* `ListIterator`.
* Forward and backward traversal.
* Adding and replacing elements during iteration.
* When `ListIterator` should be preferred over `Iterator`.
