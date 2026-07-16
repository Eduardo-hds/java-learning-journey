# Chapter 25 — Exercise 1: Student Management System (Part 1)

Now we begin the practical part of the module.

The objective is not only to practice `ArrayList`.

The goal is to apply the design principles learned:

* Collections store groups of objects.
* Models represent data.
* Services contain business logic.
* Main only controls application flow.

We will build this project progressively.

---

# Project Objective

Create a console application that manages students.

The system should allow:

* Register students.
* List students.
* Search students.
* Update student information.
* Remove students.

---

# Requirements

The application must use:

```java
ArrayList<Student>
```

The student data:

```text
ID
Name
Age
Grade
```

Example:

```text
Student
----------------
ID: 1
Name: Alice
Age: 20
Grade: 8.5
```

---

# Step 1 — Project Structure

Inside our module project:

```text
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

# Why Separate These Packages?

## model

Contains:

> What the object is.

Example:

```text
Student
Product
Employee
```

---

## service

Contains:

> What the application does.

Example:

```text
registerStudent()
removeStudent()
searchStudent()
```

---

## Main

Contains:

> Program entry point.

It should not contain business logic.

---

# Step 2 — Create Student Class

Location:

```text
model/Student.java
```

The class represents the entity.

Initial version:

```java
public class Student {

    private int id;
    private String name;
    private int age;
    private double grade;

}
```

---

# Why Private Fields?

Because objects should control their own data.

Wrong:

```java
student.grade = -50;
```

We do not want invalid values.

---

# Step 3 — Constructor

We need a way to create students.

Example:

```java
Student student =
    new Student(
        1,
        "Alice",
        20,
        8.5
    );
```

So:

```java
public Student(
        int id,
        String name,
        int age,
        double grade){

    this.id = id;
    this.name = name;
    this.age = age;
    this.grade = grade;

}
```

---

# Step 4 — Getters

The service will need access to student information.

Create:

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
public int getAge(){
    return age;
}
```

---

```java
public double getGrade(){
    return grade;
}
```

---

# Why Not Public Fields?

Compare:

## Public

```java
student.grade = -10;
```

Anyone can change anything.

---

## Getter

```java
student.getGrade();
```

The object controls access.

---

# Step 5 — Create StudentService

Location:

```text
service/StudentService.java
```

The service manages students.

---

Create the collection:

```java
private List<Student> students =
        new ArrayList<>();
```

---

# Why List Instead of ArrayList?

Important design habit.

Prefer:

```java
List<Student>
```

instead of:

```java
ArrayList<Student>
```

because the variable represents the behavior we need:

> A list of students.

The implementation can change later.

Example:

```java
List<Student> students =
        new LinkedList<>();
```

would still work.

---

# Step 6 — Add Student

Create method:

```java
public void addStudent(Student student){

    students.add(student);

}
```

---

Usage:

```java
service.addStudent(student);
```

---

# What Happens Internally?

ArrayList:

Before:

```text
[]
```

Add:

```java
students.add(student);
```

After:

```text
[Student]
```

---

# ArrayList Complexity

Adding at the end:

Average:

```text
O(1)
```

because it places the reference in the next available position.

---

# Step 7 — List Students

Create:

```java
public void listStudents(){

    for(Student student : students){

        System.out.println(
            student.getName()
        );

    }

}
```

---

# What Collection Concept Are We Practicing?

Here we apply:

```text
Iterable
Iterator
ArrayList traversal
```

The enhanced for loop internally uses:

```java
Iterator
```

---

# Step 8 — Test From Main

Main:

```java
public class Main {

    public static void main(String[] args){

        StudentService service =
                new StudentService();


        Student student =
                new Student(
                    1,
                    "Alice",
                    20,
                    8.5
                );


        service.addStudent(student);


        service.listStudents();

    }

}
```

---

Expected output:

```text
Alice
```

---

# Current Application Flow

```text
Main

 |
 |
 v

StudentService

 |
 |
 v

ArrayList<Student>

 |
 |
 v

Student objects
```

---

# What We Have Learned

This exercise already uses:

✅ Collections Framework
✅ List interface
✅ ArrayList
✅ Generics
✅ Iterable concept
✅ Package organization
✅ Separation of responsibilities

---

# Next Implementation Steps

We still need:

1. Search student by ID.
2. Remove student.
3. Update student.
4. Improve displaying.
5. Handle cases where student does not exist.

---

# Exercise Task Before Continuing

Create the current structure:

```text
model/
    Student.java

service/
    StudentService.java

Main.java
```

Implement:

* Student class.
* Constructor.
* Getters.
* StudentService.
* addStudent().
* listStudents().

Do not implement search/remove/update yet.

---

# ✔️ Next Step

In **Chapter 26 — Student Management System (Part 2)** we will implement searching with `ArrayList`, analyze the cost of searching (`O(n)`), and compare manual search versus collection methods like `contains()`.
