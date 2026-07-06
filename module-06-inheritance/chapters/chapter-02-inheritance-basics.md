# 📘 Chapter 2 — Java Inheritance Basics (`extends`, superclass, subclass)

---

# 🧠 1. What this chapter is about

Now we move from concept → code.

You will learn how Java actually implements inheritance using:

* `extends`
* superclass (parent class)
* subclass (child class)

---

# ⚙️ 2. The `extends` keyword

In Java, inheritance is created using:

```java
class Child extends Parent {
}
```

Meaning:

> “Child class inherits from Parent class”

---

# 🧱 3. Superclass vs Subclass

## 🔷 Superclass (Parent)

The class that provides shared behavior.

Example:

* `Animal`

## 🔶 Subclass (Child)

The class that inherits from the parent.

Example:

* `Dog`
* `Cat`

---

# 🧩 4. First real example (Animal system)

Let’s start inside your structure:

```text
src/
 ├── model/
 │    ├── Animal.java
 │    ├── Dog.java
 │    ├── Cat.java
```

---

## 🐾 Step 1 — Parent class: Animal

```java
package model;

public class Animal {

    String name;
    int age;

    public void eat() {
        System.out.println(name + " is eating");
    }

    public void sleep() {
        System.out.println(name + " is sleeping");
    }
}
```

---

## 🐶 Step 2 — Child class: Dog

```java
package model;

public class Dog extends Animal {

    public void bark() {
        System.out.println(name + " is barking");
    }
}
```

---

## 🐱 Step 3 — Child class: Cat

```java
package model;

public class Cat extends Animal {

    public void meow() {
        System.out.println(name + " is meowing");
    }
}
```

---

# 🧠 5. What just happened?

Both `Dog` and `Cat`:

✔ Inherited `name`
✔ Inherited `age`
✔ Inherited `eat()`
✔ Inherited `sleep()`

But also:

✔ Dog has `bark()`
✔ Cat has `meow()`

---

# 💡 6. How it works in memory (simple view)

When you create:

```java
Dog dog = new Dog();
```

Java internally creates:

```
Animal part (name, age, eat, sleep)
+
Dog part (bark)
```

So the object is a **combination of both**

---

# 🧪 7. Using inherited behavior

Now in `Main.java`:

```java
import model.Dog;
import model.Cat;

public class Main {
    public static void main(String[] args) {

        Dog dog = new Dog();
        dog.name = "Rex";
        dog.age = 3;

        dog.eat();   // inherited
        dog.sleep(); // inherited
        dog.bark();  // own method

        Cat cat = new Cat();
        cat.name = "Mimi";
        cat.age = 2;

        cat.eat();
        cat.meow();
    }
}
```

---

# ⚠️ 8. Important rules

## ✔ What child class CAN do:

* Use parent methods
* Use parent variables
* Add new methods
* Extend behavior

## ❌ What it cannot do directly:

* Remove parent features
* Access private members (we’ll expand later)

---

# 🧠 9. Key mental model

Inheritance means:

> “I reuse everything from the parent, and I add my own features.”

Not:

> “I copy code from another class”

---

# ❌ 10. Common mistakes

### Mistake 1: Forgetting `extends`

Without it, no inheritance happens.

---

### Mistake 2: Thinking inheritance copies code

It does NOT copy — it **links behavior**

---

### Mistake 3: Overusing inheritance

Not everything should extend something else

---

# 🧪 Quick check

Ask yourself:

* Does Dog automatically get eat()?
* Does Cat automatically get sleep()?
* Can Dog add new methods?

If yes → you understand the model correctly.

---

# ✔️ Next Step

Now that you understand basic inheritance, we go deeper into **how objects are initialized using constructors and `super()`**.

# 👉 Chapter 3 — Constructors & `super()` in inheritance

