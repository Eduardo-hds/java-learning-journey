Good. We’ll set this module up properly first, then move into Chapter 1.

---

# 📘 Module 06 Index — Inheritance

This module is divided into progressive chapters:

## Chapter 1 — What is Inheritance (Core Concept)

* Definition of inheritance
* Why it exists in software design
* Real-world modeling analogy
* “is-a” relationship

## Chapter 2 — Java Inheritance Basics

* `extends` keyword
* Superclass vs subclass
* Basic class hierarchy

## Chapter 3 — Constructors & `super()`

* Constructor chaining
* Initialization order
* Parent constructor calls

## Chapter 4 — Method Overriding (Basic)

* What overriding is
* `@Override` annotation
* Behavior customization

## Chapter 5 — The `super` Keyword

* Access parent methods
* Access parent constructors
* Access parent attributes

## Chapter 6 — Designing Class Hierarchies

* When inheritance makes sense
* When it becomes a bad design
* Common mistakes (over-inheritance)

## Chapter 7 — Guided Practice Systems

* Animal system
* Employee system
* Vehicle system
* Shape system

## Chapter 8 — Constructor & Overriding Practice Lab

* Focused exercises combining all concepts

## Chapter 9 — Final Project (Build Phase)

* Role-based system
* Progressive construction (no full solution upfront)

## Chapter 10 — Review & Consolidation

* Key patterns
* Common errors
* Mental model solidification

---

# 🧠 Inheritance vs Composition (Validation Step)

Before we continue, you need to be clear on this distinction:

## Inheritance (IS-A)

* Dog **is an** Animal
* Manager **is an** Employee
* Car **is a** Vehicle

Used when there is a **natural hierarchy**

## Composition (HAS-A)

* Car **has an** Engine
* Employee **has a** Salary object
* Order **has items**

Used when one class is made of other components

---

# ⚠️ Quick Check (Important)

Answer mentally or briefly:

1. Does “Car has Engine” fit inheritance or composition?
2. Does “Manager is Employee” fit inheritance or composition?
3. Would you model “Dog has Tail” using inheritance or composition?

---

# 🧩 Final Project Design (Preview)

We will build:

## 🎯 Role-Based System

### Base class:

* `Employee`

### Child classes (at least 3):

* `Manager`
* `Developer`
* `Intern`

### Expected behavior:

* Each role calculates salary differently
* Each role has its own description method
* Constructor chaining using `super()`

### Core concepts used:

* inheritance hierarchy
* method overriding
* constructor chaining
* `super`

