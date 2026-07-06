# 📘 Chapter 4 — Method Overriding (Basic Level)

---

# 🧠 1. What this chapter is about

Now we reach a key inheritance feature:

> A child class can **change the behavior of a method inherited from the parent**

This is called **method overriding**.

You will learn:

* What overriding is
* Why it exists
* How `@Override` works
* How behavior changes in subclasses

---

# ⚙️ 2. What is Method Overriding?

Method overriding happens when:

> A child class provides its own implementation of a method already defined in the parent class.

---

## 🧩 Simple idea:

* Parent defines a behavior
* Child customizes that behavior

---

# 🌍 Real-world analogy

Think:

* Animal → makesSound()
* Dog → barks
* Cat → meows

Same concept:

> Same action name, different behavior

---

# 🧱 3. Example (before overriding)

## 🐾 Animal

```java id="animal_override"
package model;

public class Animal {

    String name;

    public void makeSound() {
        System.out.println(name + " makes a generic sound");
    }
}
```

---

## 🐶 Dog (no override yet)

```java id="dog_no_override"
package model;

public class Dog extends Animal {

    public void bark() {
        System.out.println(name + " is barking");
    }
}
```

---

## Output behavior:

```java id="main_no_override"
Dog dog = new Dog();
dog.name = "Rex";

dog.makeSound();
```

### Output:

```
Rex makes a generic sound
```

---

# 🔥 4. Now with overriding

We change Dog behavior:

```java id="dog_override"
package model;

public class Dog extends Animal {

    @Override
    public void makeSound() {
        System.out.println(name + " barks loudly");
    }
}
```

---

# 🧠 5. What changed?

Now:

* Dog still HAS `makeSound()`
* But it behaves differently

---

## Output now:

```java id="main_override"
Dog dog = new Dog();
dog.name = "Rex";

dog.makeSound();
```

```
Rex barks loudly
```

---

# 🏷️ 6. What is `@Override`?

`@Override` is an annotation that tells Java:

> “This method is overriding a parent method”

---

## Why it exists:

* Helps detect mistakes
* Ensures method signature matches parent
* Improves code safety

---

### Example of error detection:

If you write:

```java id="override_error"
@Override
public void makesound() { }
```

Java will error because:

* wrong spelling
* does NOT match parent method

---

# ⚙️ 7. How overriding works internally

When calling:

```java id="runtime_call"
Animal a = new Dog();
a.makeSound();
```

Java decides at **runtime**:

> “Which version of makeSound should I use?”

It picks:

✔ Dog version (not Animal version)

This is called:

> **Dynamic Method Dispatch**

---

# 🧠 8. Why overriding exists

It allows:

* customization of behavior
* flexibility in design
* reuse of structure
* polymorphic behavior (light introduction only)

---

# 💡 9. When to use overriding

Use when:

* Child class needs different behavior
* Parent method is too generic
* You want specialization

---

## Example:

* Animal → makeSound()
* Dog → bark
* Cat → meow

---

# ❌ 10. When NOT to use overriding

Avoid when:

* Behavior is identical → no need to override
* You are forcing differences artificially
* You are breaking logical consistency

---

# ⚠️ 11. Common mistakes

### Mistake 1: Wrong method signature

```java id="wrong_signature"
public void makesound() // ❌ not same as parent
```

---

### Mistake 2: Forgetting @Override

Not required, but dangerous without it.

---

### Mistake 3: Changing meaning completely

Overriding should refine behavior, not break logic.

---

# 🧠 12. Mental model

Think:

> Parent defines WHAT it does
> Child defines HOW it does it

---

# 🧪 Quick check

Make sure you understand:

* What is overriding?
* Why does Dog behave differently from Animal?
* What does `@Override` protect you from?

---

# ✔️ Next Step

Now we learn how to directly access parent class using:

# 👉 Chapter 5 — The `super` Keyword