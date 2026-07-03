# 🧱 Chapter 2 — Classes and Objects

---

## 🧠 1. What is a Class?

A **class** is a blueprint (or template) used to create objects.

It defines:

* What data an object will have (attributes)
* What an object can do (methods)

### 🧩 Simple idea:

> A class is not a real thing. It is the “design”.

---

### 🏠 Real-world analogy

Think of a class like a blueprint of a house:

* Blueprint = class
* House built from blueprint = object

You can build many houses from the same blueprint.

---

## ⚙️ 2. What is an Object?

An **object** is a real instance created from a class.

It has:

* Actual values
* Memory allocation
* Independent state

### Example:

If `Student` is a class:

* `student1` = object
* `student2` = another object

Each one is independent.

---

## 🆚 Class vs Object (Very Important)

| Class               | Object          |
| ------------------- | --------------- |
| Blueprint           | Real instance   |
| Defined once        | Can be many     |
| No memory allocated | Uses memory     |
| Abstract concept    | Concrete entity |

---

## 🧪 3. Creating a Class in Java

```java id="class-example"
public class Student {
    String name;
    int age;
}
```

### What we just did:

* Created a blueprint called `Student`
* Defined 2 attributes:

  * name
  * age

---

## 🧪 4. Creating Objects using `new`

Now we create real objects:

```java id="object-example"
public class Main {
    public static void main(String[] args) {

        Student student1 = new Student();
        Student student2 = new Student();

        student1.name = "John";
        student1.age = 20;

        student2.name = "Maria";
        student2.age = 22;

        System.out.println(student1.name);
        System.out.println(student2.name);
    }
}
```

---

## 🧠 What is happening internally?

When you write:

```java
Student student1 = new Student();
```

Java:

* Creates an object in memory (heap)
* Returns a reference
* Stores it in `student1`

So `student1` does NOT contain the object — it points to it.

---

## 🔄 5. Object Lifecycle

An object goes through 3 stages:

### 1. Creation

```java
new Student();
```

### 2. Usage

```java
student1.name = "John";
```

### 3. Garbage Collection (automatic)

* When no references exist anymore
* Java removes it automatically

---

## 🧠 6. Multiple Objects, Same Class

This is key:

```java
Student s1 = new Student();
Student s2 = new Student();
```

They:

* Use the same blueprint
* But store different data
* Do NOT interfere with each other

---

## ⚠️ 7. Common Mistake

Many beginners think:

> “Student is the data”

Wrong.

Correct thinking:

> Student is just the blueprint. The object is the data.

---

## 🌍 8. Real-world Mapping

| Concept | Example           |
| ------- | ----------------- |
| Class   | Car blueprint     |
| Object  | Your actual car   |
| Class   | Bank account type |
| Object  | Your account      |

---

## 🧭 Key Mental Shift

You must internalize this:

> A program is not a list of actions.
> It is a collection of objects interacting.

---

# ✔️ Chapter 2 Complete

If you're ready, we move to:

# ▶️ Chapter 3 — Attributes and Methods
