# Chapter 53 — Final Project: Complete Integration and Review (Part 1)

We have reached the final integration stage of the **Library Management System**.

Throughout this module, we did not just learn syntax.

We learned how to answer:

> "Which collection solves this problem best?"

Now we will connect all components into a complete application design.

---

# Final Application Architecture

Our final structure:

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
    ├── BookAuthorComparator.java
    ├── BookTitleComparator.java
    └── UserComparator.java
```

---

# Responsibility Separation

A key software engineering principle:

> Each class should have one main responsibility.

---

# Main.java

Responsibility:

Only application entry point.

It should:

* Create services.
* Start the menu.
* Receive user input.

It should NOT:

* Store books.
* Validate users.
* Perform borrowing logic.

---

Example:

```java
public class Main {

    public static void main(String[] args){

        BookService bookService =
                new BookService();

        UserService userService =
                new UserService();

    }

}
```

---

# BookService

Responsible for:

```text
Book management
```

Contains:

```java
Map<Integer, Book>
```

---

Operations:

```text
addBook()

findBook()

removeBook()

findAll()
```

---

# UserService

Responsible for:

```text
User management
```

Contains:

```java
Map<Integer, User>
```

---

Operations:

```text
addUser()

findUser()

removeUser()

findAll()
```

---

# LibraryService

Responsible for:

```text
Library operations
```

Contains:

```java
List<BorrowRecord>

Map<Integer, Queue<User>>
```

---

Operations:

```text
borrowBook()

returnBook()

waitingQueue()
```

---

# ReportService

Responsible for:

```text
Data visualization
```

Uses:

```java
Comparable

Comparator

Collections utilities
```

---

# Sharing Collections Between Services

Important architecture decision.

We have:

```text
BookService

contains:

Map<Integer, Book>
```

and:

```text
LibraryService

needs:

same books
```

---

Problem:

If each service creates its own Map:

```text
BookService

Map A


LibraryService

Map B
```

---

They are different.

Adding a book:

```text
Map A

101 → Clean Code
```

---

LibraryService:

```text
Map B

(empty)
```

---

The services are disconnected.

---

# Solution

Share the same collection.

---

Create:

```java
Map<Integer, Book> books =
        new HashMap<>();
```

---

Pass it:

```java
BookService bookService =
        new BookService(books);


LibraryService libraryService =
        new LibraryService(
            books,
            users
        );
```

---

Architecture:

```text
             HashMap

                |

       +--------+--------+

       |                 |

BookService      LibraryService


       |                 |

       Book objects
```

---

# Updating BookService

Before:

```java
public class BookService {

    private Map<Integer, Book> books;


    public BookService(){

        books = new HashMap<>();

    }

}
```

---

Now:

```java
public class BookService {

    private Map<Integer, Book> books;


    public BookService(
            Map<Integer, Book> books){

        this.books = books;

    }

}
```

---

# Updating UserService

Same idea:

```java
public UserService(
        Map<Integer, User> users){

    this.users = users;

}
```

---

# Updating Main

Now:

```java
public class Main {

    public static void main(String[] args){


        Map<Integer, Book> books =
                new HashMap<>();


        Map<Integer, User> users =
                new HashMap<>();


        BookService bookService =
                new BookService(
                    books
                );


        UserService userService =
                new UserService(
                    users
                );


        LibraryService libraryService =
                new LibraryService(
                    books,
                    users
                );

    }

}
```

---

# Why Is This Better?

Because now:

One source of truth.

Example:

Register book:

```text
BookService

adds:

101 → Clean Code
```

---

LibraryService immediately sees:

```text
101 → Clean Code
```

---

# Dependency Injection Concept

This pattern is called:

> Dependency Injection.

The class receives what it needs.

---

Bad:

```java
class LibraryService {

    Map<Integer, Book> books =
        new HashMap<>();

}
```

---

Good:

```java
class LibraryService {

    private Map<Integer, Book> books;


    LibraryService(
        Map<Integer, Book> books){

        this.books = books;

    }

}
```

---

Why?

Because the class does not decide:

* Which Map.
* How it is created.
* Where it comes from.

---

Later in Spring Boot:

You will see:

```java
@Autowired
```

doing a similar idea automatically.

---

# Complete Data Flow Example

Scenario:

User borrows a book.

---

## Step 1

Main receives:

```text
User 1 wants Book 101
```

---

## Step 2

Calls:

```java
libraryService.borrowBook(
    1,
    101
);
```

---

## Step 3

LibraryService:

Searches:

```java
users.get(1)
```

and:

```java
books.get(101)
```

---

## Step 4

Book changes state:

```java
book.borrowBook();
```

---

## Step 5

Creates:

```java
BorrowRecord
```

---

## Step 6

Stores:

```java
history.add(record);
```

---

Final result:

```text
Book

Available = false


History

User → Book
```

---

# Collection Decisions Review

Now let's review every choice.

---

# Books

Collection:

```java
Map<Integer, Book>
```

Why?

* Fast search by ID.
* Unique identifier.
* No duplicate IDs.

Complexity:

```text
get()

Average O(1)
```

---

# Users

Collection:

```java
Map<Integer, User>
```

Why?

Same reason.

---

# Borrow History

Collection:

```java
List<BorrowRecord>
```

Why?

* Order matters.
* Duplicates allowed.
* Sequential access.

---

# Waiting Users

Collection:

```java
Queue<User>
```

Why?

FIFO behavior.

---

# Categories

Collection:

```java
Set<String>
```

Why?

No duplicates.

---

# Reports

Tools:

```java
Comparable

Comparator

Collections
```

Why?

Different sorting requirements.

---

# Final Project Checklist

Before completion:

## Models

☑ Book
☑ User
☑ BorrowRecord

---

## Collections

☑ List
☑ Set
☑ Queue
☑ Map

---

## Sorting

☑ Comparable
☑ Comparator

---

## Utilities

☑ reverse()
☑ shuffle()
☑ max()
☑ min()
☑ frequency()
☑ unmodifiableList()

---

# Exercise Task

Refactor your project:

1. Create shared collections in `Main`.
2. Inject them into services.
3. Test:

```text
Register book

Register user

Borrow book

Print history

Generate report
```

---

# ✔️ Next Step

In **Chapter 54 — Final Project: Console Menu and User Interaction** we will create the final application flow:

* Menu system.
* User commands.
* Complete execution scenario.
* Final testing before module completion.
