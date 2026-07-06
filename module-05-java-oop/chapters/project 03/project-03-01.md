# 📦 Project 3 — Inventory Management System

Welcome to the final project of **Module 05**.

This project is different from the previous two.

Project 1 focused on CRUD operations.

Project 2 focused on business rules and object collaboration.

This final project combines **everything** you've learned throughout the module into one complete application.

Rather than introducing new Java features, the goal is to strengthen your Object-Oriented Programming skills by designing a clean, well-organized application from scratch.

---

# 🎯 Project Goal

Develop a console-based **Inventory Management System** capable of managing products in a small warehouse or store.

By the end of this project, the application will be able to:

* Register products
* Search products
* Update product information
* Remove products
* Increase stock
* Decrease stock
* Calculate the total inventory value
* Display all registered products

Every operation should respect proper encapsulation and business rules.

---

# 📚 Concepts Practiced

This final project reinforces every concept learned in Module 05:

* Classes
* Objects
* Constructors
* Encapsulation
* Getters and setters
* The `this` keyword
* Arrays
* Object communication
* Separation of responsibilities
* Business rules
* CRUD operations
* Clean project organization

---

# 📁 Project Structure

```text
src/
├── Main.java
├── model/
│   └── Product.java
├── service/
│   └── InventoryManager.java
└── util/
```

This architecture should already look familiar.

We're following the same design used in the previous projects because it scales well and keeps responsibilities separated.

---

# 🧠 Responsibilities

## Product

Represents **one product**.

Responsible for:

* Product ID
* Product name
* Price
* Quantity
* Calculating its own total value
* Increasing stock
* Decreasing stock
* Displaying its information

---

## InventoryManager

Responsible for:

* Storing products
* Registering products
* Searching products
* Updating products
* Removing products
* Listing products
* Calculating the total inventory value

---

## Main

Responsible for:

* Starting the application
* Creating objects
* Calling methods
* Displaying results

Exactly like the previous projects, `Main` should remain small and free of business logic.

---

# 🏗️ Project Development Roadmap

We'll build this project progressively.

## Stage 1

Project setup.

---

## Stage 2

Create the `Product` class.

---

## Stage 3

Create the `InventoryManager`.

---

## Stage 4

Register and list products.

---

## Stage 5

Search and update products.

---

## Stage 6

Increase and decrease stock.

---

## Stage 7

Remove products.

---

## Stage 8

Calculate the total inventory value.

---

## Stage 9

Final cleanup and refactoring.

---

# 🚀 Stage 1 — Project Setup

Create the following structure:

```text
src/
├── Main.java
├── model/
│   └── Product.java
├── service/
│   └── InventoryManager.java
└── util/
```

Initially:

* `Product.java` can be an empty class.
* `InventoryManager.java` can be an empty class.

Update `Main.java`:

```java
public class Main {

    public static void main(String[] args) {

        System.out.println("===== Inventory Management System =====");

    }

}
```

Expected output:

```text
===== Inventory Management System =====
```

---

# 🧠 Why Another Manager Class?

By now, you should notice a recurring pattern.

Each project has:

* A **model** class that represents a single object.
* A **manager** class that manages many objects.
* A **Main** class that coordinates everything.

This is intentional.

Professional software often follows the same architecture because it keeps code modular, readable, and easy to extend.

---

# 💡 Real-World Mapping

Imagine a small electronics store.

Each product knows:

* Its ID
* Its name
* Its price
* How many units are in stock

But a product does **not** know:

* Every other product in the store
* The total inventory value
* How many products exist

Those responsibilities belong to the inventory management system.

Our `InventoryManager` represents that system.

---

# 🏗️ Looking Ahead

This final project will require you to reuse many techniques you've already learned.

For example:

* Searching by ID will be similar to searching for students or bank accounts.
* Updating products will reuse encapsulation through setters.
* Stock management will reuse business-rule validation like deposits and withdrawals.
* Removing products will reuse array shifting techniques from Project 1.

You'll begin to notice that good software development is often about **reusing well-designed ideas**, not constantly inventing new ones.

---

# ✔️ Stage 1 Complete

Your final project is now initialized.

Everything is ready to begin building the core of the Inventory Management System.

## ▶️ Next Step

Continue to **Project 3 — Stage 2: Building the `Product` Class**, where you'll create a fully encapsulated product model with constructors, validation, stock management methods, and the ability to calculate its own total inventory value.
