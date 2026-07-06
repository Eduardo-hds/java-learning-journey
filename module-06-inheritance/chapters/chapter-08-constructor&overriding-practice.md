# 📘 Chapter 8 — Constructor & Overriding Practice Lab

---

# 🧠 1. What this chapter is about

Now we combine everything you learned so far into **focused hands-on practice**:

* inheritance structure
* constructors + `super()`
* method overriding
* `super` usage
* initialization order

But still in a **controlled step-by-step lab**, not full projects yet.

---

# 🧩 LAB 1 — Animal Constructor Flow

---

## 🎯 Goal

Understand constructor order + inheritance together.

We will use:

* `Animal`
* `Dog`

---

## 🧱 Step 1 — Parent class (Animal)

You must ensure:

* constructor prints a message
* has a field `name`

Think first:

> What should happen when any Animal is created?

---

## 🧠 Expected behavior:

When any animal is created:

* it should initialize shared data
* it should confirm creation in console

---

## 🧩 Step 2 — Child class (Dog)

Dog must:

* call parent constructor using `super`
* add its own message
* optionally add breed field

---

## ⚙️ Key observation

When you run:

```java
new Dog();
```

You should observe:

1. Animal constructor runs first
2. Dog constructor runs second

---

## 🧪 Task

Modify your code so that output clearly shows:

* parent initialization
* child initialization

---

# 🧩 LAB 2 — Overriding Behavior Change

---

## 🎯 Goal

Understand how overriding changes runtime behavior.

We use:

* Animal
* Dog

---

## 🧠 Step 1 — Parent method

Create:

```java
makeSound()
```

in Animal:

* generic behavior

---

## 🧠 Step 2 — Child override

In Dog:

* override `makeSound()`
* change behavior completely OR extend it using `super.makeSound()`

---

## ⚙️ Experiment A

Call:

```java
Animal a = new Dog();
a.makeSound();
```

Observe result.

---

## 💡 Key idea

Even though reference type is Animal:

> runtime object decides behavior

---

# 🧩 LAB 3 — Employee Salary Override

---

## 🎯 Goal

Practice real-world inheritance logic.

---

## Structure:

* Employee (base)
* Manager (child)
* Developer (child)

---

## 🧠 Step 1 — Parent

Employee has:

* name
* baseSalary
* calculateSalary()

---

## 🧠 Step 2 — Override logic

### Manager:

* adds bonus

### Developer:

* adds performance bonus (or fixed increment)

---

## ⚙️ Key requirement

Each class must override:

```java
calculateSalary()
```

---

# 🧩 LAB 4 — Vehicle Behavior Override

---

## 🎯 Goal

Understand behavioral differences.

---

## Structure:

* Vehicle
* Car
* Motorcycle

---

## 🧠 Step 1 — Parent

Vehicle has:

* start()
* stop()

---

## 🧠 Step 2 — Override

Each subclass must:

* change message
* reflect real behavior

---

## 💡 Example idea:

* Car → engine ignition
* Motorcycle → kickstart / ignition sound

---

# 🧠 5. What you should learn from this chapter

After completing labs, you should clearly understand:

* constructor order (parent → child)
* how `super()` connects constructors
* how overriding replaces behavior
* how runtime decides method execution

---

# ⚠️ 6. Common mistakes in this stage

* forgetting `super()` in constructor
* not testing polymorphic behavior (`Animal a = new Dog()`)
* thinking methods are chosen by variable type (they are NOT)
* mixing fields between parent and child incorrectly

---

# 🧪 Final check

You are ready if you can answer:

* Who runs first: parent or child constructor?
* What does overriding change?
* Why does `Animal a = new Dog()` still call Dog methods?

---

# ✔️ Next Step

Now we move to the final challenge of this module:

# 👉 Chapter 9 — Final Project (Role-Based System)
