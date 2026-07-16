# Chapter 48 — Final Project: Collection Storage Layer (Part 1)

We now have our domain models:

```text id="r4m8x2"
Book

User

BorrowRecord
```

But objects created with `new` disappear when the program finishes.

Example:

```java
Book book = new Book(...);
```

The object exists only in memory.

We need a place to store these objects while the application is running.

This is where collections become our **storage layer**.

---

# What Is the Storage Layer?

In a real application:

```text
Application

        ↓

Service Layer

        ↓

Repository / Database

        ↓

Database
```

---

Example:

```text id="k5m8x3"
Spring Boot Application

        ↓

JPA Repository

        ↓

MySQL
```

---

But our project is console-based.

So instead of a database:

```text id="x7m3q9"
Collections
```

will temporarily store our data.

---

# Our New Architecture

Updated flow:

```text id="m8q3x5"

Main

 ↓

Services

 ↓

Collections

 ↓

Models
```

---

Example:

Registering a book:

```text id="p4m8x2"

Main

calls

BookService

stores

Map<Integer, Book>

contains

Book Object
```

---

# Why Not Store Collections in Main?

A common beginner mistake:

```java
public class Main {

    static List<Book> books =
        new ArrayList<>();

}
```

---

Problem:

Main becomes responsible for:

* Data storage.
* Validation.
* Business rules.
* User interaction.

It becomes difficult to maintain.

---

Better:

```text id="v5m9q2"
Main

only starts application


Service

handles logic
```

---

# Creating BookService

Create:

```text id="z8m3x5"
src/service/BookService.java
```

---

Responsibilities:

```text id="n6q2m8"

Add books

Remove books

Search books

List books
```

---

# First Implementation

```java
package service;

import model.Book;

import java.util.HashMap;
import java.util.Map;


public class BookService {

    private Map<Integer, Book> books;


    public BookService(){

        books = new HashMap<>();

    }

}
```

---

# Why HashMap?

Let's revisit the requirement:

Books need:

* Unique ID.
* Fast search by ID.

Example:

```text id="c5m8q2"

101 → Clean Code

102 → Effective Java

103 → Algorithms
```

---

Search:

```java
books.get(101);
```

Average:

```text id="w7m3x9"
O(1)
```

---

A List would require:

```text id="p8m2q5"

for every book:

compare id

```

Complexity:

```text id="x4m8q1"
O(n)
```

---

# Adding Books

Create method:

```java
public void addBook(Book book){

    books.put(
        book.getId(),
        book
    );

}
```

---

Example:

```java
Book book =
new Book(
    1,
    "Clean Code",
    "Robert Martin",
    "Programming"
);


bookService.addBook(book);
```

---

Map:

```text id="q7m3x8"

Key        Value

1     →    Book Object
```

---

# Searching Books

Requirement:

Search by ID.

---

Method:

```java
public Book findById(int id){

    return books.get(id);

}
```

---

Usage:

```java
Book book =
bookService.findById(1);
```

---

Result:

```text id="m5q8x2"
Clean Code
```

---

# Removing Books

Method:

```java
public void removeBook(int id){

    books.remove(id);

}
```

---

Internally:

```text id="v8m3q5"

Before:

1 → Book
2 → Book


remove(1)


After:

2 → Book
```

---

# Listing All Books

Problem:

Map does not have indexes.

We cannot:

```java
books.get(0);
```

---

Need:

```java
values()
```

---

Method:

```java
public Collection<Book> findAll(){

    return books.values();

}
```

---

Why Collection?

Because:

```text id="k7m3q9"
Map values
```

are not necessarily a List.

---

Usage:

```java
for(Book book : bookService.findAll()){

    System.out.println(book);

}
```

---

# The Collection Hierarchy Connection

Remember:

```text id="r5m8x2"

Iterable

    ↓

Collection

    ↓

List / Set / Queue
```

---

Map is separate:

```text id="x8m3q5"

Map

 |
 +-- HashMap
 +-- TreeMap
 +-- LinkedHashMap
```

---

Therefore:

```java
for(Book book : books)
```

does not work.

---

But:

```java
for(Book book : books.values())
```

works.

---

# Adding Validation

Currently:

```java
books.put(id, book);
```

allows:

```text id="p3m8q5"

101 → Book A

101 → Book B
```

The second replaces the first.

---

Is that good?

Usually:

No.

A duplicate ID should not overwrite.

---

Improve:

```java
public boolean addBook(Book book){

    if(books.containsKey(book.getId())){

        return false;

    }


    books.put(
        book.getId(),
        book
    );


    return true;

}
```

---

Now:

Existing ID:

```text id="z6m3q8"
returns false
```

New ID:

```text id="w5q2m9"
returns true
```

---

# containsKey()

Important HashMap method:

```java
books.containsKey(id)
```

---

Purpose:

Check if the key exists.

Complexity:

Average:

```text id="m4x8q2"
O(1)
```

---

# BookService Final Responsibility

Currently:

```text id="q7m3x9"

BookService

    |
    |
    + Map<Integer,Book>

Methods:

addBook()

findById()

removeBook()

findAll()
```

---

# Testing BookService

Create temporary Main:

```java
import model.Book;
import service.BookService;


public class Main {

    public static void main(String[] args) {


        BookService service =
                new BookService();


        Book book =
                new Book(
                    1,
                    "Clean Code",
                    "Robert Martin",
                    "Programming"
                );


        service.addBook(book);


        System.out.println(
            service.findById(1)
        );


    }

}
```

---

Output:

```text id="h8m3x5"
Book{id=1, title='Clean Code'...}
```

---

# Important Design Decision

Our storage:

```java
Map<Integer, Book>
```

is hidden.

Outside code does not know:

* HashMap.
* How books are stored.
* Internal structure.

It only knows:

```java
BookService
```

---

This allows future changes.

Example:

Today:

```java
HashMap
```

Tomorrow:

```java
Database
```

The rest of the application changes very little.

---

# Exercise Task

Create:

```text id="m7q3x9"
service/BookService.java
```

Implement:

Field:

```java
Map<Integer, Book>
```

Methods:

```text id="x5m8q2"
addBook()

findById()

removeBook()

findAll()
```

Test:

1. Add three books.
2. Search one book.
3. Remove one book.
4. Print all remaining books.

---

# ✔️ Next Step

In **Chapter 49 — Final Project: Collection Storage Layer (Part 2)** we will create:

* `UserService`
* `Map<Integer, User>`

and explore:

* Why Map is better than Set for user management.
* Using `equals()` and `hashCode()` in real collections.
* Preventing duplicate users.
