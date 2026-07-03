# ⚙️ Chapter 3 — Attributes and Methods

In the previous chapter, you learned that a **class** is a blueprint and an **object** is an instance created from that blueprint.

Now it's time to understand **what goes inside a class**.

Every class is mainly composed of two things:

* **Attributes** → what the object *has* (its data)
* **Methods** → what the object *can do* (its behavior)

These two concepts are the foundation of Object-Oriented Programming.

---

# 🧠 1. What are Attributes?

Attributes (also called **instance variables** or **fields**) represent the **state** of an object.

They store information about each individual object.

### Example: Student

A student has:

* Name
* Age
* Grade

These are attributes because they describe the student.

```java
public class Student {

    String name;
    int age;
    double grade;

}
```

This class doesn't do anything yet—it only describes what information every `Student` object will store.

---

## 🌍 Real-World Example

Imagine two students:

```text
Student #1
-----------
Name: John
Age: 20
Grade: 8.5

Student #2
-----------
Name: Sarah
Age: 22
Grade: 9.8
```

Both are created from the same class, but each object stores its own values.

---

# 🧠 2. What are Methods?

Methods define the **behavior** of an object.

They represent the actions an object can perform.

### Examples

A student can:

* Display information
* Study
* Take an exam

A car can:

* Accelerate
* Brake
* Turn off

A bank account can:

* Deposit money
* Withdraw money
* Check balance

These actions become methods.

---

## Example

```java
public class Student {

    String name;
    int age;
    double grade;

    void displayInformation() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Grade: " + grade);
    }

}
```

Now the class has both:

* Data
* Behavior

---

# 🧠 3. Creating and Using Objects

Let's use our class.

## Student.java

```java
public class Student {

    String name;
    int age;
    double grade;

    void displayInformation() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Grade: " + grade);
    }

}
```

## Main.java

```java
import model.Student;

public class Main {

    public static void main(String[] args) {

        Student student = new Student();

        student.name = "John";
        student.age = 20;
        student.grade = 9.4;

        student.displayInformation();

    }

}
```

Output:

```text
Name: John
Age: 20
Grade: 9.4
```

Notice how the method automatically uses the data stored inside that specific object.

---

# 🧠 4. Object State vs Behavior

This distinction is extremely important.

### State

State is the data stored inside an object.

Example:

```text
Name: John
Age: 20
Grade: 9.4
```

These values describe the current condition of the object.

---

### Behavior

Behavior is what the object can do.

Example:

```java
displayInformation();
study();
takeExam();
```

Methods allow the object's state to be used or modified.

---

## Another Example

### Car

State:

```text
Brand
Model
Current Speed
Fuel Level
```

Behavior:

```text
accelerate()
brake()
refuel()
turnOff()
```

Whenever you model something in OOP, ask yourself two questions:

1. **What information does it have?**
2. **What actions can it perform?**

The answers usually become attributes and methods.

---

# 🧠 5. How Methods Work Internally

When you call:

```java
student.displayInformation();
```

Java:

1. Finds the object referenced by `student`.
2. Looks inside its class (`Student`) for the `displayInformation()` method.
3. Executes that method using the current object's data.

Inside the method, writing:

```java
System.out.println(name);
```

is equivalent to saying:

> "Print the `name` attribute that belongs to this specific object."

At this point, Java automatically knows you're referring to the object that called the method.

Later in this module, you'll learn that this is actually represented by the `this` keyword.

---

# 🧠 6. When to Use Attributes

Use attributes when information belongs to an object.

Good examples:

```text
Student
- name
- age
- grade

Book
- title
- author
- available

Product
- price
- quantity
```

Attributes represent characteristics, not actions.

---

# 🧠 7. When to Use Methods

Use methods whenever the object needs to perform an action.

Good examples:

```text
deposit()
withdraw()
accelerate()
displayInformation()
calculateTotal()
```

Methods represent behavior.

---

# ❌ Common Beginner Mistakes

### Mixing attributes and methods

Incorrect thinking:

```text
Student
- displayInformation
- name()
```

Remember:

* Data → Attribute
* Action → Method

---

### Putting everything inside `Main`

Many beginners write all their code inside `main()`.

Example:

```java
public static void main(String[] args) {

    String name = "John";
    int age = 20;

    System.out.println(name);
}
```

This works for very small programs, but as projects grow, it becomes difficult to maintain.

Instead, the data and related behavior should live inside the appropriate class.

---

# 🏗️ Project Structure Reminder

Our project should continue following the structure introduced in Module 04.5:

```text
src/
├── Main.java
├── model/
│   ├── Student.java
│   ├── Product.java
│   ├── Car.java
│   └── Book.java
├── service/
│   └── BankAccount.java
└── util/
    └── Helper.java
```

### Why separate classes into different files?

Because each class has a **single responsibility**.

* `Student.java` models students.
* `Product.java` models products.
* `Car.java` models cars.

This organization keeps projects clean, scalable, and easier to maintain.

`Main.java` should simply create objects and coordinate the application—not contain all the business logic.

---

# 🧪 Practice Exercise

Create a class named `Student` inside the `model` package.

The class must contain:

### Attributes

* `name`
* `age`
* `grade`

### Method

```java
displayInformation()
```

The method should print all the student's information.

Then, in `Main.java`:

* Create two different `Student` objects.
* Give each one different values.
* Call `displayInformation()` for both objects.

This exercise reinforces that multiple objects created from the same class maintain **independent state** while sharing the same behavior.

---

# ✔️ Chapter 3 Complete

Excellent progress!

You now understand the core building blocks of every class:

* How attributes represent an object's **state**
* How methods represent an object's **behavior**
* How objects use their own data when executing methods
* Why classes should encapsulate both data and behavior

These concepts form the foundation of everything you'll build in Object-Oriented Programming.

## ▶️ Next Step

Continue to **Chapter 4 — Constructors**, where you'll learn how objects are initialized properly when they are created, avoiding repetitive code and making your classes much easier to use.
