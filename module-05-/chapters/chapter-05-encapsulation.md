# 🔒 Chapter 5 — Encapsulation

So far, we've created classes with **publicly accessible attributes**.

Example:

```java
public class Student {

    String name;
    int age;
    double grade;

}
```

This works, but it introduces a major problem:

**Anyone can change the object's data in any way they want.**

For example:

```java
Student student = new Student();

student.age = -10;
student.grade = 500;
student.name = null;
```

These values don't make sense, yet Java allows them.

This is exactly the problem that **encapsulation** solves.

---

# 🧠 1. What is Encapsulation?

**Encapsulation** is the practice of protecting an object's internal data by controlling how it is accessed and modified.

Instead of allowing direct access to attributes, the object decides how its data can be read or changed.

A simple definition is:

> **Hide the data, expose only what is necessary.**

---

# ❓ Why Does Encapsulation Exist?

Imagine a bank account.

Would it be safe if anyone could write:

```java
account.balance = 1000000;
```

Of course not.

The balance should only change through operations like:

* Deposit
* Withdraw

The object should control its own data.

The same idea applies to every class.

---

# 🔓 Without Encapsulation

```java
public class Student {

    String name;
    int age;
    double grade;

}
```

Usage:

```java
Student student = new Student();

student.age = -50;
student.grade = 999;
```

Nothing prevents invalid data.

---

# 🔒 With Encapsulation

We make the attributes **private**.

```java
public class Student {

    private String name;
    private int age;
    private double grade;

}
```

Now this is impossible:

```java
student.age = 20;
```

The compiler will generate an error because the field is private.

Only the `Student` class itself can directly access these attributes.

---

# 🧠 2. Access Modifiers

Access modifiers define who can access a class or its members.

For now, we'll focus on the two most common ones.

## `public`

Accessible from anywhere.

Example:

```java
public void displayInformation() {

}
```

Any class can call this method.

---

## `private`

Accessible only inside the same class.

Example:

```java
private int age;
```

Only methods inside `Student` can directly read or modify `age`.

---

# 🧠 3. Getters

A **getter** is a method that returns the value of a private attribute.

Example:

```java
public String getName() {
    return name;
}
```

Usage:

```java
System.out.println(student.getName());
```

Notice that we no longer access the field directly.

Instead of:

```java
student.name;
```

we use:

```java
student.getName();
```

---

# 🧠 4. Setters

A **setter** is a method that changes the value of a private attribute.

Example:

```java
public void setAge(int age) {
    this.age = age;
}
```

Usage:

```java
student.setAge(20);
```

Instead of writing:

```java
student.age = 20;
```

we now use a controlled method.

---

# 🧠 5. Why Are Setters Better?

Because they allow validation.

Example:

```java
public void setAge(int age) {

    if (age >= 0) {
        this.age = age;
    }

}
```

Now this:

```java
student.setAge(-10);
```

will simply be ignored.

The object protects itself.

---

Another example:

```java
public void setGrade(double grade) {

    if (grade >= 0 && grade <= 10) {
        this.grade = grade;
    }

}
```

Only valid grades are accepted.

---

# 🧠 6. Complete Example

```java
public class Student {

    private String name;
    private int age;
    private double grade;

    public Student(String name, int age, double grade) {
        setName(name);
        setAge(age);
        setGrade(grade);
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {

        if (name != null && !name.isBlank()) {
            this.name = name;
        }

    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {

        if (age >= 0) {
            this.age = age;
        }

    }

    public double getGrade() {
        return grade;
    }

    public void setGrade(double grade) {

        if (grade >= 0 && grade <= 10) {
            this.grade = grade;
        }

    }

    public void displayInformation() {

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Grade: " + grade);

    }

}
```

This is much safer than exposing the attributes directly.

---

# 🧠 7. How Encapsulation Works Internally

When another class executes:

```java
student.setAge(20);
```

Java does **not** modify the attribute directly.

Instead:

1. It calls the `setAge()` method.
2. The method checks the value.
3. If the value is valid, it updates the attribute.
4. Otherwise, it rejects the change.

The object controls its own state.

---

# 🧠 8. When Should You Use Getters and Setters?

As a general rule:

* Keep attributes **private**.
* Provide getters when other classes need to read data.
* Provide setters only when it makes sense to modify the data.

Not every field needs a setter.

For example, an account number might never change after creation.

```java
private String accountNumber;
```

You might provide:

```java
getAccountNumber()
```

but no setter.

This makes the object more secure and predictable.

---

# 🚫 Common Beginner Mistakes

## Making Everything Public

```java
public String name;
public int age;
public double grade;
```

This defeats the purpose of encapsulation.

---

## Setters Without Validation

```java
public void setAge(int age) {
    this.age = age;
}
```

This allows invalid values.

Always think about whether the new value should be accepted.

---

## Returning Internal Data Unnecessarily

Only expose information that other classes actually need.

The less you expose, the easier it is to maintain your code.

---

# 🏗️ Project Structure Reminder

Encapsulation belongs inside the model classes.

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

`Main.java` should interact with objects through their **public methods**, not by directly modifying their attributes.

Example:

```java
Student student = new Student("John", 20, 9.5);

student.setGrade(8.7);

System.out.println(student.getGrade());
```

This keeps responsibilities well separated and protects the object's internal state.

---

# 🧪 Practice Exercise

Upgrade your `Student` class using encapsulation.

### Step 1

Convert all attributes to `private`.

```java
private String name;
private int age;
private double grade;
```

---

### Step 2

Create getters for every attribute.

---

### Step 3

Create setters with validation.

Rules:

* `name` cannot be `null` or blank.
* `age` must be greater than or equal to `0`.
* `grade` must be between `0` and `10`.

---

### Step 4

Update `Main.java`.

Instead of:

```java
student.age = 20;
```

use:

```java
student.setAge(20);
```

Instead of:

```java
System.out.println(student.grade);
```

use:

```java
System.out.println(student.getGrade());
```

Try assigning invalid values and observe how your validation protects the object.

---

# ✔️ Chapter 5 Complete

Congratulations!

You've learned one of the most important principles of Object-Oriented Programming.

You now understand:

* Why encapsulation exists
* How `private` protects an object's internal state
* The purpose of getters and setters
* How validation keeps objects in a valid state
* Why objects should control their own data

Encapsulation is a cornerstone of professional Java development and will be used in nearly every class you create.

## ▶️ Next Step

Continue to **Chapter 6 — The `this` Keyword**, where you'll learn how Java refers to the current object, how `this` resolves naming conflicts, and why it is commonly used in constructors and instance methods.
