# Chapter 36 — Exercise 5: Contact Manager (Part 1)

We have now practiced:

* `List` → Student Management
* `Map<Integer, Product>` → Inventory
* `Set<String>` → Unique Word Counter
* `Queue<Task>` → Task Processing

Now we will return to `Map`, but with a different design.

This time, instead of using:

```java
Map<Integer, Object>
```

we will use:

```java
Map<String, Contact>
```

The key will be the contact name.

---

# Exercise Objective

Create a contact management system.

The system must allow:

* Add contacts.
* Search contacts by name.
* Update phone numbers.
* Remove contacts.
* List all contacts.

---

# Why Use Map?

Let's analyze the problem.

A contact manager works mainly like:

> "I know the person's name. Find their information."

Example:

Input:

```text id="m8q3x5"
John
```

Return:

```text id="v4n9p2"
John
555-1234
```

This is a key/value relationship.

---

# Data Structure Choice

Possible designs:

---

## Option 1 — List

```java id="q5m8x3"
List<Contact>
```

Data:

```text id="x8m2p6"
[
 John,
 Maria,
 Carlos
]
```

Search:

```java id="n7q3m9"
find("Maria")
```

Requires:

```text id="p4m8x1"
loop through everything
```

Complexity:

```text id="z6m3q8"
O(n)
```

---

## Option 2 — Map

```java id="r5q8m2"
Map<String, Contact>
```

Structure:

```text id="w3m9x6"
Name        Contact

John   →    Contact Object
Maria  →    Contact Object
```

Search:

```java id="k8q2m5"
contacts.get("John");
```

Average:

```text id="s7m3x9"
O(1)
```

---

# Project Structure

Add:

```text id="q4m8x7"
src/
│
├── Main.java
│
├── model/
│   └── Contact.java
│
├── service/
│   └── ContactService.java
│
└── util/
```

---

# Step 1 — Create Contact Model

Location:

```text id="h5m9x3"
model/Contact.java
```

---

Attributes:

```java id="z8m4q1"
public class Contact {

    private String name;
    private String phone;

}
```

---

# Why Only These Fields?

A contact has:

Identity:

```text id="v7m2x5"
name
```

Information:

```text id="c9q3m8"
phone
```

The name will become the Map key.

---

# Step 2 — Constructor

```java id="p6m3x9"
public Contact(
        String name,
        String phone){

    this.name = name;
    this.phone = phone;

}
```

---

# Step 3 — Getters

Name:

```java id="x4m8q2"
public String getName(){

    return name;

}
```

---

Phone:

```java id="m7q3x5"
public String getPhone(){

    return phone;

}
```

---

# Step 4 — Update Phone Method

We should not directly modify:

```java id="y8m2q6"
contact.phone
```

Instead:

```java id="r3m9x1"
public void updatePhone(
        String phone){

    this.phone = phone;

}
```

---

# Step 5 — toString()

Add:

```java id="n5q8m3"
@Override
public String toString(){

    return "Contact{" +
            "name='" + name + '\'' +
            ", phone='" + phone + '\'' +
            '}';

}
```

---

# Step 6 — Create ContactService

Location:

```text id="v6m2x8"
service/ContactService.java
```

---

Create Map:

```java id="p8q3m5"
private Map<String, Contact> contacts =
        new HashMap<>();
```

---

# Why Interface Type?

Prefer:

```java id="m4x9q2"
Map<String, Contact>
```

instead of:

```java id="z7m3x8"
HashMap<String, Contact>
```

---

Because later we could change:

```java
Map<String, Contact> contacts =
        new TreeMap<>();
```

and automatically get sorted names.

---

# Step 7 — Add Contact

Method:

```java id="s5m8x3"
public void addContact(Contact contact){

    contacts.put(
        contact.getName(),
        contact
    );

}
```

---

Example:

```java id="h8q2m4"
Contact john =
    new Contact(
        "John",
        "555-1234"
    );


addContact(john);
```

---

Map:

```text id="x6m3q9"
John → Contact Object
```

---

# Duplicate Names Problem

What happens?

```java id="q7m2x5"
addContact(
    new Contact(
        "John",
        "9999"
    )
);
```

---

HashMap behavior:

The old value is replaced.

Before:

```text id="n8q4m6"
John → 555-1234
```

After:

```text id="w5m9x2"
John → 9999
```

---

# Preventing Duplicate Contacts

Business rule:

> A contact name cannot already exist.

Use:

```java id="c3m8q7"
public boolean addContact(Contact contact){

    if(contacts.containsKey(
            contact.getName())){

        return false;

    }


    contacts.put(
        contact.getName(),
        contact
    );


    return true;

}
```

---

# containsKey()

Important Map operation:

```java id="r9m3x6"
contacts.containsKey(name)
```

Checks if the key exists.

Complexity:

Average:

```text id="k5q8m1"
O(1)
```

---

# Step 8 — Search Contact

Method:

```java id="t7m2x9"
public Contact findByName(String name){

    return contacts.get(name);

}
```

---

Example:

```java id="p4m8x3"
Contact contact =
        service.findByName(
            "John"
        );
```

---

Result:

```text id="w6m3q8"
Contact{name='John', phone='555-1234'}
```

---

# Step 9 — Update Phone

Method:

```java id="m9q2x5"
public void updatePhone(
        String name,
        String newPhone){

    Contact contact =
            contacts.get(name);


    if(contact != null){

        contact.updatePhone(
            newPhone
        );

    }

}
```

---

# Flow

Search:

```java
contacts.get("John")
```

returns:

```text id="z4m8q1"
Contact Object
```

Then:

```java
updatePhone()
```

changes the object.

---

# Current ContactService

Implemented:

```text id="b7m3x9"
ContactService

+ addContact()
+ findByName()
+ updatePhone()
```

---

# Comparing Map Uses

We have now used Map in three different domains:

---

# Product Inventory

```java id="x2m8q5"
Map<Integer, Product>
```

Key:

```text id
```

Reason:

Fast lookup by identifier.

---

# Contact Manager

```java id="v9m3q7"
Map<String, Contact>
```

Key:

```text name
```

Reason:

Fast lookup by natural identifier.

---

# Student Alternative

Could be:

```java id="n4q8m2"
Map<Integer, Student>
```

Key:

```text student ID
```

---

# Important Lesson

The key choice is the most important Map decision.

Ask:

> "What information uniquely identifies this object?"

That becomes the key.

---

# Exercise Task

Create:

### Contact.java

Implement:

* Fields.
* Constructor.
* Getters.
* updatePhone().
* toString().

---

### ContactService.java

Implement:

* `Map<String, Contact>`
* `addContact()`
* `findByName()`
* `updatePhone()`

---

Test:

Add:

```text id="m6x3q9"
John → 1111
Maria → 2222
```

Search:

```text id="q8m4x2"
John
```

Update:

```text id="r5m9p1"
John → 9999
```

---

# ✔️ Next Step

In **Chapter 37 — Exercise 5: Contact Manager (Part 2)** we will complete the system:

* Remove contacts.
* List contacts using `entrySet()`.
* Compare `HashMap`, `LinkedHashMap`, and `TreeMap`.
* Decide which Map implementation fits each scenario.
