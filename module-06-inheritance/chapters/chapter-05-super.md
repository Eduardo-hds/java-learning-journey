# 📘 Chapter 5 — The `super` Keyword

---

# 🧠 1. What this chapter is about

Now you will learn how a child class can **explicitly interact with its parent class** using:

> `super`

You will understand:

* Accessing parent methods
* Accessing parent constructors (quick review + expansion)
* Accessing parent attributes
* Why `super` is important in real designs

---

# ⚙️ 2. What is `super`?

`super` is a reference that points to the **parent class object part inside a child object**.

In simple terms:

> “I want to access something from the parent version of this class”

---

# 🧱 3. Using `super` to access parent methods

---

## 🐾 Example setup

### Animal

```java id="animal_super"
package model;

public class Animal {

    String name;

    public void makeSound() {
        System.out.println(name + " makes a generic sound");
    }
}
```

---

### Dog (overriding + super usage)

```java id="dog_super"
package model;

public class Dog extends Animal {

    @Override
    public void makeSound() {
        super.makeSound(); // call parent version first
        System.out.println(name + " barks loudly");
    }
}
```

---

# 🧠 4. What happens here?

When calling:

```java id="call_super_method"
Dog dog = new Dog();
dog.name = "Rex";
dog.makeSound();
```

### Output:

```text id="out_super_method"
Rex makes a generic sound  
Rex barks loudly
```

---

## 💡 Key idea:

You are combining:

* parent behavior (`super.makeSound()`)
* child behavior (`barks loudly`)

---

# 🧱 5. Using `super` with attributes

You normally access inherited attributes directly:

```java id="attr_direct"
name = "Rex";
```

But `super` can be used to clarify parent access (especially in complex cases).

---

## Example:

```java id="super_attr"
System.out.println(super.name);
```

⚠️ Usually used when:

* child redeclares a field with same name
* or to improve clarity

---

# ⚙️ 6. `super()` vs `super.method()`

| Usage            | Meaning                  |
| ---------------- | ------------------------ |
| `super()`        | Calls parent constructor |
| `super.method()` | Calls parent method      |
| `super.field`    | Access parent field      |

---

# 🧱 7. Full real example (combining everything)

---

## Animal

```java id="animal_full"
package model;

public class Animal {

    String name;

    public Animal(String name) {
        this.name = name;
        System.out.println("Animal created: " + name);
    }

    public void makeSound() {
        System.out.println(name + " makes a sound");
    }
}
```

---

## Dog

```java id="dog_full"
package model;

public class Dog extends Animal {

    public Dog(String name) {
        super(name); // constructor chaining
        System.out.println("Dog created: " + name);
    }

    @Override
    public void makeSound() {
        super.makeSound(); // parent behavior
        System.out.println(name + " barks");
    }
}
```

---

# 🧠 8. Why `super` is important

Without `super`:

* You lose access to parent logic
* You duplicate code
* You break hierarchy consistency

With `super`:

* You reuse behavior
* You extend behavior instead of replacing it
* You keep code clean and structured

---

# ❌ 9. Common mistakes

### Mistake 1: Forgetting super in constructor

```java id="missing_super"
public Dog(String name) {
    this.name = name; // ❌ wrong design in inheritance
}
```

---

### Mistake 2: Calling super incorrectly

```java id="wrong_super"
super.makeSound(); // only works if method exists in parent
```

---

### Mistake 3: Overusing super

If you always call parent + child, overriding loses meaning.

---

# 🧠 10. Mental model

Think:

> `super` = “parent version of this object”

---

# 🧪 Quick check

Make sure you understand:

* What does `super.makeSound()` do?
* What is the difference between `super()` and `super.method()`?
* Why do we use super in constructors?

---

# ✔️ Next Step

Now we move to design thinking:

# 👉 Chapter 6 — Class Hierarchy Design (When to use / avoid inheritance)