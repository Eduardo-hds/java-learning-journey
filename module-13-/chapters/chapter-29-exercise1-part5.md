# Chapter 29 — Exercise 1: Student Management System (Part 5)

In the previous chapters, we built our first version using:

```java
List<Student>
```

with:

```java
ArrayList<Student>
```

This worked well, but now we will analyze a real-world design question:

> "Is a List really the best structure for this problem?"

The answer depends on how the application uses the data.

---

# Current Design — Version 1

Our current storage:

```java
private List<Student> students =
        new ArrayList<>();
```

Structure:

```text
Index

0  → Student
1  → Student
2  → Student
```

---

# Strengths of This Design

## 1. Maintains Order

Example:

Students registered:

```text
1 - Alice
2 - Bob
3 - Carlos
```

The order is preserved.

---

## 2. Simple Iteration

Displaying all students:

```java
for(Student student : students){

    System.out.println(student);

}
```

Very natural.

---

## 3. Good for Reports

Example:

"Show all students in registration order."

A List is perfect.

---

# Weaknesses

The biggest problem:

Searching by ID.

Current:

```java
findById(1000);
```

Implementation:

```java
for(Student student : students)
```

---

Complexity:

```text
O(n)
```

---

# Problem Scenario

Imagine:

```text
500,000 students
```

Search:

```text
ID = 499999
```

The application may check:

```text
499999 students
```

before finding the result.

---

# Introducing HashMap

Now we redesign.

Instead of:

```java
List<Student>
```

we use:

```java
Map<Integer, Student>
```

---

# New Structure

Example:

```java
private Map<Integer, Student> students =
        new HashMap<>();
```

---

Data:

```text
Key       Value

1    →    Alice
2    →    Bob
3    →    Carlos
```

---

# Why Use ID as Key?

Because:

```text
Student ID
```

is unique.

It becomes the direct identifier.

---

# Adding Students

Before:

```java
students.add(student);
```

Now:

```java
students.put(
    student.getId(),
    student
);
```

---

Example:

```java
students.put(
    1,
    Alice
);
```

Result:

```text
1 → Alice
```

---

# Searching

Before:

```java
for(Student student : students)
```

Now:

```java
Student student =
        students.get(id);
```

---

Example:

```java
students.get(2);
```

Returns:

```text
Bob
```

---

# Complexity Comparison

## ArrayList

Search:

```text
O(n)
```

---

## HashMap

Search:

Average:

```text
O(1)
```

---

This is a huge difference.

---

# Updating Students

With ArrayList:

```java
find student
change values
```

---

With HashMap:

```java
Student student =
        students.get(id);


student.setGrade(10);
```

Much simpler.

---

# Removing Students

ArrayList:

```java
students.remove(student);
```

Needs:

1. Search.
2. Shift elements.

Complexity:

```text
O(n)
```

---

HashMap:

```java
students.remove(id);
```

Average:

```text
O(1)
```

---

# But Is HashMap Always Better?

No.

This is the important lesson.

Every collection is a trade-off.

---

# HashMap Disadvantages

## 1. No guaranteed order

Example:

Insert:

```text
Alice
Bob
Carlos
```

Iteration may not follow insertion order.

---

## 2. More Memory

HashMap stores:

* Key.
* Value.
* Hash information.

More overhead.

---

## 3. Not Designed for Sorting

Example:

"Show students alphabetically."

HashMap does not solve this.

---

# Solution: Use Multiple Collections

Professional applications often combine collections.

Example:

```java
List<Student> students;

Map<Integer,Student> studentsById;
```

---

Why?

List:

```text
Display
Reports
Ordering
```

Map:

```text
Fast lookup
```

---

# Real Example

Database:

```
STUDENTS TABLE

ID | NAME
---------
1  | Alice
2  | Bob
3  | Carlos
```

Application:

List:

```java
List<Student>
```

For:

```
Show all students
```

---

Map:

```java
Map<Integer,Student>
```

For:

```
Find student by ID
```

---

# Refactoring StudentService

A possible new design:

```java
public class StudentService {

    private Map<Integer, Student> students =
            new HashMap<>();

}
```

---

# New addStudent()

```java
public void addStudent(Student student){

    students.put(
        student.getId(),
        student
    );

}
```

---

# New findById()

```java
public Student findById(int id){

    return students.get(id);

}
```

---

# New removeStudent()

```java
public void removeStudent(int id){

    students.remove(id);

}
```

---

# New listStudents()

Problem:

Map is not a List.

We cannot:

```java
for(Student s : students)
```

---

We need:

```java
for(Student s : students.values()){

    System.out.println(s);

}
```

---

# Map Views

A Map provides:

## keys

```java
students.keySet();
```

Returns:

```text
1
2
3
```

---

## values

```java
students.values();
```

Returns:

```text
Alice
Bob
Carlos
```

---

## entries

```java
students.entrySet();
```

Returns:

```text
1 → Alice
2 → Bob
3 → Carlos
```

---

# Important Comparison

| Operation     | ArrayList | HashMap      |
| ------------- | --------- | ------------ |
| Search by ID  | O(n)      | O(1) average |
| Insert        | O(1) end  | O(1)         |
| Remove        | O(n)      | O(1) average |
| Keep order    | Yes       | No           |
| Memory        | Lower     | Higher       |
| Access by key | No        | Yes          |

---

# Design Decision

For our Student Management System:

If the main requirement is:

> "Find students quickly by ID"

Use:

```java
HashMap<Integer, Student>
```

---

If the main requirement is:

> "Maintain registration order"

Use:

```java
ArrayList<Student>
```

---

If we need both:

Use:

```java
ArrayList + HashMap
```

---

# Exercise Task

Create a second version:

```
StudentServiceMap
```

using:

```java
HashMap<Integer, Student>
```

Implement:

* addStudent()
* findById()
* removeStudent()
* listStudents()

Compare with the previous version.

---

# What We Learned

This exercise was not only about coding.

We learned:

* Collection choice depends on access patterns.
* ArrayList is excellent for ordered data.
* HashMap is excellent for lookup.
* Real systems often combine collections.
* Performance decisions are architectural decisions.

---

# ✔️ Next Step

In **Chapter 30 — Exercise 2: Product Inventory System (Part 1)** we will start the second exercise.

We will move from `List` to `Map` and build an inventory system using:

```java
HashMap<Integer, Product>
```

Features:

* Register products.
* Search by ID.
* Update stock.
* Remove products.

This will reinforce why Maps exist.
