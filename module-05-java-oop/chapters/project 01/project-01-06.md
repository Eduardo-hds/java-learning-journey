# 💼 Project 1 — Stage 6: Updating Students

Your Student Management System can now:

* ✅ Create students
* ✅ Store students
* ✅ List all students
* ✅ Search students by name

The next logical feature is the ability to **update existing student information**.

Imagine that a student's grade changes after a new exam, or their age needs to be corrected.

Instead of creating a new student, we should modify the existing object.

---

# 🎯 Stage Goal

Implement the ability to update a student's information.

By the end of this stage, your application will be able to:

* Find a student by name
* Modify one or more attributes
* Keep all validation rules
* Display the updated information

---

# 📁 Project Structure

```text id="p1-stage6-structure"
src/
├── Main.java
├── model/
│   └── Student.java
├── service/
│   └── StudentManager.java
└── util/
```

Both `StudentManager` and `Main` will be updated.

---

# 🧠 Designing the Update Feature

A common beginner question is:

> Should we create a method like `updateStudent()` inside the `Student` class?

The answer is **no**.

The `Student` object already provides setters:

```java
student.setName(...);
student.setAge(...);
student.setGrade(...);
```

Those methods already perform validation.

The manager's job is simply to **find the correct student** and ask it to update itself.

---

# 🏗️ Step 1 — Reuse the Search Method

One of the biggest advantages of OOP is **code reuse**.

Instead of searching through the array again, reuse:

```java
findStudentByName(String name)
```

Example:

```java
Student student = findStudentByName(name);
```

This avoids duplicated code.

---

# 🏗️ Step 2 — Create the Update Method

Inside `StudentManager`, create:

```java
public boolean updateStudent(
    String currentName,
    String newName,
    int newAge,
    double newGrade
)
```

Why return a `boolean`?

Because the update has two possible outcomes:

* `true` → student updated successfully.
* `false` → student not found.

Returning a boolean allows `Main` to decide what message should be displayed.

---

# 🏗️ Step 3 — Find the Student

Inside the method:

```java
Student student = findStudentByName(currentName);
```

If the result is `null`:

```text
Return false.
```

Otherwise, continue.

---

# 🏗️ Step 4 — Update the Object

Use the setters:

```java
student.setName(newName);

student.setAge(newAge);

student.setGrade(newGrade);
```

Notice that `StudentManager` is **not** modifying the attributes directly.

It communicates with the object through its public methods.

This respects encapsulation.

---

# 🏗️ Step 5 — Return Success

After updating:

```java
return true;
```

The manager reports that the operation succeeded.

---

# 🧠 Why Use Setters Instead of Direct Access?

Imagine someone tries to update the grade:

```text
15
```

This is invalid.

The setter already contains validation.

```java
student.setGrade(15);
```

The object protects itself.

If we modified the field directly:

```java
student.grade = 15;
```

the object could become invalid.

Encapsulation continues to protect our data.

---

# 🧪 Testing

Suppose we have:

```text
John
Age: 20
Grade: 8.5
```

Update:

```text
Name : John

New Age : 21

New Grade : 9.4
```

Call:

```java
boolean updated =
    manager.updateStudent(
        "John",
        "John",
        21,
        9.4
    );
```

If successful:

```text
Student updated successfully.
```

Then:

```java
manager.listStudents();
```

Expected output:

```text
-------------------------
Student Information
-------------------------
Name : John
Age  : 21
Grade: 9.4
-------------------------
```

---

# 🧠 Internal Execution

Conceptually, Java performs the following steps:

```text
Main

↓

updateStudent()

↓

findStudentByName()

↓

Student found

↓

setName()

↓

setAge()

↓

setGrade()

↓

Return true
```

Notice how responsibilities remain separated.

---

# 💡 Design Principle

The update operation demonstrates excellent object-oriented design.

### Student

Responsible for:

* Storing valid data
* Validating changes
* Protecting its own state

---

### StudentManager

Responsible for:

* Finding students
* Coordinating the update

---

### Main

Responsible for:

* Requesting the update
* Showing the result

Each class performs exactly one role.

---

# 🚀 Why This Design Scales Well

Imagine adding more validation later.

For example:

* Grades must have only one decimal place.
* Age cannot exceed 120.
* Names must have at least two characters.

Where should these rules go?

Inside `Student`.

The manager doesn't need to change at all.

This is one of the greatest benefits of encapsulation: business rules stay close to the data they protect.

---

# 🏗️ Current Project Architecture

```text
               Main
                 │
                 ▼
        StudentManager
         │      │
         │      ▼
         │  findStudentByName()
         │
         ▼
     Student
   ├── setName()
   ├── setAge()
   └── setGrade()
```

Objects communicate through methods instead of directly manipulating each other's data.

---

# ✔️ Stage 6 Complete

Excellent work!

Your Student Management System now supports:

* ✅ Creating students
* ✅ Storing students
* ✅ Listing students
* ✅ Searching students
* ✅ Updating student information

More importantly, you've learned how to reuse existing methods instead of duplicating logic and how encapsulation naturally protects your objects during updates.

## ▶️ Next Step

Continue to **Project 1 — Stage 7: Removing Students**, where you'll implement the ability to delete students from the system, reorganize the internal array, and maintain a consistent collection without leaving empty gaps.
