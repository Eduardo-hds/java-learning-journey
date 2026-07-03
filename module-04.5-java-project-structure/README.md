# Chapter 4.5 — Java Project Structure & File Organization

This chapter is about something that most beginners ignore at first — but every professional Java developer uses every day: **how to organize code properly across files and folders**.

Even if your code “works” in a single file, real Java projects are always split into multiple files with a clear structure.

---

# 1. Project Structure Fundamentals

A standard Java project is organized like this:

```text
src/
 ├── Main.java
 ├── model/
 ├── service/
 └── util/
```

## What is `src`?

`src` stands for **source**.

It is the folder where all your Java code lives.

When you compile a project, Java only looks inside `src`.

---

## What are packages?

Packages are just **folders inside `src` that organize classes by purpose**.

Example:

* `model/` → data classes (Student, Product, Car)
* `service/` → logic classes (bank rules, calculations, operations)
* `util/` → helper tools (formatters, small reusable functions)

Think of packages as:

> “Labels that tell Java and developers where each class belongs.”

---

## Why we separate code into folders

Without structure:

* Everything becomes hard to find
* Code becomes messy fast
* Collaboration becomes impossible

With structure:

* Each class has a clear responsibility
* Code becomes scalable
* Projects look professional

---

# 2. File Organization Rules

## Rule 1 — One class per file

```text
Student.java → only Student class
Product.java → only Product class
```

---

## Rule 2 — File name must match class name

```java
public class Student {}
```

Must be saved as:

```text
Student.java
```

---

## Rule 3 — Main class is the entry point

Your program always starts here:

```java
public class Main {
    public static void main(String[] args) {
    }
}
```

`Main` should stay clean — only starting the program, not containing all logic.

---

## Rule 4 — Do NOT mix everything in Main

Bad practice:

```java
// everything inside Main
```

Good practice:

```text
Main → starts program
Other classes → do the work
```

---

# 3. Recommended Project Structure

We will use this structure throughout the bootcamp:

```text
src/
 ├── Main.java
 ├── model/
 │    ├── Student.java
 │    ├── Product.java
 │    └── Car.java
 ├── service/
 │    └── BankAccount.java
 ├── util/
 │    └── Helper.java
```

---

## What goes where?

### model/

Holds simple data structures:

* Student
* Product
* Car

👉 Purpose: represent “things”

---

### service/

Holds logic and operations:

* BankAccount
* Payment processing
* Calculations

👉 Purpose: “do things”

---

### util/

Holds reusable tools:

* formatting
* validations
* helper methods

👉 Purpose: “assist everything”

---

### Main.java

* Only starts the program
* Calls other classes
* Should stay clean

---

# 4. Practical Demonstration

## Step 1 — Create a simple class in a separate file

### `model/Student.java`

```java
package model;

public class Student {
    public String name = "Default Name";
}
```

---

## Step 2 — Main class

### `Main.java`

```java
import model.Student;

public class Main {
    public static void main(String[] args) {

        Student student = new Student();

        System.out.println(student.name);
    }
}
```

---

## What just happened?

* `Student` is in another file
* We used `import model.Student`
* Java connected both files at compile time

---

# 5. How Java handles multiple files

When you run your program:

1. Java compiles ALL `.java` files inside `src`
2. It converts them into `.class` files
3. The JVM connects them automatically
4. `Main.main()` is executed first

You don’t need to manually “link” files — Java handles it.

---

# 6. Packages and Imports

## What is a package line?

```java
package model;
```

This tells Java:

> “This class belongs to the model folder.”

---

## Why imports are needed

If a class is in another package:

```java
import model.Student;
```

Without import, Java won’t find it.

---

## Default package vs named packages

### ❌ Default package (bad practice)

No package declared.

### ✅ Named packages (correct)

```java
package model;
package service;
```

Professional projects ALWAYS use packages.

---

# 7. Clean Architecture Basics (Beginner level)

You are not building full architecture yet — just learning separation.

But the idea is:

## Separation of concerns

* model → data
* service → logic
* util → helpers
* main → entry point

This prevents:

* messy code
* duplicated logic
* unreadable projects

---

# 8. Hands-on Exercises

## Exercise 1 — Create structure

Manually create:

```text
src/
 ├── Main.java
 ├── model/
 ├── service/
 └── util/
```

---

## Exercise 2 — Create files

Create:

* `model/Student.java`
* `model/Product.java`
* `Main.java`

---

## Exercise 3 — Move logic out of Main

1. Create `Student`
2. Create object in Main
3. Print values from Student

Main should NOT contain data definitions.

---

## Exercise 4 — Add package

Inside `Student.java`:

```java
package model;
```

Then fix imports in Main.

---

## Exercise 5 — Organize messy project

Take a project with everything in Main and:

* move classes to packages
* fix imports
* clean Main

---

# 9. Final Objective of this Chapter

At this point, you should be able to:

* Understand how Java projects are structured
* Know what `src`, packages, and folders are
* Create multiple files correctly
* Move code between files safely
* Use imports without confusion
* Keep `Main` clean and minimal

---

# 10. Checklist — Java Project Organization

Before starting any Java project, check:

* [ ] I have a `src` folder
* [ ] I use packages (`model`, `service`, `util`)
* [ ] Each class is in its own file
* [ ] File name matches class name
* [ ] Main is only the entry point
* [ ] I use imports correctly
* [ ] I don’t mix everything in one file
* [ ] My code is easy to navigate

---

# ✔️ Ready for Next Step

You are now ready to move forward.

Next: **Chapter 05 — Object-Oriented Programming (OOP)**

Where everything you learned here becomes essential:
classes, objects, attributes, methods, and real application design.
