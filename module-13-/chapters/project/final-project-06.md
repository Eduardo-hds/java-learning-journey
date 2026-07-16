# Chapter 50 — Final Project: Borrowing System (List + Queue)

Until now, our system can:

✅ Store books
✅ Store users

Using:

```text id="v8m3q5"
Map<Integer, Book>

Map<Integer, User>
```

But a library is not only about storing data.

The main operation is:

> A user borrows a book.

Now we will create the borrowing system.

This chapter combines:

* `Map`
* `List`
* `Queue`

---

# Borrowing Requirements

The system must support:

## Borrow a book

Example:

```text id="q5m8x2"

User:

Eduardo


Book:

Clean Code

```

Result:

```text id="x7m3q9"

Book becomes unavailable.

Borrowing record is created.

```

---

## Return a book

Example:

```text id="m4q8x1"

Eduardo returns Clean Code.

```

Result:

```text id="z8m3q5"

Book becomes available again.

```

---

## Keep history

The system needs:

```text id="p5m8x2"

Who borrowed what?

```

---

## Waiting queue

If a book is unavailable:

Example:

```text id="w6m3q9"

Clean Code

Maria waiting

Carlos waiting

```

The first person should receive it.

---

# Choosing Collections

Now we analyze.

---

# Borrow History

Requirement:

Order matters.

Example:

```text id="r7m3x9"

1 - Clean Code

2 - Effective Java

3 - Algorithms

```

---

Need:

* Keep insertion order.
* Allow duplicates.

---

Set?

No.

Because:

```text id="x5m8q2"

Two borrowings can happen for same book.
```

---

Map?

Not ideal.

We do not need key lookup.

---

Decision:

```java id="m6q2x8"
List<BorrowRecord>
```

---

# Waiting Queue

Requirement:

First person waiting gets priority.

Example:

```text id="v4m9q2"

Queue:

Maria

John

Carlos

```

When book returns:

Maria gets it first.

---

This is:

```text id="n8m3q5"
FIFO
```

---

Decision:

```java id="z7m3x9"
Queue<User>
```

---

# Creating LibraryService

Create:

```text id="x8m2q5"
src/service/LibraryService.java
```

---

Responsibilities:

```text id="p5m8x2"

Borrow books

Return books

Manage history

Manage waiting queues

```

---

Initial structure:

```java id="q7m3x9"
package service;

import model.Book;
import model.BorrowRecord;
import model.User;

import java.util.*;


public class LibraryService {


    private Map<Integer, Book> books;

    private Map<Integer, User> users;

    private List<BorrowRecord> history;


}
```

---

# Constructor

We need initialize collections:

```java id="m4x8q2"
public LibraryService(
        Map<Integer, Book> books,
        Map<Integer, User> users){


    this.books = books;

    this.users = users;

    this.history =
            new ArrayList<>();

}
```

---

# Why Receive Maps Instead of Creating New Ones?

Example:

Wrong:

```java id="x5m8q2"
new HashMap<>();
```

inside LibraryService.

---

Why?

Because then:

```text id="v7m3q9"

BookService

has one Map


LibraryService

has another Map

```

---

The services would not share data.

---

Correct:

```text id="r8m3x5"

BookService
       |
       |
       v

same Map

       ^
       |
LibraryService

```

---

# Borrowing a Book

Method:

```java id="k6m3x8"
public boolean borrowBook(
        int userId,
        int bookId){

}
```

---

Steps:

1. Find user.
2. Find book.
3. Check availability.
4. Update book.
5. Create record.

---

# Step 1 — Find User

```java id="p5m8q2"
User user =
        users.get(userId);
```

---

If:

```java id="z8m3q5"
user == null
```

User does not exist.

---

# Step 2 — Find Book

```java id="x7m3q9"
Book book =
        books.get(bookId);
```

---

# Step 3 — Check Availability

```java id="m4x8q2"
if(!book.isAvailable()){

    return false;

}
```

---

# Step 4 — Borrow

Call object behavior:

```java id="q7m3x9"
book.borrowBook();
```

---

Remember:

We do not do:

```java id="n5m8x2"
book.setAvailable(false);
```

---

The object controls its state.

---

# Step 5 — Create Record

```java id="v8m3q5"
BorrowRecord record =
        new BorrowRecord(
            user,
            book
        );
```

---

Add history:

```java id="p4m8x1"
history.add(record);
```

---

# Complete Flow

Conceptually:

```text id="r7m3x9"

borrowBook()

      |

Find User

      |

Find Book

      |

Check availability

      |

Book.borrowBook()

      |

history.add()

```

---

# Returning a Book

Method:

```java id="x5m8q2"
public void returnBook(
        int bookId){

}
```

---

Find:

```java id="m6q2x8"
Book book =
        books.get(bookId);
```

---

Return:

```java id="v4m9q2"
book.returnBook();
```

---

# Listing History

Method:

```java id="z7m3x9"
public List<BorrowRecord> getHistory(){

    return history;

}
```

---

Usage:

```java id="p5m8q2"
for(BorrowRecord record : history){

    System.out.println(record);

}
```

---

# Adding Queue Support

Now the more interesting part.

Imagine:

```text id="q8m3x5"

Clean Code

Unavailable.

```

---

Maria wants it:

```text id="x7m2q9"
waiting
```

---

Need:

```java id="m4x8q2"
Map<Integer, Queue<User>>
```

---

Why?

Because each book can have its own waiting list.

Example:

```text id="r5m8q2"

Book ID

101 → [Maria, John]

102 → [Carlos]

```

---

Structure:

```java id="v8m3x5"
private Map<Integer, Queue<User>> waitingQueues;
```

---

Initialize:

```java id="z6m2q8"
waitingQueues =
        new HashMap<>();
```

---

# Adding User To Queue

Method:

```java id="x4m8q2"
public void addToWaitingQueue(
        int bookId,
        User user){

}
```

---

Get queue:

```java id="p7m3x9"
Queue<User> queue =
        waitingQueues
        .computeIfAbsent(
            bookId,
            id -> new LinkedList<>()
        );
```

---

Add:

```java id="m5q8x2"
queue.offer(user);
```

---

# Why Queue Instead of List?

Could use:

```java id="r8m3x5"
List<User>
```

but:

Queue communicates intent.

The code says:

> This is FIFO processing.

---

# Queue Operations

Important methods:

| Method  | Purpose      |
| ------- | ------------ |
| offer() | Add element  |
| poll()  | Remove first |
| peek()  | View first   |

---

Example:

Queue:

```text id="x7m3q9"

Maria
John
Carlos

```

---

```java id="m4x8q2"
queue.poll();
```

Returns:

```text id="z8m3q5"
Maria
```

---

Queue becomes:

```text id="p5m8x2"

John
Carlos
```

---

# Current Library Architecture

```text id="q7m3x9"

LibraryService


books

Map<Integer, Book>



users

Map<Integer, User>



history

List<BorrowRecord>



waitingQueues

Map<Integer, Queue<User>>

```

---

# Collections Used So Far

We now have:

## Map

```text id="x8m2q5"
Fast lookup
```

---

## List

```text id="m6q2x8"
Ordered history
```

---

## Queue

```text id="v4m9q2"
Waiting system
```

---

# Exercise Task

Implement in `LibraryService`:

Methods:

```text id="z7m3x9"

borrowBook()

returnBook()

getHistory()

addToWaitingQueue()

```

Test scenario:

1. Create one book.
2. Create two users.
3. User A borrows the book.
4. User B tries to borrow the same book.
5. User B enters waiting queue.
6. User A returns the book.

---

# Expected Flow

Before:

```text id="p5m8q2"

Book:

Clean Code

Available: true

```

---

After User A:

```text id="x7m3q9"

Available: false

History:

Eduardo → Clean Code

```

---

User B:

```text id="m4x8q2"

Waiting:

Maria

```

---

After return:

```text id="z8m3q5"

Book:

Available: true

Queue:

Maria

```

---

# ✔️ Next Step

In **Chapter 51 — Final Project: Sorting and Reports** we will implement:

* `Comparable` for natural ordering.
* `Comparator` for different reports.
* Sorting books by:

  * title
  * author
  * category
* Using:

  * `Collections.sort()`
  * `List.sort()`

This will complete the sorting requirements of the project.
