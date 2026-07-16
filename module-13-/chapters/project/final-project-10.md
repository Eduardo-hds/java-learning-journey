# Chapter 54 — Final Project: Console Menu and User Interaction

Our application logic is now complete.

We have:

✅ Models
✅ Services
✅ Collections
✅ Sorting
✅ Reports

Now we need the part that allows a user to interact with the system.

A console application needs:

* Input handling.
* Options menu.
* Calling the correct service methods.

---

# Application Flow

The final execution flow:

```text
User

 ↓

Main Menu

 ↓

Service

 ↓

Collection

 ↓

Model Object
```

---

Example:

User chooses:

```text
1 - Register Book
```

Flow:

```text
Main

calls

BookService.addBook()

stores in

Map<Integer, Book>
```

---

# Why Keep Menu Logic in Main?

For this project:

`Main` is responsible for:

* Starting the program.
* Reading input.
* Calling services.

It should not contain:

* Collection manipulation.
* Business rules.

---

# Creating Menu Structure

Example:

```text
==============================
 Library Management System
==============================

1 - Register Book
2 - List Books
3 - Register User
4 - List Users
5 - Borrow Book
6 - Return Book
7 - View Borrow History
8 - Exit

Choose:
```

---

# Scanner

Create:

```java
Scanner scanner =
        new Scanner(System.in);
```

---

Read option:

```java
int option =
        scanner.nextInt();
```

---

# Main Loop

A menu normally runs until the user exits.

Structure:

```java
boolean running = true;


while(running){

    showMenu();

    int option =
        scanner.nextInt();


    switch(option){

        case 1:
            registerBook();
            break;


        case 8:
            running = false;
            break;

    }

}
```

---

# Why Use while?

Because:

The program should not end after one operation.

Example:

```text
Register book

then

Register user

then

Borrow book
```

---

The application state remains in memory.

---

# Registering Books

Method:

```java
private static void registerBook(
        Scanner scanner,
        BookService service){

}
```

---

Collect data:

```java
System.out.print("ID: ");
int id = scanner.nextInt();


scanner.nextLine();


System.out.print("Title: ");
String title = scanner.nextLine();
```

---

Create object:

```java
Book book =
    new Book(
        id,
        title,
        author,
        category
    );
```

---

Store:

```java
boolean added =
        service.addBook(book);
```

---

Result:

```java
if(added){

    System.out.println(
        "Book registered"
    );

}
```

---

# Listing Books

Service already provides:

```java
findAll()
```

---

Main only displays:

```java
for(Book book :
        service.findAll()){


    System.out.println(book);

}
```

---

Notice:

Main does not know:

```text
HashMap
```

or:

```text
Map<Integer,Book>
```

---

It only knows:

```java
BookService
```

---

# Registering Users

Same pattern:

Input:

```text
ID
Name
Email
```

Create:

```java
User user =
    new User(
        id,
        name,
        email
    );
```

---

Store:

```java
userService.addUser(user);
```

---

# Borrowing a Book

User enters:

```text
User ID:
1


Book ID:
100
```

---

Main calls:

```java
libraryService.borrowBook(
    userId,
    bookId
);
```

---

The service handles:

* Does user exist?
* Does book exist?
* Is available?
* Create record.

---

# Returning a Book

Input:

```text
Book ID:
100
```

---

Call:

```java
libraryService.returnBook(
    bookId
);
```

---

# Viewing History

Call:

```java
libraryService.getHistory()
```

---

Print:

```java
for(BorrowRecord record :
        history){

    System.out.println(record);

}
```

---

# Complete Main Responsibility

At the end:

```text
Main.java


Responsible:

✓ Menu

✓ User input

✓ Calling services


Not responsible:

✗ Collections

✗ Validation

✗ Business rules
```

---

# Example Complete Execution

Starting:

```text
Library Management System
```

---

Register book:

```text
ID: 1
Title: Clean Code
Author: Robert Martin
Category: Programming
```

Stored:

```text
Map

1 → Book
```

---

Register user:

```text
ID: 10
Name: Eduardo
```

Stored:

```text
Map

10 → User
```

---

Borrow:

```text
User 10

borrows

Book 1
```

---

Internal changes:

Before:

```text
Book

available = true
```

After:

```text
Book

available = false
```

History:

```text
[
 Eduardo → Clean Code
]
```

---

# Testing Scenarios

Before final completion, test edge cases.

---

# Test 1 — Duplicate Book ID

Attempt:

```text
Book ID: 1
```

again.

Expected:

```text
Registration failed
```

---

# Test 2 — Duplicate User ID

Attempt:

```text
User ID: 10
```

again.

Expected:

```text
Registration failed
```

---

# Test 3 — Borrow Unavailable Book

User A:

```text
Borrow Book 1
```

User B:

```text
Borrow Book 1
```

Expected:

```text
Book unavailable
```

---

# Test 4 — Search Missing Book

Try:

```text
Book ID: 999
```

Expected:

```text
Book not found
```

---

# Test 5 — Waiting Queue

Scenario:

```text
Book unavailable

User B waits

User A returns

```

Expected:

```text
Queue processed
```

---

# Performance Review

Let's analyze our operations.

---

## Find Book

Collection:

```java
Map<Integer,Book>
```

Operation:

```java
get()
```

Average:

```text
O(1)
```

---

## Add Borrow Record

Collection:

```java
ArrayList
```

Operation:

```java
add()
```

Average:

```text
O(1)
```

---

## Search History

Collection:

```java
List
```

Operation:

```text
loop
```

Complexity:

```text
O(n)
```

---

## Queue Processing

Collection:

```java
Queue
```

Operation:

```java
poll()
```

Complexity:

```text
O(1)
```

---

# What We Learned From The Project

The project was not about memorizing:

```java
new ArrayList<>()
```

or:

```java
new HashMap<>()
```

The real skill:

Analyzing requirements.

---

Example:

Requirement:

> Find books quickly by ID.

Decision:

```java
Map<Integer,Book>
```

---

Requirement:

> Keep borrowing order.

Decision:

```java
List<BorrowRecord>
```

---

Requirement:

> First person waiting receives the book.

Decision:

```java
Queue<User>
```

---

Requirement:

> Avoid duplicate categories.

Decision:

```java
Set<String>
```

---

# Final Project Status

The Library Management System now contains:

```text
Models
 |
 +-- Book
 +-- User
 +-- BorrowRecord


Services
 |
 +-- BookService
 +-- UserService
 +-- LibraryService
 +-- ReportService


Collections
 |
 +-- Map
 +-- List
 +-- Set
 +-- Queue


Sorting
 |
 +-- Comparable
 +-- Comparator
```

---

# Exercise Task

Complete your application:

1. Create the menu.
2. Connect all services.
3. Run all test scenarios.
4. Refactor duplicated code.
5. Add comments explaining collection decisions.

---

# ✔️ Next Step

In **Chapter 55 — Module Review: Collections Framework Deep Review** we will review:

* Complete Collections hierarchy.
* Internal behavior of each collection.
* Performance comparison table.
* When to use each collection.
* Common interview questions.
