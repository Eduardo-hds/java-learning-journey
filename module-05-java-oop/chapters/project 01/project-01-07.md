# 💼 Project 1 — Stage 7: Removing Students

Your Student Management System is almost complete.

Current features:

* ✅ Create students
* ✅ Store students
* ✅ List all students
* ✅ Search students
* ✅ Update students

The final core feature of any management system is the ability to **remove** data.

However, removing an element from an array is not as simple as setting it to `null`.

In this stage, you'll learn how to properly remove an object while keeping the array organized.

---

# 🎯 Stage Goal

Implement the ability to remove a student by name.

By the end of this stage, your application will be able to:

* Search for a student
* Remove the student from the array
* Shift the remaining students to fill the gap
* Update the student count
* Keep the array organized

---

# 📁 Project Structure

```text id="p1-stage7-structure"
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

# 🧠 Why Can't We Simply Set the Element to `null`?

Suppose our array looks like this:

```text id="before-remove"
Index

0 → John
1 → Sarah
2 → Michael
3 → Emma
```

If we remove Sarah like this:

```java
students[1] = null;
```

The array becomes:

```text id="after-null"
Index

0 → John
1 → null
2 → Michael
3 → Emma
```

Now there is a gap.

When listing students, you'll either:

* Need extra checks for `null`
* Or risk a `NullPointerException`

The collection becomes inconsistent.

---

# 🧠 The Correct Approach

Instead of leaving an empty position, move every student after the removed one one position to the left.

Example:

Before:

```text id="shift-before"
0 → John
1 → Sarah
2 → Michael
3 → Emma
```

Remove Sarah:

```text id="shift-after"
0 → John
1 → Michael
2 → Emma
3 → null
```

Finally:

```text id="count-after"
studentCount--;
```

Now the array remains compact.

---

# 🏗️ Step 1 — Create the Method

Inside `StudentManager`, create:

```java id="remove-method"
public boolean removeStudent(String name)
```

Return:

* `true` if the student was removed.
* `false` if no matching student exists.

---

# 🏗️ Step 2 — Find the Student's Position

Notice something important.

To remove an element from an array, you need its **index**, not just the object.

Loop through the registered students:

```text id="loop"
0

↓

1

↓

2

↓

...

↓

studentCount - 1
```

For each student:

```java
students[i].getName().equalsIgnoreCase(name)
```

If the names match:

You found the position to remove.

---

# 🏗️ Step 3 — Shift the Elements

Suppose the student is at index `i`.

Move every remaining element one position to the left.

Conceptually:

```text id="shift-logic"
students[i] = students[i + 1]

students[i + 1] = students[i + 2]

...

Until the last registered student
```

This closes the gap left by the removed student.

---

# 🏗️ Step 4 — Clear the Last Position

After shifting:

The last valid object now exists twice.

Example:

Before clearing:

```text id="duplicate"
0 → John
1 → Michael
2 → Emma
3 → Emma
```

Clear the last position:

```java
students[studentCount - 1] = null;
```

Now:

```text id="clean"
0 → John
1 → Michael
2 → Emma
3 → null
```

This removes the duplicate reference and allows Java's Garbage Collector to reclaim the removed object if nothing else references it.

---

# 🏗️ Step 5 — Update the Counter

Decrease the number of registered students.

```java
studentCount--;
```

This tells the manager that one less student is stored.

---

# 🏗️ Step 6 — Return the Result

If a student was removed:

```java
return true;
```

If the entire array was searched without a match:

```java
return false;
```

---

# 🧪 Testing

Current students:

```text id="students-before"
John

Sarah

Michael

Emma
```

Call:

```java
boolean removed =
    manager.removeStudent("Sarah");
```

Expected result:

```text id="removed-msg"
Student removed successfully.
```

List the students:

```text id="students-after"
John

Michael

Emma
```

Sarah no longer appears, and there are no empty gaps.

---

# 🧠 Internal Execution

Conceptually, Java performs:

```text id="flow"
Find Sarah

↓

Shift Michael

↓

Shift Emma

↓

Clear last position

↓

Decrease studentCount

↓

Return true
```

---

# ⚠️ Common Beginner Mistakes

## Forgetting to Shift

Incorrect:

```java
students[i] = null;
```

Result:

```text id="gap"
John

null

Michael
```

---

## Forgetting to Decrease `studentCount`

Even after removing a student:

```text id="count"
studentCount

↓

Still 4
```

Now the manager believes there are four students when there are only three.

---

## Forgetting to Clear the Last Position

After shifting:

```text id="duplicate2"
John

Michael

Emma

Emma
```

The last reference must be set to `null`.

---

# 💡 Design Principle

Notice how responsibilities remain unchanged.

### Student

Responsible for:

* Representing one student
* Protecting its own data

---

### StudentManager

Responsible for:

* Managing the student collection
* Adding
* Listing
* Searching
* Updating
* Removing

---

### Main

Responsible for:

* Calling the appropriate operations
* Displaying results to the user

Each class still has one clear responsibility.

---

# 🏗️ Current Project Architecture

```text id="architecture"
               Main
                 │
                 ▼
        StudentManager
     ├── addStudent()
     ├── listStudents()
     ├── findStudentByName()
     ├── updateStudent()
     └── removeStudent()
                 │
                 ▼
             Student
```

At this point, the manager provides the complete set of CRUD operations:

* **Create**
* **Read**
* **Update**
* **Delete**

These four operations are the foundation of countless real-world software systems.

---

# ✔️ Project 1 Complete 🎉

Congratulations!

You have successfully built your first complete Object-Oriented Java application.

Throughout this project, you applied every major concept introduced in this module:

* Classes and objects
* Constructors
* Encapsulation
* Getters and setters
* The `this` keyword
* Package organization
* Object interaction
* Separation of responsibilities
* CRUD operations
* Array management

More importantly, you learned how to think in terms of **objects collaborating together**, rather than writing all your logic inside `main()`.

This mindset is what distinguishes Object-Oriented Programming from procedural programming.

## ▶️ Next Step

Continue to **Project 2 — Bank System**, where you'll build a more realistic application focused on business rules, account operations, and stronger encapsulation, reinforcing everything you've learned while introducing more complex object interactions.
