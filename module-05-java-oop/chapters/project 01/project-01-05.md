# 💼 Project 1 — Stage 5: Searching Students

Your Student Management System is becoming more useful.

Current features:

* ✅ Create students
* ✅ Store students
* ✅ Display all students

However, imagine having 500 students.

Would you scroll through the entire list just to find one student?

Of course not.

A management system should allow users to search for specific information quickly.

---

# 🎯 Stage Goal

Implement the ability to search for a student by name.

By the end of this stage, your application will be able to:

* Receive a student's name
* Search through the registered students
* Return the matching student
* Inform the user if no student is found

---

# 📁 Project Structure

```text id="p1-stage5-structure"
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

# 🧠 Designing the Search

Where should the search logic be?

### Option 1

Inside `Student`

```text id="wrong-design"
Student

↓

searchStudent()
```

This doesn't make sense.

A single student cannot search through all other students.

---

### Option 2

Inside `StudentManager`

```text id="correct-design"
StudentManager

↓

searchStudent()
```

This is correct.

The manager owns the collection of students, so it is responsible for searching it.

---

# 🏗️ Step 1 — Create the Method

Inside `StudentManager`, create:

```java id="search-method"
public Student findStudentByName(String name)
```

Notice the return type.

We are returning a **Student object**, not just printing information.

Why?

Because returning the object makes the method much more flexible.

The caller can decide what to do with it.

---

# 🧠 Why Return the Object?

Imagine this method only printed the student.

Later you might want to:

* Update the student's grade
* Remove the student
* Check the student's age

You would have to search again.

Instead, returning the object allows reuse.

Example:

```java id="returned-object"
Student student = manager.findStudentByName("John");
```

Now you have direct access to that object.

---

# 🏗️ Step 2 — Search Through the Array

Loop only through:

```java id="student-count"
studentCount
```

For each student:

Compare the stored name with the requested name.

Example:

```java id="comparison"
student.getName().equalsIgnoreCase(name)
```

Why `equalsIgnoreCase()`?

Because:

```text id="comparison-example"
John

john

JOHN
```

should all be considered the same name.

---

# 🏗️ Step 3 — Return the Student

When a match is found:

```text id="return-logic"
Return the Student object immediately.
```

The search ends as soon as the first match is found.

There is no need to continue searching.

---

# 🏗️ Step 4 — Return `null`

If the loop finishes without finding anyone:

```java id="return-null"
return null;
```

This tells the caller:

> "No matching student exists."

---

# 🧠 What Does `null` Mean?

`null` means:

> There is no object.

For example:

```java id="null-example"
Student student = manager.findStudentByName("Peter");
```

If Peter doesn't exist:

```text id="null-result"
student

↓

null
```

The variable exists, but it doesn't reference any object.

---

# 🏗️ Step 5 — Use the Search

In `Main.java`:

```java id="main-search"
Student foundStudent =
    manager.findStudentByName("Sarah");
```

Always verify the result.

Example logic:

```text id="if-logic"
If student exists

    Display information

Else

    Print

    Student not found.
```

Never assume a search always succeeds.

---

# ⚠️ Why Is the Null Check Important?

Suppose you write:

```java id="wrong-null"
Student student =
    manager.findStudentByName("Peter");

student.displayInformation();
```

If Peter doesn't exist:

```text id="null-pointer"
student

↓

null
```

Java will throw:

```text id="exception"
NullPointerException
```

Always check first.

---

# 🧪 Testing

Create several students.

```java id="students"
manager.addStudent(new Student("John", 20, 9.5));
manager.addStudent(new Student("Sarah", 22, 8.8));
manager.addStudent(new Student("Michael", 19, 7.6));
```

Search:

```java id="search"
Student student =
    manager.findStudentByName("Sarah");
```

Expected output:

```text id="found"
Student found!

-------------------------
Student Information
-------------------------
Name : Sarah
Age  : 22
Grade: 8.8
-------------------------
```

Now search for:

```text id="missing"
Emily
```

Expected:

```text id="not-found"
Student not found.
```

---

# 🧠 Internal Execution

When searching for:

```text id="search-name"
Sarah
```

Java performs something conceptually like this:

```text id="execution-flow"
John

↓

Not a match

↓

Sarah

↓

Match found

↓

Return object

↓

Search ends
```

The remaining students are never checked.

This makes the search more efficient.

---

# 💡 Design Principle

Notice that responsibilities are still perfectly separated.

### Student

Responsible for:

* Holding student data
* Displaying student information

---

### StudentManager

Responsible for:

* Storing students
* Listing students
* Searching students

---

### Main

Responsible for:

* Calling the search
* Handling the returned result
* Deciding what to display

This separation keeps the code easy to understand and extend.

---

# 🚀 Looking Ahead

Right now, searching is useful by itself.

But it will become even more valuable in the next stages.

Why?

Because both updating and removing a student require finding the correct student first.

Instead of rewriting the search logic, you'll reuse the method you just created.

This is a perfect example of code reuse in Object-Oriented Programming.

---

# ✔️ Stage 5 Complete

Excellent!

Your Student Management System can now:

* Create students
* Store students
* Display all students
* Search students by name

You have also learned an important design technique: returning objects instead of printing inside methods, making your code more reusable and flexible.

## ▶️ Next Step

Continue to **Project 1 — Stage 6: Updating Students**, where you'll use the search functionality to modify existing student information while maintaining encapsulation and keeping object responsibilities properly separated.
