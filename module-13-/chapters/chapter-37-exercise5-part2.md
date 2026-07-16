# Chapter 37 — Exercise 5: Contact Manager (Part 2)

In the previous chapter, we created the base Contact Manager using:

```java
Map<String, Contact>
```

with:

```java
HashMap
```

We implemented:

* Adding contacts.
* Searching by name.
* Updating phone numbers.

Now we will complete the system and compare the main `Map` implementations:

* `HashMap`
* `LinkedHashMap`
* `TreeMap`

---

# Current ContactService

Current:

```text
ContactService

+ addContact()
+ findByName()
+ updatePhone()
```

New:

```text
+ removeContact()
+ listContacts()
```

---

# Part 1 — Removing Contacts

Requirement:

Remove contact by name.

Example:

Before:

```text
John → 1111
Maria → 2222
Carlos → 3333
```

Remove:

```text
Maria
```

After:

```text
John → 1111
Carlos → 3333
```

---

# Implementation

```java
public void removeContact(String name){

    contacts.remove(name);

}
```

---

# How Does HashMap Find The Contact?

When we execute:

```java
contacts.remove("Maria");
```

HashMap uses:

1. `hashCode()`
2. `equals()`

to locate the key.

---

# Complexity

Average:

```text
O(1)
```

---

# Part 2 — Listing Contacts

A Map cannot be directly iterated:

Wrong:

```java
for(Contact contact : contacts)
```

Because a Map contains:

```text
Key + Value
```

---

We need Map views.

---

# Option 1 — values()

If we only need contacts:

```java
public void listContacts(){

    for(Contact contact : contacts.values()){

        System.out.println(contact);

    }

}
```

---

Output:

```text
Contact{name='John', phone='1111'}

Contact{name='Maria', phone='2222'}
```

---

# Option 2 — keySet()

If we need only names:

```java
for(String name : contacts.keySet()){

    System.out.println(name);

}
```

Output:

```text
John
Maria
```

---

# Option 3 — entrySet()

Most complete option.

It gives:

```text
Key + Value
```

Example:

```java
public void listContacts(){

    for(Map.Entry<String, Contact> entry :
            contacts.entrySet()){


        System.out.println(
            "Name: "
            + entry.getKey()
        );


        System.out.println(
            "Contact: "
            + entry.getValue()
        );

    }

}
```

---

Output:

```text
Name: John

Contact:
Contact{name='John', phone='1111'}
```

---

# Why entrySet() Is Important?

Consider:

```java
contacts.keySet()
```

You get:

```text
John
Maria
```

Then:

```java
contacts.get(name)
```

requires another lookup.

---

Using:

```java
entrySet()
```

you already have:

```text
key
+
value
```

---

# Part 3 — Comparing Map Implementations

Java provides:

```text
Map

 |
 +-- HashMap
 |
 +-- LinkedHashMap
 |
 +-- TreeMap
```

---

# HashMap

Current implementation:

```java
Map<String, Contact> contacts =
        new HashMap<>();
```

---

## Internal Structure

High-level:

```text
Hash Table
```

Uses:

* hashCode()
* equals()

---

## Ordering

No guaranteed order.

Example:

Insertion:

```text
John
Maria
Carlos
```

Possible output:

```text
Carlos
John
Maria
```

---

## Performance

Average:

| Operation | Complexity |
| --------- | ---------- |
| put()     | O(1)       |
| get()     | O(1)       |
| remove()  | O(1)       |

---

## When To Use

Use when:

* Fast lookup is priority.
* Order does not matter.

Example:

```text
User ID → User
Product ID → Product
```

---

# LinkedHashMap

Change:

```java
Map<String, Contact> contacts =
        new LinkedHashMap<>();
```

---

## Internal Structure

Conceptually:

```text
Hash table
+
Doubly linked list
```

---

Why?

It keeps track of insertion order.

---

Example:

Insert:

```text
John
Maria
Carlos
```

Output:

```text
John
Maria
Carlos
```

---

## Performance

Very similar to HashMap:

| Operation | Complexity |
| --------- | ---------- |
| put()     | O(1)       |
| get()     | O(1)       |
| remove()  | O(1)       |

---

## Extra Cost

Needs extra memory for links:

```text
Previous
Next
```

---

## When To Use

When you need:

* Fast lookup.
* Predictable iteration order.

Example:

```text
Recent searches
History
Configuration files
```

---

# TreeMap

Change:

```java
Map<String, Contact> contacts =
        new TreeMap<>();
```

---

## Internal Structure

Usually:

```text
Red-Black Tree
```

---

## Ordering

Keys are automatically sorted.

Example:

Insert:

```text
John
Carlos
Maria
```

Output:

```text
Carlos
John
Maria
```

---

## Performance

| Operation | Complexity |
| --------- | ---------- |
| put()     | O(log n)   |
| get()     | O(log n)   |
| remove()  | O(log n)   |

---

## Why Slower?

Because the tree must maintain sorting.

---

## When To Use

When you need:

* Sorted keys.
* Range operations.

Example:

```text
A-Z dictionary
Ranking system
Sorted reports
```

---

# Map Comparison Table

| Feature                   | HashMap    | LinkedHashMap | TreeMap  |
| ------------------------- | ---------- | ------------- | -------- |
| Key/value                 | Yes        | Yes           | Yes      |
| Fast lookup               | ⭐⭐⭐        | ⭐⭐⭐           | ⭐⭐       |
| Maintains insertion order | No         | Yes           | No       |
| Sorted keys               | No         | No            | Yes      |
| Internal structure        | Hash table | Hash + List   | Tree     |
| get()                     | O(1) avg   | O(1) avg      | O(log n) |

---

# Choosing For Contact Manager

Question:

## Do we only need fast search?

Example:

"Find John"

Use:

```java
HashMap
```

---

## Do we want contacts in registration order?

Example:

"Show contacts as added"

Use:

```java
LinkedHashMap
```

---

## Do we want alphabetical contacts?

Example:

"Show A-Z"

Use:

```java
TreeMap
```

---

# Improving Contact Manager

A professional choice:

```java
Map<String, Contact> contacts =
        new TreeMap<>();
```

because:

Contacts naturally benefit from:

```text
Alphabetical order
```

---

Now:

Adding:

```text
John
Carlos
Maria
```

Listing:

```text
Carlos
John
Maria
```

automatically.

No sorting needed.

---

# Important Design Lesson

The collection changes the behavior of the application.

Same interface:

```java
Map<String, Contact>
```

Different implementations:

```java
HashMap
LinkedHashMap
TreeMap
```

produce different results.

This is the power of programming to interfaces.

---

# Contact Manager Complete

Features:

```text
ContactService

+ addContact()
+ findByName()
+ updatePhone()
+ removeContact()
+ listContacts()
```

Uses:

```text
Map<String, Contact>
```

---

# Exercise Task

Implement:

1. `removeContact()`
2. `listContacts()` using:

   * values()
   * entrySet()

Then replace:

```java
HashMap
```

with:

```java
LinkedHashMap
```

and:

```java
TreeMap
```

Observe the difference.

---

# ✔️ Next Step

In **Chapter 38 — Exercise 6: Sorting Practice (Part 1)** we will start learning collection sorting:

* `Comparable`
* Natural ordering
* `Collections.sort()`
* Sorting custom objects

We will use `Product` objects and create different sorting strategies.
