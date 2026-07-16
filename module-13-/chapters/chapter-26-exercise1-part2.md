# Chapter 26 — Exercise 1: Student Management System (Part 2)

In the previous chapter, we created:

* `Student` model.
* `StudentService`.
* `ArrayList<Student>`.
* Adding students.
* Listing students.

Now we will implement one of the most common collection operations:

> Finding an object inside a collection.

We will build:

* Search by ID.
* Analyze the performance.
* Understand why searching in an `ArrayList` is different from searching in a `HashMap`.

---

# Current Structure

Our project:

```text id="6s8n2w"
src/
│
├── Main.java
│
├── model/
│   └── Student.java
│
├── service/
│   └── StudentService.java
│
└── util/
```

---

# New Requirement

The system needs:

```
Search student by ID
```

Example:

Input:

```text id="4m7q1d"
ID: 2
```

Output:

```text id="2g9k5x"
Student found:

ID: 2
Name: Bob
Age: 21
Grade: 9.0
```

---

# Step 1 — Understanding the Problem

Our collection:

```java id="7v0p4s"
List<Student> students;
```

contains:

```text id="n6k3q9"
[
 Student(1,"Alice"),
 Student(2,"Bob"),
 Student(3,"Carlos")
]
```

We need:

```text id="c9q7m2"
Find Student where id == 2
```

---

# Step 2 — Manual Search

Create in:

```text id="s1m8z3"
StudentService.java
```

Method:

```java id="u4n8q2"
public Student findById(int id){

    for(Student student : students){

        if(student.getId() == id){

            return student;

        }

    }

    return null;
}
```

---

# How This Works

Iteration:

First element:

```text id="b3m7p8"
Student id = 1
```

Comparison:

```java id="t5x9k1"
1 == 2?
```

False.

---

Second element:

```text id="p7q2m5"
Student id = 2
```

Comparison:

```java id="r4z8n0"
2 == 2?
```

True.

Return object.

---

# Step 3 — Testing

Main:

```java id="d5x8m3"
Student result =
        service.findById(2);


System.out.println(
        result.getName()
);
```

Output:

```text id="m8q4p6"
Bob
```

---

# What If Student Does Not Exist?

Example:

```java id="s6v2y9"
findById(99);
```

Nothing found.

The method returns:

```java id="f7m1x4"
null
```

---

# Handling Null

Better:

```java id="v9k3q5"
Student student =
        service.findById(99);


if(student != null){

    System.out.println(
        student.getName()
    );

}
else{

    System.out.println(
        "Student not found"
    );

}
```

---

# Performance Analysis

Now the important part.

How fast is this search?

---

# ArrayList Search Complexity

Our algorithm:

```java id="z5n7p2"
for each student
```

checks elements one by one.

Example:

100 students:

```text id="h2m9q4"
1
2
3
...
100
```

Worst case:

The student is last.

The program checks:

```text id="x7q3m8"
100 elements
```

---

Complexity:

```text id="k6v8r1"
O(n)
```

---

# Why O(n)?

Because the amount of work grows with the number of students.

10 students:

```text id="w4q9m2"
10 comparisons
```

10,000 students:

```text id="p3x8k5"
10,000 comparisons
```

---

# Alternative: HashMap

Imagine:

```java id="m7q2v9"
Map<Integer, Student> students;
```

Structure:

```text id="r5x1k8"
ID → Student
```

Example:

```text id="8m2q6w"
1 → Alice
2 → Bob
3 → Carlos
```

Search:

```java id="h3v9p0"
students.get(2);
```

Average:

```text id="q6x8m4"
O(1)
```

---

# Why Are We Not Using HashMap?

Because the exercise objective is:

Practice:

```text id="z1m5q8"
List
ArrayList
```

Later we will redesign this system using:

```text id="v4k7p2"
Map
```

and compare both approaches.

---

# Step 4 — Improve Student Display

Currently:

```java id="w8q3m1"
System.out.println(
    student.getName()
);
```

Output is limited.

Instead, override:

```java id="p9m4x6"
toString()
```

in `Student`.

---

# Student.java

Add:

```java id="d7k2m5"
@Override
public String toString(){

    return "Student{" +
            "id=" + id +
            ", name='" + name + '\'' +
            ", age=" + age +
            ", grade=" + grade +
            '}';

}
```

---

Now:

```java id="x5q8m3"
System.out.println(student);
```

automatically calls:

```java id="z8m1p4"
toString()
```

---

Output:

```text id="n2q7v5"
Student{id=2, name='Bob', age=21, grade=9.0}
```

---

# Why Is toString() Useful?

Without it:

```text id="c4m8z9"
model.Student@5e2de80c
```

Java only shows:

* Class name.
* Memory reference representation.

---

With it:

```text id="s7q1m4"
Readable object information.
```

---

# Step 5 — List All Students Better

Update:

```java id="r8m3x6"
public void listStudents(){

    for(Student student : students){

        System.out.println(student);

    }

}
```

---

Output:

```text id="p5x9k2"
Student{id=1, name='Alice', age=20, grade=8.5}

Student{id=2, name='Bob', age=21, grade=9.0}
```

---

# What Collection Concepts Were Used?

## ArrayList

Storage:

```text id="h7m2q5"
List<Student>
```

---

## Iterable

Traversal:

```java id="m8x3q1"
for(Student s : students)
```

---

## Generics

Type safety:

```java id="y5q9v4"
ArrayList<Student>
```

---

## Object comparison

Manual comparison:

```java id="z3m7p8"
student.getId() == id
```

---

# Current StudentService

Capabilities:

```text id="w2q8m5"
StudentService

+ addStudent()
+ listStudents()
+ findById()
```

---

# Exercise Task

Implement:

1. `findById()` method.
2. Improve `Student.toString()`.
3. Test:

   * Existing student.
   * Non-existing student.

Example:

Search:

```text id="m3v8q2"
ID 2
```

Should return:

```text id="x7p5k1"
Bob
```

Search:

```text id="k9m2x6"
ID 99
```

Should show:

```text id="q4v8m1"
Student not found
```

---

# ✔️ Next Step

In **Chapter 27 — Student Management System (Part 3)** we will implement:

* Removing students.
* Updating students.
* Why removing from `ArrayList` costs `O(n)`.
* The importance of `equals()` when working with collections.
