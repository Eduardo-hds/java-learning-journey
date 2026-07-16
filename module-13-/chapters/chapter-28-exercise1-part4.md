# Chapter 28 — Exercise 1: Student Management System (Part 4)

In the previous chapters, we built the basic CRUD operations:

* Create → `addStudent()`
* Read → `listStudents()`, `findById()`
* Update → `updateStudent()`
* Delete → `removeStudent()`

This is the classic CRUD pattern used in real applications.

Now we will improve searching.

We will implement:

* Search by name.
* Understand `contains()`.
* Learn why `ArrayList` is not always the best choice.
* Prepare for the next design evolution using `Map`.

---

# Current Structure

```text id="k5n2p7"
StudentService

+ addStudent()
+ listStudents()
+ findById()
+ removeStudent()
+ updateStudent()
```

New:

```text id="w8q3m6"
+ findByName()
```

---

# Part 1 — Searching by Name

Requirement:

The user enters:

```text id="m4x9q1"
Name: Alice
```

The system returns:

```text id="s7k2v5"
Student{id=1, name='Alice'}
```

---

# Implementation

StudentService:

```java id="j7m3q9"
public Student findByName(String name){

    for(Student student : students){

        if(student.getName()
                 .equals(name)){

            return student;

        }

    }

    return null;
}
```

---

# How It Works

Collection:

```text id="c8q2m5"
[
 Alice,
 Bob,
 Carlos
]
```

Search:

```text id="p3x7k9"
findByName("Bob")
```

Java checks:

---

First:

```text id="u6m1q4"
Alice.equals(Bob)
```

False.

---

Second:

```text id="v8n3p2"
Bob.equals(Bob)
```

True.

Return.

---

# Complexity

Again:

```text id="y5q8m3"
O(n)
```

Because we may need to check every student.

---

# Improving Name Comparison

Current:

```java id="h8p3x1"
equals()
```

is case-sensitive.

Example:

```text id="m7q4v9"
Alice
alice
```

are different.

---

# Case-Insensitive Search

Use:

```java id="z4n8m2"
equalsIgnoreCase()
```

Example:

```java id="b6q9x3"
if(student.getName()
          .equalsIgnoreCase(name))
```

Now:

```text id="p2m7v5"
Alice
alice
ALICE
```

all match.

---

# Part 2 — Using contains()

Collections provide:

```java id="q5m8x1"
contains()
```

Example:

```java id="d8p3v6"
students.contains(student);
```

Question:

How does Java know if the student exists?

Answer:

It uses:

```java id="x7m2q9"
equals()
```

---

# Example

Student:

```java id="r4n8k6"
Student(1,"Alice")
```

Search:

```java id="h3q7m2"
Student(1,"Alice")
```

Without equals():

```text id="k9v5p1"
Not found
```

Because they are different objects.

---

With equals():

```text id="m2x8q4"
Found
```

---

# Important Collection Relationship

Many methods depend on equals():

| Method         | Uses equals() |
| -------------- | ------------- |
| contains()     | Yes           |
| remove(Object) | Yes           |
| indexOf()      | Yes           |
| lastIndexOf()  | Yes           |

---

# Part 3 — indexOf()

Another useful method:

```java id="v8m3q6"
students.indexOf(student);
```

Returns position.

Example:

```text id="y6p2n8"
[
 Alice,
 Bob,
 Carlos
]
```

Code:

```java id="s4x7m9"
indexOf(Bob)
```

Result:

```text id="n9q3v5"
1
```

---

# Why Is This Important?

Because:

```java id="m8x2q5"
ArrayList
```

is based on indexes.

Internally:

```text id="d4q7p1"
0 -> Alice
1 -> Bob
2 -> Carlos
```

---

# Part 4 — Searching Performance Problem

Our current design:

```java id="q8m5v2"
List<Student>
```

Search:

```java id="z6n3x9"
findById()
```

requires:

```text id="h1q5m7"
Loop through everything
```

---

Imagine:

```text id="x3p8n6"
1 million students
```

Searching:

```text id="v7m2q9"
ID = 999999
```

requires:

```text id="c5n8m3"
999999 comparisons
```

---

# Better Design: HashMap

Instead of:

```java id="u9m3x7"
List<Student>
```

we could use:

```java id="p6q8m2"
Map<Integer,Student>
```

Structure:

```text id="n5v2x8"
ID
 |
 v
Student
```

Example:

```text id="w3m7q9"
1 → Alice
2 → Bob
3 → Carlos
```

Search:

```java id="r8p2m5"
students.get(2);
```

---

Complexity:

Average:

```text id="m6q9x1"
O(1)
```

---

# Why Not Change Now?

Because we are learning the collections one by one.

This exercise intentionally shows:

## ArrayList strengths:

* Ordered data.
* Simple traversal.
* Easy implementation.

## ArrayList weakness:

* Slow searching by identifier.

---

# Real Application Design

Many applications use both:

Example:

```java id="v4m8q2"
List<Student> studentList;

Map<Integer,Student> studentMap;
```

---

Why?

List:

```text id="x7q3m5"
Display students in order
```

Map:

```text id="p9m4v8"
Fast lookup by ID
```

---

# Part 5 — Add Search by Name Returning Multiple Students

A name is not always unique.

Example:

```text id="z2m6q8"
John
John
Maria
```

Returning one student is incorrect.

Better:

```java id="f8n3m7"
public List<Student> findByName(String name)
```

---

Return:

```text id="h5q1v9"
[
 Student John,
 Student John
]
```

---

Implementation:

```java id="x3m7p5"
public List<Student> findByName(String name){

    List<Student> result =
            new ArrayList<>();


    for(Student student : students){

        if(student.getName()
                 .equalsIgnoreCase(name)){

            result.add(student);

        }

    }


    return result;

}
```

---

# Why Create Another List?

Because we should not expose the original collection.

Wrong:

```java id="m9q3x6"
return students;
```

The caller could modify our internal data.

---

Better:

```text id="v5p8m2"
Create result
Return matching objects
```

---

# Current StudentService

Now:

```text id="k7m3q8"
StudentService

+ addStudent()
+ listStudents()
+ findById()
+ findByName()
+ removeStudent()
+ updateStudent()
```

---

# Concepts Practiced

You used:

✅ ArrayList searching
✅ equals()
✅ contains()
✅ indexOf()
✅ Case-insensitive comparison
✅ Returning filtered collections
✅ Complexity analysis

---

# Exercise Task

Implement:

1. `findByName(String name)` returning one student.
2. Improve it to return `List<Student>`.
3. Test with duplicate names.

Example:

Students:

```text
John
Maria
John
```

Search:

```text
John
```

Result:

```text
2 students found
```

---

# ✔️ Next Step

In **Chapter 29 — Student Management System (Part 5)** we will refactor the project and compare two designs:

**Version 1:**

```java
ArrayList<Student>
```

**Version 2:**

```java
HashMap<Integer, Student>
```

We will analyze the trade-offs and decide which structure is better for a real student management system.
