# Chapter 46 — Final Project: Creating Domain Models (Part 1)

Now we begin the implementation phase of the **Library Management System**.

Before creating collections, services, and business rules, we need to create the objects that our collections will store.

This is an important design principle:

> Collections organize objects. They do not replace object design.

A bad model creates problems later, even if the collection choice is correct.

---

# Project Architecture

Current structure:

```text
src/
│
├── Main.java
│
├── model/
│   ├── Book.java
│   ├── User.java
│   └── BorrowRecord.java
│
├── service/
│   ├── BookService.java
│   ├── UserService.java
│   ├── LibraryService.java
│   └── ReportService.java
│
└── util/
    ├── BookComparator.java
    └── UserComparator.java
```

---

# Why Start With Models?

The flow of our application:

```text
Main

 ↓

Services

 ↓

Collections

 ↓

Model Objects
```

Example:

A book is created:

```java
Book book = new Book();
```

Then stored:

```java
Map<Integer, Book>
```

The collection does not know what a book is.

It only stores references.

---

# Domain Model 1 — Book

A library book needs information.

Let's analyze the requirements.

---

# Book Requirements

A book needs:

## Identification

Something unique.

Examples:

* ID.
* ISBN.

We will use:

```java
int id;
```

---

## Information

The user needs:

```java
String title;

String author;

String category;
```

---

## Availability

The system needs to know:

Can someone borrow it?

```java
boolean available;
```

---

# Book Class

Create:

```text
src/model/Book.java
```

---

Initial structure:

```java
package model;

public class Book {

    private int id;
    private String title;
    private String author;
    private String category;
    private boolean available;

}
```

---

# Why private fields?

Because objects should control their own state.

Wrong:

```java
book.available = false;
```

Anyone can change it.

---

Better:

```java
book.borrow();
```

The object controls the change.

---

# Constructor

A book cannot exist without basic information.

Create:

```java
public Book(
        int id,
        String title,
        String author,
        String category){

    this.id = id;
    this.title = title;
    this.author = author;
    this.category = category;
    this.available = true;

}
```

---

# Why Default Available?

When registering a book:

```text
Book enters library
```

Naturally:

```text
Available = true
```

---

# Getters

We need access to information.

Example:

The service needs:

```java
book.getId();
```

---

Add:

```java
public int getId(){

    return id;

}
```

---

```java
public String getTitle(){

    return title;

}
```

---

```java
public String getAuthor(){

    return author;

}
```

---

```java
public String getCategory(){

    return category;

}
```

---

# Availability Methods

Instead of exposing:

```java
boolean available;
```

create behavior.

---

Check:

```java
public boolean isAvailable(){

    return available;

}
```

---

Borrow:

```java
public void borrowBook(){

    available = false;

}
```

---

Return:

```java
public void returnBook(){

    available = true;

}
```

---

# Why Methods Instead of Setter?

Imagine later we add:

* Borrow date.
* Validation.
* Maximum borrow time.

With:

```java
setAvailable(false);
```

we cannot control the process.

With:

```java
borrowBook();
```

we can expand behavior.

---

# Current Book Class

Conceptually:

```text
Book

Attributes:

id
title
author
category
available


Behaviors:

isAvailable()

borrowBook()

returnBook()
```

---

# Adding toString()

Collections often need readable output.

Without:

```java
System.out.println(book);
```

Output:

```text
model.Book@4a54c0
```

Not useful.

---

Add:

```java
@Override
public String toString(){

    return "Book{" +
            "id=" + id +
            ", title='" + title + '\'' +
            ", author='" + author + '\'' +
            ", category='" + category + '\'' +
            ", available=" + available +
            '}';

}
```

---

# Why toString() Matters With Collections

Example:

```java
Map<Integer, Book> books;
```

Printing:

```java
System.out.println(books);
```

uses:

```text
Book.toString()
```

---

# Important Collections Connection

Our future collection:

```java
Map<Integer, Book>
```

will use:

```text
id
```

as the key.

Example:

```java
books.put(
    101,
    new Book(...)
);
```

---

Structure:

```text
Key        Value

101   →    Book Object
```

---

# Does Book Need equals() and hashCode()?

Good question.

Depends where it is used.

---

If we store:

```java
List<Book>
```

Maybe not immediately.

---

If we store:

```java
Set<Book>
```

Yes.

Because Set needs to know:

> Are these two books the same?

---

Example:

```java
Book b1 =
new Book(
101,
"Java",
"Author",
"Programming"
);


Book b2 =
new Book(
101,
"Java",
"Author",
"Programming"
);
```

---

Without equals:

Java sees:

```text
b1 != b2
```

because they are different objects in memory.

---

Later we will decide:

Which fields define book equality.

---

# Exercise Task

Create:

```text
model/Book.java
```

Implement:

Fields:

```text
id
title
author
category
available
```

Methods:

```text
constructor

getters

isAvailable()

borrowBook()

returnBook()

toString()
```

---

Test in Main:

```java
Book book =
    new Book(
        1,
        "Clean Code",
        "Robert Martin",
        "Programming"
    );


System.out.println(book);
```

Expected:

```text
Book{id=1, title='Clean Code', author='Robert Martin', category='Programming', available=true}
```

---

# Design Lesson

Before choosing:

```java
Map<Integer, Book>
```

we designed:

```java
Book
```

because:

> The collection choice depends on the object structure.

---

# ✔️ Next Step

In **Chapter 47 — Final Project: Creating Domain Models (Part 2)** we will create:

* `User`
* `BorrowRecord`

and discuss:

* Object identity.
* `equals()` and `hashCode()`.
* Why these methods are critical for `HashMap` and `HashSet`.
