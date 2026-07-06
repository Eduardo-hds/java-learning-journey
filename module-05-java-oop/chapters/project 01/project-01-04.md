# 💼 Project 1 — Stage 4: Listing Students

Our application can now:

* Create `Student` objects
* Store them inside `StudentManager`

However, there is still a problem.

Once a student is added, we have no way to see the registered students.

A management system isn't very useful if it can't display its data.

In this stage, we'll solve that problem.

---

# 🎯 Stage Goal

Implement the ability to display **all registered students**.

By the end of this stage, `StudentManager` will be able to:

* Check if there are registered students
* Iterate through the student array
* Display each student's information

---

# 📁 Project Structure

```text id="p1-stage4-structure"
src/
├── Main.java
├── model/
│   └── Student.java
├── service/
│   └── StudentManager.java
└── util/
```

Only `StudentManager` and `Main` will be updated.

---

# 🏗️ Step 1 — Create `listStudents()`

Inside `StudentManager`, create the method:

```java id="p1-stage4-method"
public void listStudents()
```

This method is responsible for displaying every registered student.

Notice something important:

It **does not** print the student's information itself.

Instead, it asks each `Student` object to display its own information.

This is object interaction.

---

# 🧠 Why Is This Better?

Imagine writing this inside `StudentManager`:

```java id="bad-example"
System.out.println(student.getName());
System.out.println(student.getAge());
System.out.println(student.getGrade());
```

Now `StudentManager` is responsible for formatting student information.

But that's already the responsibility of the `Student` class.

Instead:

```java id="good-example"
student.displayInformation();
```

Each object knows how to present itself.

This keeps responsibilities separated.

---

# 🏗️ Step 2 — Check if the List is Empty

Before looping through the array, verify if any students exist.

Example logic:

```text id="empty-logic"
If studentCount == 0

    Print:
    No students registered.

    Stop the method.
```

Why?

Because there's no point looping through an empty array.

---

# 🏗️ Step 3 — Loop Through the Students

Loop only through the registered students.

Not through the entire array.

Example:

```text id="loop-logic"
From index 0

Until studentCount - 1

    Display each student
```

Remember:

The array may have a capacity of 100 students, but only the first `studentCount` positions are valid.

---

# 🧠 Why Not Loop Through `students.length`?

Suppose your array looks like this:

```text id="array-example"
Index

0 → John
1 → Sarah
2 → Michael
3 → null
4 → null
5 → null
...
99 → null
```

If you loop through the entire array:

```java id="wrong-loop"
for (int i = 0; i < students.length; i++)
```

Eventually you'll try to access:

```text id="null-example"
students[3]
```

which is:

```text id="null-value"
null
```

Trying to call:

```java id="null-call"
students[3].displayInformation();
```

would cause a:

```text id="exception"
NullPointerException
```

Always loop until:

```java id="correct-loop"
studentCount
```

not

```java id="wrong-length"
students.length
```

---

# 🏗️ Step 4 — Display a Header

Before displaying students, print a simple header.

Example:

```text id="header"
========== Registered Students ==========
```

This makes the output much easier to read.

---

# 🏗️ Step 5 — Display Each Student

Inside the loop:

```text id="display-logic"
Get the student

Call

displayInformation()
```

Notice the communication:

```text id="interaction"
StudentManager

↓

Student
```

The manager doesn't know how the student prints itself.

It simply asks the object to do its job.

This is one of the biggest ideas in Object-Oriented Programming.

---

# 🧪 Testing

Update `Main.java`.

Create several students.

Example:

```java id="main-create"
Student student1 = new Student("John", 20, 9.5);
Student student2 = new Student("Sarah", 22, 8.8);
Student student3 = new Student("Michael", 19, 7.6);
```

Add them:

```java id="main-add"
manager.addStudent(student1);
manager.addStudent(student2);
manager.addStudent(student3);
```

Finally:

```java id="main-list"
manager.listStudents();
```

Example output:

```text id="expected-output"
========== Registered Students ==========

-------------------------
Student Information
-------------------------
Name : John
Age  : 20
Grade: 9.5
-------------------------

-------------------------
Student Information
-------------------------
Name : Sarah
Age  : 22
Grade: 8.8
-------------------------

-------------------------
Student Information
-------------------------
Name : Michael
Age  : 19
Grade: 7.6
-------------------------
```

---

# 🧠 Internal Execution

When you call:

```java id="execution"
manager.listStudents();
```

Java performs something conceptually like this:

```text id="flow"
StudentManager

↓

Student #1
displayInformation()

↓

Student #2
displayInformation()

↓

Student #3
displayInformation()
```

Each object prints its own information.

The manager simply coordinates the process.

---

# 💡 Design Principle

Notice how responsibilities remain separated:

### Student

Responsible for:

* Storing student data
* Displaying student information

---

### StudentManager

Responsible for:

* Managing the collection
* Deciding which students to display

---

### Main

Responsible for:

* Creating the manager
* Creating students
* Calling the manager

Nobody is doing someone else's job.

This is exactly what good object-oriented design looks like.

---

# ✔️ Stage 4 Complete

Excellent!

Your application can now:

* Create students
* Store multiple students
* Display every registered student

For the first time, your project behaves like a real management system instead of a collection of independent objects.

## ▶️ Next Step

Continue to **Project 1 — Stage 5: Searching Students**, where you'll implement the ability to find a student by name, introducing searching algorithms and object retrieval while keeping the application's responsibilities clean and well organized.
