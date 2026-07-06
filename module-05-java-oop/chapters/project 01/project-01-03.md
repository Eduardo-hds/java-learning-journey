# 💼 Project 1 — Stage 3: Building the `StudentManager` Class

Until now, our application can create individual `Student` objects.

However, a real management system needs to handle **multiple students**.

Should the `Student` class be responsible for storing other students?

**No.**

This would violate one of the most important principles of Object-Oriented Programming:

> **A class should have one single responsibility.**

This is why we're introducing a new class:

**`StudentManager`**

---

# 🎯 Stage Goal

By the end of this stage, the application will have a class responsible for:

* Storing students
* Adding new students
* Providing access to the student collection

For now, we are **not** searching, updating, or removing students. We'll implement those features in later stages.

---

# 📁 Project Structure

```text id="p1-stage3-structure"
src/
├── Main.java
├── model/
│   └── Student.java
├── service/
│   └── StudentManager.java
└── util/
```

In this stage, we will implement **StudentManager.java**.

---

# 🧠 Why Create a Manager Class?

Imagine putting everything inside `Student`.

```text
Student
├── name
├── age
├── grade
├── addStudent()
├── removeStudent()
├── searchStudent()
├── updateStudent()
├── listStudents()
```

This doesn't make sense.

A single student should not know how to manage all students in the system.

Instead:

```text
Student
├── name
├── age
├── grade
└── displayInformation()

StudentManager
├── addStudent()
├── listStudents()
├── searchStudent()
├── removeStudent()
```

Each class has one responsibility.

---

# 🏗️ Step 1 — Create the Student Collection

Since we haven't learned collections like `ArrayList` yet, we'll use an array.

Inside `StudentManager`:

```java id="p1-stage3-array"
private Student[] students;
private int studentCount;
```

### Why two variables?

The array stores the students.

```java
students
```

The counter keeps track of how many students are actually stored.

```java
studentCount
```

Remember:

If the array has a size of 100, it doesn't mean there are 100 students.

The counter tells us how many positions are currently in use.

---

# 🏗️ Step 2 — Create the Constructor

Initialize the array.

Example:

```java id="p1-stage3-constructor"
public StudentManager() {
    students = new Student[100];
    studentCount = 0;
}
```

This means:

* Maximum of 100 students
* Initially, zero students are registered

---

# 🏗️ Step 3 — Create `addStudent()`

Create a method:

```java
public void addStudent(Student student)
```

Responsibilities:

* Check if there is space in the array.
* Store the student.
* Increase `studentCount`.
* Print a success message.

Pseudo-code:

```text
If studentCount < students.length

    Store the student

    Increase studentCount

    Print:
    Student added successfully.

Else

    Print:
    Student list is full.
```

---

# 🧠 How Does This Work?

Suppose the array has five positions.

Initially:

```text
Index

0 -> null
1 -> null
2 -> null
3 -> null
4 -> null
```

After adding John:

```text
0 -> John
1 -> null
2 -> null
3 -> null
4 -> null
```

`studentCount`

```text
1
```

After adding Sarah:

```text
0 -> John
1 -> Sarah
2 -> null
3 -> null
4 -> null
```

`studentCount`

```text
2
```

Notice that we always insert at the next available position.

---

# 🏗️ Step 4 — Create `getStudentCount()`

Create a getter for the number of registered students.

```java
public int getStudentCount()
```

This allows other classes to know how many students have been added without directly accessing the private field.

---

# 🧪 Testing the Manager

Update `Main.java`.

Create the manager:

```java id="p1-stage3-main1"
StudentManager manager = new StudentManager();
```

Create two students:

```java id="p1-stage3-main2"
Student student1 = new Student("John", 20, 9.5);

Student student2 = new Student("Sarah", 22, 8.8);
```

Add them:

```java id="p1-stage3-main3"
manager.addStudent(student1);

manager.addStudent(student2);
```

Print the total:

```java id="p1-stage3-main4"
System.out.println(
    "Students registered: " +
    manager.getStudentCount()
);
```

Expected output:

```text
Student added successfully.

Student added successfully.

Students registered: 2
```

---

# 💡 Why Doesn't `Main` Store the Array?

A beginner might write:

```java
Student[] students = new Student[100];
```

inside `Main.java`.

This works for tiny programs, but it quickly becomes messy.

Instead:

* `Main` starts the application.
* `StudentManager` manages students.
* `Student` represents a student.

Each class has a clear responsibility.

---

# 🧠 Professional Insight

This design follows a principle known as **Separation of Responsibilities**.

Each class should answer one question:

**Student**

> "Who am I?"

**StudentManager**

> "How do I manage students?"

**Main**

> "How do I start and coordinate the application?"

Keeping these responsibilities separate makes software much easier to expand and maintain.

---

# 🏗️ Current Project Architecture

```text
               Main
                 │
                 ▼
        StudentManager
                 │
      ┌──────────┴──────────┐
      ▼                     ▼
 Student               Student
```

`Main` communicates with `StudentManager`.

`StudentManager` communicates with many `Student` objects.

The `Student` objects do not know about each other.

---

# ✔️ Stage 3 Complete

Excellent work!

Your application now has a proper object-oriented structure:

* `Student` represents one student.
* `StudentManager` manages many students.
* `Main` coordinates the application.

This separation of responsibilities is a fundamental principle you'll continue using throughout your Java journey.

## ▶️ Next Step

Continue to **Project 1 — Stage 4: Listing Students**, where you'll implement the first real management feature by displaying every registered student using the data stored inside `StudentManager`.
