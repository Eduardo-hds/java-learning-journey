# 🏗️ Chapter 4 — Constructors

Until now, every time we created an object, we had to manually assign values to its attributes.

Example:

```java
Student student = new Student();

student.name = "John";
student.age = 20;
student.grade = 9.5;
```

This works, but it becomes repetitive and error-prone as classes grow.

To solve this problem, Java provides **constructors**.

---

# 🧠 1. What is a Constructor?

A **constructor** is a special method that is automatically executed when an object is created.

Its main purpose is to **initialize the object's state**.

Think of it as the setup process that prepares an object before it is used.

---

## Why do constructors exist?

Imagine creating 100 students.

Without constructors:

```java
Student s1 = new Student();
s1.name = "John";
s1.age = 20;
s1.grade = 9.5;

Student s2 = new Student();
s2.name = "Sarah";
s2.age = 21;
s2.grade = 8.8;
```

You repeat the same assignments over and over.

With constructors:

```java
Student s1 = new Student("John", 20, 9.5);
Student s2 = new Student("Sarah", 21, 8.8);
```

Cleaner, safer, and easier to read.

---

# 🧠 2. Constructor Syntax

A constructor looks similar to a method, but there are two important differences:

* It has the **same name as the class**.
* It has **no return type**, not even `void`.

Example:

```java
public class Student {

    String name;
    int age;
    double grade;

    public Student() {

    }

}
```

Notice:

* Class name: `Student`
* Constructor name: `Student`
* No return type

---

# ⚙️ 3. The Default Constructor

A **default constructor** receives no parameters.

Example:

```java
public class Student {

    String name;
    int age;
    double grade;

    public Student() {
        System.out.println("Student created!");
    }

}
```

Creating an object:

```java
Student student = new Student();
```

Output:

```text
Student created!
```

The constructor runs automatically.

---

# 🧠 4. What Happens Internally?

When Java executes:

```java
Student student = new Student();
```

The following steps occur:

1. Memory is allocated for the object.
2. Attributes receive default values.
3. The constructor executes.
4. The reference is returned.
5. The object is ready to use.

Default values:

| Type    | Default Value |
| ------- | ------------- |
| int     | 0             |
| double  | 0.0           |
| boolean | false         |
| char    | '\u0000'      |
| Object  | null          |

---

# 🧠 5. Parameterized Constructor

Usually, we want objects to be created with meaningful values.

Example:

```java
public class Student {

    String name;
    int age;
    double grade;

    public Student(String name, int age, double grade) {

        this.name = name;
        this.age = age;
        this.grade = grade;

    }

}
```

Creating an object:

```java
Student student = new Student("John", 20, 9.5);
```

Now the object is fully initialized as soon as it is created.

---

# 🧠 6. Understanding `this`

Inside the constructor:

```java
this.name = name;
```

There are two variables named `name`.

The parameter:

```java
name
```

The object's attribute:

```java
this.name
```

So this line means:

> Assign the parameter `name` to the current object's `name` attribute.

We'll study `this` in depth later, but you'll see it frequently inside constructors.

---

# 🧠 7. Constructor Overloading

A class can have **multiple constructors**, as long as their parameter lists are different.

Example:

```java
public class Student {

    String name;
    int age;
    double grade;

    public Student() {

    }

    public Student(String name) {
        this.name = name;
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Student(String name, int age, double grade) {
        this.name = name;
        this.age = age;
        this.grade = grade;
    }

}
```

Now Java can choose the correct constructor depending on how the object is created.

Examples:

```java
Student s1 = new Student();

Student s2 = new Student("John");

Student s3 = new Student("John", 20);

Student s4 = new Student("John", 20, 9.5);
```

This is called **constructor overloading**.

---

# 🧠 8. When Should You Use Constructors?

Use constructors whenever an object needs to start with valid data.

Examples:

### Student

```java
Student student = new Student("John", 20, 9.5);
```

### Product

```java
Product product = new Product("Keyboard", 150.0, 10);
```

### Car

```java
Car car = new Car("Toyota", "Corolla");
```

This makes your objects immediately ready to use.

---

# 🚫 When NOT to Overload Constructors

Avoid creating too many constructors with similar purposes.

Bad example:

```java
Student()

Student(String name)

Student(String name, int age)

Student(String name, int age, double grade)

Student(String name, int age, double grade, boolean active)

Student(String name, int age, double grade, boolean active, String city)
```

While valid, having many overloaded constructors can make a class difficult to understand and maintain.

As you'll learn in future modules, there are alternative patterns that handle complex object creation more elegantly.

---

# 🏗️ Project Structure Reminder

Constructors belong inside the classes they initialize.

Example:

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

`Main.java` should simply create objects:

```java
Student student = new Student("John", 20, 9.5);
```

The logic for initializing those objects belongs inside the class itself.

---

# 🧪 Practice Exercise

## Part 1

Create a `Student` class with:

Attributes:

* `name`
* `age`
* `grade`

Create a **default constructor** that prints:

```text
New student created.
```

---

## Part 2

Create a **parameterized constructor** that initializes all three attributes.

Example:

```java
Student student = new Student("John", 20, 9.5);
```

---

## Part 3

Create a `displayInformation()` method to print the student's data.

---

## Part 4

In `Main.java`:

* Create one student using the default constructor.
* Create another student using the parameterized constructor.
* Display both students' information.
* Observe the differences between the two objects.

---

# ✔️ Chapter 4 Complete

Excellent work!

You now understand one of the most important parts of object creation in Java:

* What constructors are
* Why they exist
* How Java automatically calls them
* The difference between default and parameterized constructors
* How constructor overloading works
* Why constructors help create valid, ready-to-use objects

These concepts will be used constantly in every object-oriented project you build.

## ▶️ Next Step

Continue to **Chapter 5 — Encapsulation**, where you'll learn how to protect an object's data using `private` fields, expose controlled access through getters and setters, and enforce validation to keep objects in a valid state.
