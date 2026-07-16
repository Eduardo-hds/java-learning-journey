# Chapter 27 — Exercise 1: Student Management System (Part 3)

In the previous chapter, we implemented:

* Adding students.
* Listing students.
* Searching by ID.

Now we will implement two more important operations:

1. Removing students.
2. Updating students.

During this process, we will learn an essential Collections concept:

> How Java decides whether two objects are the same.

This introduces:

```java
equals()
```

---

# Current StudentService

Currently:

```text
StudentService

+ addStudent()
+ listStudents()
+ findById()
```

We will add:

```text
+ removeStudent()
+ updateStudent()
```

---

# Part 1 — Removing Students

Requirement:

Remove a student using ID.

Example:

Before:

```text
[
 Student(1,"Alice"),
 Student(2,"Bob"),
 Student(3,"Carlos")
]
```

Remove:

```text
ID = 2
```

After:

```text
[
 Student(1,"Alice"),
 Student(3,"Carlos")
]
```

---

# First Approach — Search Then Remove

We could do:

```java
Student student = findById(id);

students.remove(student);
```

But there is a problem.

Let's analyze.

---

# How ArrayList.remove() Works

ArrayList has:

```java
remove(Object object)
```

It searches using:

```java
equals()
```

Example:

```java
students.remove(student);
```

Java asks:

> "Which object in the list is equal to this object?"

---

# The Problem With Objects

Imagine:

```java
Student a =
    new Student(1,"Alice",20,8.5);


Student b =
    new Student(1,"Alice",20,8.5);
```

Are they the same?

Memory:

```text
a ---> Student Object

b ---> Student Object
```

They are different objects.

By default:

```java
a.equals(b)
```

returns:

```text
false
```

---

# Why?

Because Object's default equals compares references.

Conceptually:

```java
this == other
```

Meaning:

> Are these the exact same object in memory?

---

# Solution: Override equals()

Our Student identity is:

```text
ID
```

Two students with the same ID represent the same student.

---

# Student.java

Add:

```java
@Override
public boolean equals(Object obj){

    if(this == obj){
        return true;
    }


    if(!(obj instanceof Student)){
        return false;
    }


    Student other = (Student) obj;


    return this.id == other.id;

}
```

---

# Breaking Down equals()

## Step 1

Same reference?

```java
this == obj
```

Example:

```java
student.equals(student)
```

Obviously true.

---

## Step 2

Wrong type?

```java
obj instanceof Student
```

Avoid:

```java
Student.equals(Product)
```

---

## Step 3

Compare IDs

```java
this.id == other.id
```

---

# hashCode()

Whenever we override:

```java
equals()
```

we should also override:

```java
hashCode()
```

Because collections like:

* HashSet
* HashMap

depend on both.

---

Add:

```java
@Override
public int hashCode(){

    return Integer.hashCode(id);

}
```

---

# Why hashCode Matters?

Rule:

If:

```java
a.equals(b)
```

is true,

then:

```java
a.hashCode()
```

must equal:

```java
b.hashCode()
```

---

# Now Remove Works

Example:

```java
Student student =
        findById(2);


students.remove(student);
```

ArrayList:

1. Searches.
2. Uses equals().
3. Removes matching element.

---

# Complexity

Removing from ArrayList:

Example:

```text
[A][B][C][D]
```

Remove B:

```text
[A][C][D]
```

C and D shift left.

Complexity:

```text
O(n)
```

---

# Implement removeStudent()

In:

```text
service/StudentService.java
```

Add:

```java
public void removeStudent(int id){

    Student student =
            findById(id);


    if(student != null){

        students.remove(student);

    }

}
```

---

# Testing

Before:

```text
Alice
Bob
Carlos
```

Execute:

```java
removeStudent(2);
```

After:

```text
Alice
Carlos
```

---

# Part 2 — Updating Students

Requirement:

Change student information.

Example:

Before:

```text
Bob
Age:21
Grade:8
```

Update:

```text
Grade:9
```

---

# How Do We Update?

With ArrayList:

We need:

1. Find object.
2. Change fields.

---

# First Problem

Our fields are private:

```java
private double grade;
```

We need controlled modification.

---

# Add Setters

Student.java:

```java
public void setAge(int age){

    this.age = age;

}


public void setGrade(double grade){

    this.grade = grade;

}
```

---

# Why Not Public Fields?

Wrong:

```java
student.grade = -100;
```

Setter allows validation later:

```java
public void setGrade(double grade){

    if(grade >= 0){

        this.grade = grade;

    }

}
```

---

# Implement updateStudent()

StudentService:

```java
public void updateStudent(
        int id,
        double newGrade){

    Student student =
            findById(id);


    if(student != null){

        student.setGrade(newGrade);

    }

}
```

---

# Testing

Before:

```text
Student{id=2, grade=8.0}
```

Execute:

```java
updateStudent(2,9.5);
```

After:

```text
Student{id=2, grade=9.5}
```

---

# Current StudentService

Now:

```text
StudentService

+ addStudent()
+ listStudents()
+ findById()
+ removeStudent()
+ updateStudent()
```

---

# Collections Concepts Practiced

## ArrayList operations

Added:

```text
add()
remove()
get()
```

---

## Searching

Complexity:

```text
O(n)
```

---

## Removing

Complexity:

```text
O(n)
```

---

## equals()

Used by:

```text
remove(Object)
contains()
```

---

## hashCode()

Required for:

```text
HashSet
HashMap
```

later.

---

# Important Design Lesson

The collection does not know your business rules.

ArrayList only knows:

> "I store objects."

Your class defines:

> "When are two students considered equal?"

That responsibility belongs to:

```java
equals()
```

---

# Exercise Task

Implement:

### Student.java

Add:

* `setAge()`
* `setGrade()`
* `equals()`
* `hashCode()`

---

### StudentService.java

Add:

* `removeStudent(int id)`
* `updateStudent(int id, double grade)`

---

Test:

1. Add 3 students.
2. Remove one.
3. Update one.
4. Print the list.

---

# ✔️ Next Step

In **Chapter 28 — Student Management System (Part 4)** we will improve this application by adding:

* Searching by name.
* Understanding `contains()`.
* Comparing `ArrayList` search with `HashMap`.
* Preparing the design transition from List-based storage to Map-based storage.
