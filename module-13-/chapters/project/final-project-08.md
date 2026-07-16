# Chapter 52 — Final Project: Integrating Collections Utility Methods

At this point, our Library Management System already uses:

✅ `Map`
✅ `List`
✅ `Queue`
✅ `Comparable`
✅ `Comparator`

Now we will improve our reports and operations using helper methods from:

```java
java.util.Collections
```

---

# What Is Collections?

Before continuing, remember:

There are two similar names:

## Collection

Interface:

```java
java.util.Collection
```

Represents groups of objects.

Examples:

```java
List
Set
Queue
```

---

## Collections

Utility class:

```java
java.util.Collections
```

Provides static helper methods.

Examples:

```java
Collections.sort()

Collections.reverse()

Collections.max()
```

---

# Collections Utility Methods

We will implement:

* `reverse()`
* `shuffle()`
* `max()`
* `min()`
* `frequency()`
* `unmodifiableList()`

---

# 1 — Collections.reverse()

## What is it?

Reverses the order of a list.

Example:

Before:

```text
Book A
Book B
Book C
```

After:

```text
Book C
Book B
Book A
```

---

## Why does it exist?

Because reversing manually is unnecessary.

Without:

```java
for(...)
```

swapping elements yourself.

---

Java provides:

```java
Collections.reverse(list);
```

---

# Example

```java
List<Book> books =
        new ArrayList<>();


Collections.reverse(books);
```

---

# Important Detail

`reverse()` modifies the original list.

Before:

```text
Original:

A
B
C
```

After:

```text
Original:

C
B
A
```

---

If you want to preserve the original:

```java
List<Book> copy =
        new ArrayList<>(books);


Collections.reverse(copy);
```

---

# 2 — Collections.shuffle()

## What is it?

Randomizes list order.

Example:

Before:

```text
Book A
Book B
Book C
```

After:

```text
Book C
Book A
Book B
```

---

## Why use it?

Possible library examples:

* Random recommendations.
* Featured books.
* Random selections.

---

Usage:

```java
Collections.shuffle(books);
```

---

# Complexity

Shuffle:

```text
O(n)
```

because every element is visited.

---

# 3 — Collections.max()

## What does it do?

Returns the greatest element.

But Java needs to know:

> Greater according to what rule?

---

For this:

```java
Collections.max(list);
```

The objects need:

```java
Comparable
```

---

Our Book already has:

```java
Comparable<Book>
```

using:

```text
title
```

---

Example:

```java
Book max =
    Collections.max(books);
```

---

Result:

The book with the last title alphabetically.

Example:

```text
Algorithms

Clean Code

Java
```

Returns:

```text
Java
```

---

# Using Comparator With max()

Suppose we want:

> The book with the longest title.

Natural ordering does not help.

---

Create comparator:

```java
Comparator<Book> titleLength =
    (b1, b2) ->
        Integer.compare(
            b1.getTitle().length(),
            b2.getTitle().length()
        );
```

---

Use:

```java
Book longest =
    Collections.max(
        books,
        titleLength
    );
```

---

# 4 — Collections.min()

Works exactly like `max()`.

Difference:

Returns smallest element.

---

Example:

```java
Book first =
    Collections.min(books);
```

---

Using natural order:

```text
Algorithms
```

would be returned.

---

# 5 — Collections.frequency()

## What is it?

Counts occurrences of an element.

Example:

```text
Java
Java
Python
Java
```

Frequency of:

```text
Java
```

is:

```text
3
```

---

Usage:

```java
int amount =
    Collections.frequency(
        words,
        "Java"
    );
```

---

# Library Example

Imagine:

Borrow history:

```text
Clean Code
Java
Clean Code
Algorithms
Clean Code
```

---

Count:

```java
Collections.frequency(
    borrowedBooks,
    cleanCode
);
```

Result:

```text
3
```

---

# Important Requirement

Frequency uses:

```java
equals()
```

to compare objects.

---

Example:

```java
Book book1 =
new Book(
1,
"Java",
"Author",
"Programming"
);


Book book2 =
new Book(
1,
"Java",
"Author",
"Programming"
);
```

---

Without:

```java
equals()
```

Java sees:

```text
different objects
```

---

With:

```java
equals()
```

they are considered:

```text
same book
```

---

This is another reason why:

```text
equals()
hashCode()
```

are important.

---

# 6 — Collections.unmodifiableList()

Now we discuss immutability.

---

Imagine:

ReportService returns:

```java
public List<Book> getBooks()
```

---

External code can do:

```java
books.clear();
```

---

Problem:

The internal collection is destroyed.

---

Solution:

```java
Collections.unmodifiableList(list);
```

---

Example:

```java
public List<BorrowRecord> getHistory(){

    return Collections.unmodifiableList(
        history
    );

}
```

---

Now:

Allowed:

```java
history.get(0);
```

---

Not allowed:

```java
history.clear();
```

---

Result:

```text
UnsupportedOperationException
```

---

# Why Is This Useful?

Because services should control their data.

Example:

LibraryService owns:

```java
List<BorrowRecord>
```

---

Other classes should:

Read:

✅

Modify:

❌

---

# Updating ReportService

Now we can add:

```java
public Book getFirstBook(
        List<Book> books){

    return Collections.min(books);

}
```

---

```java
public Book getLastBook(
        List<Book> books){

    return Collections.max(books);

}
```

---

```java
public void reverseBooks(
        List<Book> books){

    Collections.reverse(books);

}
```

---

# Final Project Collection Usage

Our project now demonstrates:

---

# List

Used for:

```text
Borrow history
```

Operations:

* Add records.
* Maintain order.
* Sort reports.

---

# Map

Used for:

```text
Books

Users
```

Operations:

* Fast lookup.
* Unique identifiers.

---

# Queue

Used for:

```text
Waiting users
```

Operations:

* FIFO processing.

---

# Set

Still missing.

We need to integrate:

```text
Unique categories
```

or:

```text
Unique registrations
```

---

# Adding Set To Project

Requirement:

Prevent duplicate categories.

Example:

```text
Programming

Fantasy

Programming
```

Should become:

```text
Programming

Fantasy
```

---

Create:

```java
private Set<String> categories;
```

Implementation:

```java
categories =
    new HashSet<>();
```

---

Adding:

```java
categories.add(
    book.getCategory()
);
```

---

Result:

```text
No duplicates.
```

---

# Complete Collection Map

Our final architecture:

```text
Library Management System


Map<Integer, Book>

        |
        |
      Books


Map<Integer, User>

        |
        |
      Users


List<BorrowRecord>

        |
        |
 Borrow history


Queue<User>

        |
        |
 Waiting list


Set<String>

        |
        |
 Categories
```

---

# Exercise Task

Improve your project:

Implement:

## ReportService

Methods:

```text
getMaxBook()

getMinBook()

reverseBooks()

shuffleBooks()
```

---

## LibraryService

Change:

```java
getHistory()
```

to return:

```java
Collections.unmodifiableList()
```

---

## Add Categories

Create:

```java
Set<String>
```

and store unique categories.

---

# ✔️ Next Step

In **Chapter 53 — Final Project: Complete Integration and Review** we will:

* Connect all services.
* Create the final console menu.
* Review every collection used.
* Analyze design decisions.
* Prepare the final module completion.
