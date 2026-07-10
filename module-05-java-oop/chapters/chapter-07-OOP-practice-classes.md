# 🧪 Chapter 7 — OOP Practice Classes

Congratulations! You have now learned all the fundamental concepts of Object-Oriented Programming covered in this module:

* Classes
* Objects
* Attributes
* Methods
* Constructors
* Encapsulation
* The `this` keyword

Now it's time to put everything together.

Instead of learning new concepts, this chapter is focused entirely on **practice**.

You will build several small classes that model real-world entities while applying everything you've learned so far.

---

# 🎯 Chapter Goal

By the end of this chapter, you should be able to:

* Design simple classes
* Model real-world objects
* Create constructors
* Encapsulate data
* Validate user input
* Organize files into packages
* Keep `Main.java` clean
* Understand how objects interact

---

# 📁 Project Structure

Throughout these exercises, keep the same project organization:

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

### Why this structure?

Each class has a single responsibility.

* `model` contains the entities of your application.
* `service` contains classes responsible for business operations.
* `util` contains helper or utility classes.
* `Main` is responsible only for starting the program and coordinating the objects.

This separation keeps projects organized and scalable.

---

# 📝 Exercise 1 — Student

## Objective

Create a class that represents a student.

### Attributes

```java
private String name;
private int age;
private double grade;
```

### Constructors

Create:

* A default constructor
* A parameterized constructor

### Methods

```java
displayInformation()
```

Print all student information.

### Validation

* Name cannot be blank.
* Age cannot be negative.
* Grade must be between `0` and `10`.

---

# 🛒 Exercise 2 — Product

## Objective

Model a product in an inventory.

### Attributes

```java
private String name;
private double price;
private int quantity;
```

### Methods

```java
calculateTotalValue()
```

Returns:

```text
price × quantity
```

Example:

```text
Price: 20

Quantity: 5

Total Value: 100
```

### Validation

* Price must be greater than zero.
* Quantity cannot be negative.

---

# 🏦 Exercise 3 — BankAccount

Place this class inside the **service** package.

## Attributes

```java
private String owner;
private double balance;
```

### Methods

```java
deposit()
withdraw()
displayAccount()
```

### Rules

Deposit:

* Cannot deposit negative values.

Withdraw:

* Cannot withdraw more than the balance.
* Cannot withdraw negative values.

Example:

```text
Deposit: 500

Withdraw: 200

Balance: 300
```

---

# 🚗 Exercise 4 — Car

## Attributes

```java
private String brand;
private String model;
private int speed;
```

### Methods

```java
accelerate()
brake()
displayStatus()
```

Rules:

* Speed cannot go below `0`.
* Speed increases by fixed values.
* Speed decreases by fixed values.

Example:

```text
Brand: Toyota

Model: Corolla

Speed: 60 km/h
```

---

# 📚 Exercise 5 — Book

## Attributes

```java
private String title;
private String author;
private boolean available;
```

### Methods

```java
borrowBook()
returnBook()
displayInformation()
```

Rules:

If already borrowed:

```text
Book is not available.
```

Otherwise:

```text
Book borrowed successfully.
```

---

# 🏗️ Exercise 6 — Constructor Practice

Go back to every class and make sure each one has:

* Default constructor
* Parameterized constructor

Example:

```java
Product()
```

```java
Product(String name, double price, int quantity)
```

Repeat this for:

* Student
* Product
* Car
* Book
* BankAccount

---

# 🔒 Exercise 7 — Encapsulation Review

Every attribute should now be:

```java
private
```

Every class should include:

* Getters
* Setters
* Validation

Examples:

Student

```text
Age >= 0

Grade between 0 and 10
```

Product

```text
Price > 0

Quantity >= 0
```

Car

```text
Speed >= 0
```

BankAccount

```text
Balance cannot become negative.
```

---

# 🧠 Design Challenge

Before writing any code for each class, ask yourself these two questions:

### 1. What information does this object have?

These become the **attributes**.

Example:

A `Book` has:

* Title
* Author
* Availability

---

### 2. What actions can this object perform?

These become the **methods**.

Example:

A `Book` can:

* Be borrowed
* Be returned
* Display its information

This way of thinking is one of the most valuable habits you can develop in Object-Oriented Programming.

---

# 💡 Best Practices Learned in This Module

As you complete these exercises, keep these principles in mind:

* One class should represent one concept.
* Keep attributes `private`.
* Expose behavior through methods.
* Validate data before changing an object's state.
* Use constructors to initialize objects.
* Use `this` when referring to the current object.
* Keep `Main.java` focused on coordinating objects, not implementing business logic.
* Organize related classes into appropriate packages.

Following these practices from the beginning will make your code cleaner, easier to maintain, and much closer to professional Java development.

---

# ✔️ Module Practice Complete

Excellent work!

You have now practiced every core concept introduced in this module:

* Creating classes and objects
* Defining attributes and methods
* Initializing objects with constructors
* Protecting data through encapsulation
* Using getters and setters with validation
* Working with the `this` keyword
* Organizing a project using packages
* Modeling real-world entities using Object-Oriented Programming

You are now ready to apply these concepts in complete applications.
