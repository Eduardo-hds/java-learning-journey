# 💼 Project 1 — Stage 2: Building the `Student` Class

Now that the project structure is ready, it's time to build the heart of our application.

The `Student` class represents **one student**.

Remember one of the most important OOP principles:

> **A class should represent one real-world entity and have one clear responsibility.**

The `Student` class should only know about a single student. It should **not** know how to manage a list of students—that will be the responsibility of `StudentManager`.

---

# 🎯 Stage Goal

By the end of this stage, the `Student` class will:

* Represent a single student
* Store its own data
* Protect its data using encapsulation
* Validate information
* Display its own information

---

# 📁 Project Structure

```text
src/
├── Main.java
├── model/
│   └── Student.java
├── service/
│   └── StudentManager.java
└── util/
```

Only `Student.java` will be implemented in this stage.

---

# 🏗️ Step 1 — Create the Attributes

Inside `Student.java`, create the following private attributes:

```java
private String name;
private int age;
private double grade;
```

### Why `private`?

Because the object's data should not be modified directly from outside the class.

Instead of:

```java
student.age = -10;
```

we will force other classes to use setters that validate the data.

---

# 🏗️ Step 2 — Create the Constructors

## Default Constructor

```java
public Student() {
    this("Unknown", 0, 0.0);
}
```

This creates a student with default values.

---

## Parameterized Constructor

```java
public Student(String name, int age, double grade) {
    setName(name);
    setAge(age);
    setGrade(grade);
}
```

Notice something important.

Instead of writing:

```java
this.name = name;
```

we call the setters.

### Why?

Because the setters already contain validation.

This prevents invalid data from being assigned even during object creation.

This is considered a good practice.

---

# 🏗️ Step 3 — Create Getters

Create one getter for each attribute.

Example:

```java
public String getName() {
    return name;
}
```

Repeat for:

* age
* grade

---

# 🏗️ Step 4 — Create Setters with Validation

## Name

```java
public void setName(String name) {

    if (name != null && !name.isBlank()) {
        this.name = name;
    }

}
```

---

## Age

```java
public void setAge(int age) {

    if (age >= 0) {
        this.age = age;
    }

}
```

---

## Grade

```java
public void setGrade(double grade) {

    if (grade >= 0 && grade <= 10) {
        this.grade = grade;
    }

}
```

Now the object protects itself from invalid values.

---

# 🏗️ Step 5 — Create `displayInformation()`

Add a method that prints the student's information.

Example output:

```text
-------------------------
Student Information
-------------------------
Name : John
Age  : 20
Grade: 9.5
-------------------------
```

The method should only **display** information.

It should not ask for user input or modify the object.

---

# 🧠 Design Discussion

Why does `displayInformation()` belong inside `Student`?

Because the student already knows all of its own data.

If `Main` printed every attribute manually:

```java
System.out.println(student.getName());
System.out.println(student.getAge());
System.out.println(student.getGrade());
```

that formatting logic would have to be repeated everywhere.

Instead, the object becomes responsible for presenting itself.

---

# 🧪 Testing the Class

Update `Main.java` temporarily.

Create two students.

Example:

```java
Student student1 = new Student(
    "John",
    20,
    9.5
);

Student student2 = new Student(
    "Sarah",
    22,
    8.8
);
```

Display both:

```java
student1.displayInformation();

student2.displayInformation();
```

Expected output:

```text
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
```

---

# 💡 Why Are We Testing Now?

Professional developers test small pieces before building larger systems.

Right now, we are verifying that:

* Constructors work
* Validation works
* Getters and setters work
* Objects store independent data
* Methods behave correctly

Only after the model is reliable do we move on to managing multiple students.

---

# ✔️ Stage 2 Complete

Excellent!

You have now built the first real class of your application.

Your `Student` class now follows good Object-Oriented Programming practices:

* Private attributes
* Constructors
* Encapsulation
* Validation
* Clean public methods
* Single responsibility

This class is now ready to be used by other parts of the system.

## ▶️ Next Step

Continue to **Project 1 — Stage 3: Building the `StudentManager` Class**, where you'll create a class responsible for storing and managing multiple `Student` objects while keeping `Student` focused on representing a single student.
