# Chapter 49 — Final Project: Collection Storage Layer (Part 2)

In the previous chapter, we created:

```text id="g4m8x2"
BookService
```

using:

```java
Map<Integer, Book>
```

Now we will create:

```text id="p7q3m9"
UserService
```

using:

```java
Map<Integer, User>
```

While doing this, we will reinforce an important Collections Framework decision:

> The best collection is chosen based on how the data will be accessed.

---

# User Management Requirements

Our system needs:

## Register users

Example:

```text id="v5m8q2"
ID: 1
Name: Eduardo
Email: edu@email.com
```

---

## Search users

Examples:

```text id="m4x8q1"
Find user by ID
```

---

## Remove users

Example:

```text id="z7m3q5"
Remove user 10
```

---

## Prevent duplicate registration

The same ID cannot exist twice.

---

# Choosing the Collection

Let's analyze possible options.

---

# Option 1 — List<User>

Structure:

```text id="x8m2q5"
[
User,
User,
User
]
```

---

Searching:

```java id="q6m3x8"
find user 100
```

requires:

```text id="p5m8q2"
check every user
```

Complexity:

```text id="r7m3x9"
O(n)
```

---

Problem:

The user ID is the main way we identify users.

A List is not optimized for this.

---

# Option 2 — Set<User>

A Set prevents duplicates.

Example:

```java id="m8q3x5"
Set<User>
```

---

Good:

```text id="v4m9x2"
No duplicate users
```

---

But searching:

```java id="k7m3q8"
find user by id
```

still requires:

```text id="n5m8x2"
iteration
```

Complexity:

```text id="w6m3q9"
O(n)
```

---

# Option 3 — Map<Integer, User>

Structure:

```text id="z8m2q5"

ID          User

1      →   Eduardo

2      →   Maria

3      →   Carlos
```

---

Search:

```java id="p4m8x1"
users.get(1)
```

Average:

```text id="x7m3q9"
O(1)
```

---

Decision:

```java id="m5q8x2"
Map<Integer, User>
```

---

# Creating UserService

Create:

```text id="c6m8x3"
src/service/UserService.java
```

---

Initial structure:

```java id="r5m2q8"
package service;

import model.User;

import java.util.Collection;
import java.util.HashMap;
import java.util.Map;


public class UserService {

    private Map<Integer, User> users;


    public UserService(){

        users = new HashMap<>();

    }

}
```

---

# Adding Users

Method:

```java id="v8m3q5"
public boolean addUser(User user){

    if(users.containsKey(user.getId())){

        return false;

    }


    users.put(
        user.getId(),
        user
    );


    return true;

}
```

---

# Why containsKey()?

Because:

```java id="p7m3x9"
Map
```

uses:

```text id="z4m8q2"
key uniqueness
```

---

Example:

Before:

```text id="n8m3q5"

1 → Eduardo

```

Adding:

```text id="x5m9q2"

1 → Maria

```

---

Without validation:

```text id="m4q8x1"

Eduardo disappears.

```

Because:

```java
put()
```

replaces existing values.

---

# Searching Users

Method:

```java id="q7m3x9"
public User findById(int id){

    return users.get(id);

}
```

---

Example:

```java id="w5m8q2"
User user =
    userService.findById(1);
```

---

# Removing Users

Method:

```java id="x8m3q5"
public void removeUser(int id){

    users.remove(id);

}
```

---

# Listing Users

Maps do not implement Collection.

Remember:

Wrong:

```java id="m6q2x9"
for(User user : users)
```

---

Correct:

```java id="p5m8q2"
users.values()
```

---

Method:

```java id="z7m3x8"
public Collection<User> findAll(){

    return users.values();

}
```

---

Usage:

```java id="r4m8x1"
for(User user : userService.findAll()){

    System.out.println(user);

}
```

---

# Testing UserService

Main:

```java id="k8m3x5"
UserService service =
        new UserService();


User user =
        new User(
            1,
            "Eduardo",
            "edu@email.com"
        );


service.addUser(user);


System.out.println(
        service.findById(1)
);
```

---

Output:

```text id="x5m8q2"
User{id=1, name='Eduardo'...}
```

---

# Where Does equals() Matter Now?

Good question.

Currently:

```java
Map<Integer, User>
```

uses:

```text id="p7m3x9"
Integer key
```

to identify users.

The User object's:

```java
equals()
hashCode()
```

are not used for searching by ID.

---

Example:

```java
users.get(1);
```

Java compares:

```text id="m8q3x5"
Integer keys
```

---

# When Would User.equals() Matter?

If we had:

```java
Set<User>
```

Example:

```java
Set<User> users =
        new HashSet<>();
```

Then:

```java
users.add(user);
```

would use:

1. `hashCode()`
2. `equals()`

---

# Map Internally

Our HashMap:

```java
Map<Integer, User>
```

works conceptually like:

```text id="v4m9x2"

hashCode()

     ↓

bucket

     ↓

equals()
```

---

The key:

```java
Integer
```

already has:

```text id="z8m3q5"
equals()
hashCode()
```

implemented.

---

# BookService vs UserService

Notice the similarity:

```text id="q7m3x9"

BookService

Map<Integer, Book>



UserService

Map<Integer, User>
```

---

Only the object type changes.

This suggests:

> Later we could create generic repositories.

Example:

```java
Repository<T>
```

But generics are not the focus of this module.

---

# Service Layer Responsibility

Our services now hide storage.

Outside code does not do:

```java
users.put()
```

---

Instead:

```java
userService.addUser();
```

---

Why?

Because validation belongs here.

Example:

Later we can add:

```text id="m5q8x2"

Check email format

Check age

Check restrictions

```

without changing Main.

---

# Current Architecture

```text id="x8m3q5"

Main

 |
 v

Services

 |
 +----------------+
 |                |
 v                v

BookService    UserService

 |                |

Map             Map

 |                |

Book            User
```

---

# Exercise Task

Create:

```text id="r7m3x9"
service/UserService.java
```

Implement:

Field:

```java
Map<Integer, User>
```

Methods:

```text
addUser()

findById()

removeUser()

findAll()
```

Test:

1. Register three users.
2. Search one user.
3. Remove one user.
4. Print remaining users.
5. Try adding a duplicate ID.

Expected:

Duplicate registration should fail.

---

# ✔️ Next Step

In **Chapter 50 — Final Project: Borrowing System (List + Queue)** we will implement the main library behavior:

* Borrow books.
* Return books.
* Store borrowing history.
* Create waiting queues.
* Combine `List`, `Queue`, and `Map` together.
