# Chapter 47 — Final Project: Creating Domain Models (Part 2)

In the previous chapter, we created our first domain object:

```java
Book
```

Now we will create the remaining objects:

* `User`
* `BorrowRecord`

During this process, we will also learn an essential Collections Framework concept:

> How Java identifies objects inside collections.

This leads us to:

* `equals()`
* `hashCode()`

---

# Domain Model 2 — User

The library needs people who interact with the system.

A user needs:

* Identification.
* Personal information.
* Borrowing relationship.

---

# User Requirements

A user has:

## ID

Unique identifier:

```java
int id;
```

---

## Name

```java
String name;
```

---

## Email

```java
String email;
```

---

# User Class

Create:

```text
src/model/User.java
```

---

Initial structure:

```java
package model;

public class User {

    private int id;
    private String name;
    private String email;

}
```

---

# Constructor

A user requires:

```java
id
name
email
```

---

Implementation:

```java
public User(
        int id,
        String name,
        String email){

    this.id = id;
    this.name = name;
    this.email = email;

}
```

---

# Getters

Add:

```java
public int getId(){

    return id;

}
```

---

```java
public String getName(){

    return name;

}
```

---

```java
public String getEmail(){

    return email;

}
```

---

# toString()

For readable output:

```java
@Override
public String toString(){

    return "User{" +
            "id=" + id +
            ", name='" + name + '\'' +
            ", email='" + email + '\'' +
            '}';

}
```

---

# The Collections Problem

Now imagine:

```java
Set<User> users;
```

The requirement:

> A user cannot register twice.

---

Example:

```java
User user1 =
new User(
    1,
    "Eduardo",
    "edu@email.com"
);


User user2 =
new User(
    1,
    "Eduardo",
    "edu@email.com"
);
```

---

Without customization:

```java
users.add(user1);

users.add(user2);
```

Result:

```text
2 users
```

Why?

Because Java compares:

```text
Memory address
```

not the user data.

---

# Object Equality

Java asks:

> When are two objects considered equal?

For our User:

Two users are equal when:

```text
same id
```

---

Example:

```text
User 1

ID: 10
Name: Eduardo


User 2

ID: 10
Name: Another Name
```

Should they be the same user?

Yes.

Because:

```text
ID identifies the entity.
```

---

# equals()

The equals method defines logical equality.

Add:

```java
@Override
public boolean equals(Object object){

    if(this == object){
        return true;
    }


    if(!(object instanceof User)){
        return false;
    }


    User user = (User) object;


    return id == user.id;

}
```

---

# Understanding equals()

First:

```java
if(this == object)
```

Checks:

> Same memory reference?

Example:

```java
user1 == user1
```

Always true.

---

Second:

```java
instanceof User
```

Checks:

> Is this another User?

---

Third:

```java
id == user.id
```

Our business rule:

Same ID = same user.

---

# hashCode()

Now the important part.

Hash-based collections use:

```java
HashMap
HashSet
```

They do not only use equals.

They also use:

```java
hashCode()
```

---

Rule:

If:

```text
a.equals(b) == true
```

then:

```text
a.hashCode() == b.hashCode()
```

must also be true.

---

Add:

```java
@Override
public int hashCode(){

    return Integer.hashCode(id);

}
```

---

# Why Is This Important?

HashSet internally works like:

```text
hashCode()

↓

find bucket

↓

equals()
```

---

Without hashCode:

Java may search in the wrong place.

---

# User Final Structure

```text
User

Fields:

id
name
email


Methods:

getters

equals()

hashCode()

toString()
```

---

# Domain Model 3 — BorrowRecord

Now we need to represent borrowing.

A borrowing connects:

```text
User

+

Book
```

---

Example:

```text
User:
Eduardo


Borrowed:

Clean Code
```

---

# BorrowRecord Requirements

Needs:

```java
User user;

Book book;
```

---

Maybe later:

```java
LocalDate borrowDate;
```

But Date API belongs to another module.

For now:

Keep simple.

---

# Create Class

File:

```text
src/model/BorrowRecord.java
```

---

Structure:

```java
package model;

public class BorrowRecord {

    private User user;
    private Book book;

}
```

---

# Constructor

```java
public BorrowRecord(
        User user,
        Book book){

    this.user = user;
    this.book = book;

}
```

---

# Getters

```java
public User getUser(){

    return user;

}
```

---

```java
public Book getBook(){

    return book;

}
```

---

# toString()

```java
@Override
public String toString(){

    return "BorrowRecord{" +
            "user=" + user.getName() +
            ", book=" + book.getTitle() +
            '}';

}
```

---

# Why Store Objects Instead of IDs?

Question:

Why not:

```java
int userId;

int bookId;
```

?

---

Because objects provide relationships.

Example:

```text
BorrowRecord

        |
        |
        v

User Object

        |
        |
        v

Book Object
```

---

We can directly access:

```java
record.getUser().getName();
```

---

Instead of:

```text
search user by id again
```

---

# Collections Connection

Now our final system has:

---

## Books

```java
Map<Integer, Book>
```

---

## Users

```java
Map<Integer, User>
```

---

## Borrow History

```java
List<BorrowRecord>
```

---

## Waiting Queue

```java
Queue<User>
```

---

# Why These Models Matter

Collections store references.

Example:

```java
books.put(
    1,
    book
);
```

The Map stores:

```text
Reference → Book object
```

not a copy.

---

# Common Mistakes

---

## Mistake 1 — Comparing Objects With ==

Wrong:

```java
user1 == user2
```

This compares:

```text
memory reference
```

---

Correct:

```java
user1.equals(user2)
```

---

## Mistake 2 — Creating equals Without hashCode

Wrong:

```java
@Override
equals()
```

only.

---

For:

```java
HashSet
HashMap
```

always implement both.

---

## Mistake 3 — Using Mutable Fields in hashCode

Bad:

```java
hashCode(name)
```

because:

```text
name changes
```

and the object may become unreachable inside a HashSet.

---

# Exercise Task

Create:

```text
model/User.java
```

with:

Fields:

```text
id
name
email
```

Methods:

```text
constructor

getters

equals()

hashCode()

toString()
```

---

Create:

```text
model/BorrowRecord.java
```

with:

Fields:

```text
User user

Book book
```

Methods:

```text
constructor

getters

toString()
```

---

Test:

Create:

```java
User user1 =
new User(
1,
"Eduardo",
"edu@email.com"
);


User user2 =
new User(
1,
"Eduardo",
"edu@email.com"
);
```

Check:

```java
System.out.println(
    user1.equals(user2)
);
```

Expected:

```text
true
```

---

# ✔️ Next Step

In **Chapter 48 — Final Project: Collection Storage Layer** we will create the first services:

* `BookService`
* `UserService`

and implement:

* `Map<Integer, Book>`
* `Map<Integer, User>`

We will see how collections become the application's storage layer.
