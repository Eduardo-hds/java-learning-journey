# Chapter 51 — Final Project: Sorting and Reports

Our Library Management System currently supports:

✅ Books storage
✅ Users storage
✅ Borrowing
✅ Returning
✅ Borrow history
✅ Waiting queues

Now we need another important feature:

> Generate organized reports.

A library does not only store data.

It needs to present information in useful ways.

Examples:

* Books alphabetically.
* Books by author.
* Books by category.
* Users by name.

This is where we apply:

* `Comparable`
* `Comparator`
* `Collections.sort()`
* `List.sort()`

---

# Why Sorting Exists in Collections

A collection stores objects.

Example:

```java id="x7m3q9"
List<Book> books;
```

Current order:

```text id="m4q8x2"
Algorithms

Clean Code

Java

Design Patterns
```

Maybe we need:

```text id="z5m8q2"
Alphabetical order
```

---

The collection does not automatically know:

> What does "ordered" mean for a Book?

Java needs a rule.

---

# Two Ways To Define Ordering

Java provides:

## Comparable

Object defines:

> Its natural order.

---

## Comparator

External class defines:

> Alternative sorting rules.

---

# Comparable

Interface:

```java id="q7m3x9"
java.lang.Comparable<T>
```

---

Method:

```java id="m5q8x2"
int compareTo(T object)
```

---

Meaning:

Compare:

```text id="v8m3q5"
this object

against

another object
```

---

# Example: Book Natural Order

Question:

What should be the default order of books?

Possible:

* ID.
* Title.
* Author.

---

Usually:

```text id="p4m8x1"
Title
```

is a good natural order.

---

So:

```java id="x8m2q5"
Book implements Comparable<Book>
```

---

# Updating Book Class

Change:

```java
public class Book
```

to:

```java id="r7m3x9"
public class Book
        implements Comparable<Book>
```

---

Now add:

```java id="m6q2x8"
@Override
public int compareTo(Book other){

    return this.title.compareTo(
            other.title
    );

}
```

---

# Understanding compareTo()

Example:

```text id="v4m9q2"
Book A

title:
Algorithms


Book B

title:
Java
```

---

Comparison:

```java
"Algorithms".compareTo("Java")
```

returns:

negative number.

Meaning:

```text id="z8m3q5"
Algorithms comes before Java
```

---

# Sorting With Comparable

Example:

```java id="p5m8q2"
List<Book> books =
        new ArrayList<>();
```

---

Sort:

```java id="x7m3q9"
Collections.sort(books);
```

---

Result:

Before:

```text id="m4x8q2"
Java
Algorithms
Clean Code
```

After:

```text id="r5m8x2"
Algorithms
Clean Code
Java
```

---

# List.sort()

Modern Java alternative:

```java id="q7m3x9"
books.sort(null);
```

---

`null` means:

Use natural ordering.

Same idea as:

```java id="z6m3q8"
Collections.sort()
```

---

# Why Not Always Use Comparable?

Because a class can have only one natural order.

Example:

Book:

Natural:

```text id="x5m8q2"
title
```

But reports need:

```text id="p7m3x9"
author
```

or:

```text id="m4q8x1"
category
```

---

For these cases:

Use:

```text id="v8m3q5"
Comparator
```

---

# Comparator

Interface:

```java id="x7m3q9"
java.util.Comparator<T>
```

---

Purpose:

Create external sorting rules.

---

Example:

```text id="m5q8x2"

Sort books by price

Sort products by quantity

Sort users by name

```

---

# Creating Book Comparators

Create package:

```text id="z8m3q5"
util/
```

---

File:

```text id="p4m8x1"
BookTitleComparator.java
```

---

Example:

```java id="r7m3x9"
package util;

import model.Book;

import java.util.Comparator;


public class BookTitleComparator
        implements Comparator<Book> {


    @Override
    public int compare(
            Book b1,
            Book b2){

        return b1.getTitle()
                .compareTo(
                    b2.getTitle()
                );

    }

}
```

---

This is similar to Comparable.

The difference:

The rule is outside the object.

---

# Sorting By Author

Create:

```text id="m6q2x8"
BookAuthorComparator.java
```

---

Logic:

```java
return b1.getAuthor()
        .compareTo(
            b2.getAuthor()
        );
```

---

---

# Using Comparator

Example:

```java id="v4m9q2"
books.sort(
    new BookAuthorComparator()
);
```

---

Result:

```text id="z7m3x9"
Robert Martin
Joshua Bloch
Martin Fowler
```

---

# Comparable vs Comparator

| Feature         | Comparable    | Comparator     |
| --------------- | ------------- | -------------- |
| Location        | Inside class  | Outside class  |
| Methods         | compareTo()   | compare()      |
| Number of rules | One           | Many           |
| Used for        | Default order | Custom reports |

---

# ReportService

Now create:

```text id="x8m2q5"
src/service/ReportService.java
```

---

Responsibility:

```text id="p5m8q2"

Generate reports

Sort data

Display information
```

---

Structure:

```java id="q7m3x9"
package service;

public class ReportService {


}
```

---

# Report Example

Method:

```java id="m4x8q2"
public void printBooksByTitle(
        List<Book> books){

}
```

---

Copy list first:

```java id="z6m3q8"
List<Book> copy =
        new ArrayList<>(books);
```

---

Why?

Because sorting changes the list.

We may not want:

```text id="v8m3q5"
original data modified
```

---

Sort:

```java id="x7m3q9"
Collections.sort(copy);
```

---

Display:

```java
for(Book book : copy){

    System.out.println(book);

}
```

---

# Why Copy Before Sorting?

Imagine:

Borrow history:

```text id="m5q8x2"
Oldest
Newest
```

---

A report sorts it:

```text id="p4m8x1"
Newest
Oldest
```

---

Now history order changed.

Bad.

---

Create a copy:

```text id="r7m3x9"
Original

Oldest → Newest


Copy

Newest → Oldest
```

---

# Complexity

Sorting:

```text id="q8m3x5"
O(n log n)
```

---

Because Java uses optimized sorting algorithms internally.

---

# Applying To Library Project

Now reports can do:

---

## Books alphabetically

Uses:

```text id="x5m8q2"
Comparable
```

---

## Books by author

Uses:

```text id="m4q8x1"
Comparator
```

---

## Books by category

Uses:

```text id="z7m3q9"
Comparator
```

---

# Exercise Task

Implement:

---

## 1 — Comparable

Modify:

```text id="p5m8q2"
Book
```

Implement:

```java
Comparable<Book>
```

Natural order:

```text id="x7m3q9"
title
```

---

## 2 — Comparator

Create:

```text id="m6q2x8"
BookAuthorComparator
```

---

## 3 — Reports

Create:

```text id="v4m9q2"
ReportService
```

Implement:

```text id="z8m3q5"

printBooksByTitle()

printBooksByAuthor()

```

---

# ✔️ Next Step

In **Chapter 52 — Final Project: Integrating Collections Utilities** we will finish the project features:

* `Collections.max()`
* `Collections.min()`
* `Collections.frequency()`
* `Collections.reverse()`
* `Collections.shuffle()`
* `Collections.unmodifiableList()`

Then we will perform the final project review.
