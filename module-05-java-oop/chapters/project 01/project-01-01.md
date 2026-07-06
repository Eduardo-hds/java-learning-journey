# 💼 Project 1 — Student Management System

Welcome to your first complete Object-Oriented Programming project!

This project is intentionally simple, but it will be built using the same principles used in much larger applications.

Unlike the exercises from Chapter 7, this is a **real project** that will be developed step by step. We will not write everything at once. Instead, each stage will introduce new functionality while reinforcing the OOP concepts you've learned.

---

# 🎯 Project Goal

Build a console-based application capable of managing students.

By the end of the project, the application will be able to:

* Create students
* Store student information
* Display student information
* Manage multiple students
* Search for students
* Update student information
* Remove students
* Display all registered students

Everything will be done using only the Java concepts learned so far.

---

# 📚 Concepts Practiced

This project reinforces:

* Classes
* Objects
* Constructors
* Encapsulation
* Getters and setters
* Object interaction
* Package organization
* Clean code structure

---

# 📁 Project Structure

We will continue using the same project organization.

```text
src/
├── Main.java
├── model/
│   └── Student.java
├── service/
│   └── StudentManager.java
└── util/
```

Notice something new:

```
StudentManager
```

The **Student** class represents a student.

The **StudentManager** class manages many students.

This separation is extremely common in professional software.

---

# 🧠 Understanding Responsibilities

One of the most important ideas in OOP is that each class should have **one responsibility**.

## Student

Responsible for:

* Name
* Age
* Grade
* Displaying its own information

It should **NOT** know how to manage an entire collection of students.

---

## StudentManager

Responsible for:

* Storing students
* Adding students
* Removing students
* Searching students
* Listing students

It should **NOT** contain student-specific data like `name` or `grade`.

---

## Main

Responsible for:

* Starting the application
* Creating objects
* Calling methods

`Main` should never become a giant file full of business logic.

---

# 🏗️ Project Development Roadmap

We'll build the project in small stages.

## Stage 1

Create the project structure.

---

## Stage 2

Create the `Student` model.

---

## Stage 3

Create the `StudentManager`.

---

## Stage 4

Register students.

---

## Stage 5

Display all students.

---

## Stage 6

Search students.

---

## Stage 7

Update students.

---

## Stage 8

Remove students.

---

## Stage 9

Final cleanup and refactoring.

---

# 🚀 Stage 1 — Project Setup

Create the following structure:

```text
src/
├── Main.java
├── model/
│   └── Student.java
├── service/
│   └── StudentManager.java
└── util/
```

At this stage:

* `Student.java` can be an empty class.
* `StudentManager.java` can be an empty class.
* `Main.java` should simply print:

```text
===== Student Management System =====
```

Example:

```java
public class Main {

    public static void main(String[] args) {

        System.out.println("===== Student Management System =====");

    }

}
```

Expected output:

```text
===== Student Management System =====
```

---

# 💡 Why Start Small?

Many beginners try to build an entire application at once.

Professional developers don't.

Instead, they:

* Build a small piece.
* Test it.
* Make sure it works.
* Add the next feature.

This approach makes projects easier to understand, debug, and maintain.

---

# ✔️ Stage 1 Complete

Your project structure is now ready.

In the next stage, we'll create the **Student** class properly, adding:

* Private attributes
* Constructors
* Getters and setters
* Validation
* A `displayInformation()` method

This class will become the foundation of the entire application.

## ▶️ Next Step

Continue to **Project 1 — Stage 2: Building the `Student` Class**, where you'll implement the core model that every other part of the system will use.
