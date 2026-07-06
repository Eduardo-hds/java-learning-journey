# 📘 Chapter 3 — Constructors & `super()` in Inheritance

---

# 🧠 1. What this chapter is about

Now we connect inheritance with object creation.

You will learn:

* What happens when a child object is created
* How constructors behave in inheritance
* Why `super()` exists
* How initialization order works

---

# ⚙️ 2. Key idea: object creation in inheritance

When you create a child object:

```java
Dog dog = new Dog();
```

Java does NOT only create the Dog part.

It also automatically creates the **Animal part first**.

So the flow is:

> Parent constructor → Child constructor

---

# 🧱 3. Constructor chaining (important concept)

Constructor chaining means:

> A constructor calls another constructor during object creation.

In inheritance, this happens automatically using `super()`.

---

# 🔷 4. What is `super()`?

`super()` is a special call that refers to the **parent class constructor**.

Example:

```java
super();
```

It means:

> “Call the constructor of the superclass”

---

# ⚙️ 5. Default behavior (important)

Even if you don’t write `super()` explicitly:

```java
public Dog() {
}
```

Java automatically adds:

```java
super();
```

BUT only if the parent has a **no-argument constructor**.

---

# 🧩 6. Example with constructors

Let’s improve your Animal system.

---

## 🐾 Animal (Parent)

```java id="animal_ctor"
package model;

public class Animal {

    String name;
    int age;

    public Animal() {
        System.out.println("Animal constructor called");
    }

    public void eat() {
        System.out.println(name + " is eating");
    }
}
```

---

## 🐶 Dog (Child)

```java id="dog_ctor"
package model;

public class Dog extends Animal {

    public Dog() {
        super(); // calls Animal constructor
        System.out.println("Dog constructor called");
    }

    public void bark() {
        System.out.println(name + " is barking");
    }
}
```

---

# 🧠 7. What happens when we run this?

```java
Dog dog = new Dog();
```

### Execution order:

1. Animal constructor runs
2. Dog constructor runs

### Output:

```
Animal constructor called
Dog constructor called
```

---

# ⚠️ 8. Important rule: parent ALWAYS initializes first

No matter what:

> Parent class constructor always runs before child constructor

This ensures:

* parent data is ready
* child can safely use inherited fields

---

# 🧱 9. Constructor with parameters

Now we make it more realistic.

---

## 🐾 Animal

```java id="animal_param"
package model;

public class Animal {

    String name;
    int age;

    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
        System.out.println("Animal created: " + name);
    }
}
```

---

## 🐶 Dog

```java id="dog_param"
package model;

public class Dog extends Animal {

    String breed;

    public Dog(String name, int age, String breed) {
        super(name, age); // sending values to parent
        this.breed = breed;

        System.out.println("Dog created: " + breed);
    }
}
```

---

# 🧠 10. What is happening here?

* Dog constructor receives 3 values
* It passes 2 to Animal using `super(name, age)`
* Animal initializes shared fields
* Dog initializes its own field

---

# 💡 11. Why `super()` is important

Without `super(name, age)`:

* Parent data would NOT be initialized correctly
* You would duplicate logic in child class
* Design becomes messy and error-prone

---

# ❌ 12. Common mistakes

### Mistake 1: Not calling super when needed

```java
super(name, age);
```

Missing this breaks proper initialization.

---

### Mistake 2: Trying to use parent fields before super()

```java
this.name = name; // ❌ too early sometimes
super(name, age);
```

Wrong order → always call `super()` first.

---

### Mistake 3: Assuming constructors are inherited

Constructors are NOT inherited.

Each class defines its own constructors.

---

# 🧠 13. Mental model

Think:

> Parent builds the foundation
> Child builds on top of it

So:

* Animal = base structure
* Dog = extended structure

---

# 🧪 Quick check

Before moving on, you should understand:

* Does parent constructor run first?
* What does `super()` do?
* Are constructors inherited?

---

# ✔️ Next Step

Now we will modify behavior in child classes using:

# 👉 Chapter 4 — Method Overriding (Basic Level)