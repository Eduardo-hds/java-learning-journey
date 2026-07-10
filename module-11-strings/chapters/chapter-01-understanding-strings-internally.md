# Chapter 01 — Understanding Strings Internally

## Chapter Objective

By the end of this chapter, you should understand:

* What a String actually is in Java
* Why String is a class and not a primitive type
* How text is represented internally
* What immutability means
* Why Java Strings were designed to be immutable
* The advantages and disadvantages of immutable objects
* How immutability affects memory and performance
* Common mistakes caused by misunderstanding Strings

---

# 1. What is a String?

A **String** represents a sequence of characters.

Examples:

```java
"Hello"
"Java"
"Eduardo"
"12345"
"example@email.com"
```

A String can contain:

* letters
* numbers
* symbols
* spaces
* special characters

Example:

```java
String message = "Hello Java";
```

Here:

```text
H e l l o   J a v a
```

is a sequence of characters.

---

However, in Java, a String is **not a primitive type**.

This is different from:

```java
int age = 25;
double price = 10.5;
boolean active = true;
```

Those are primitive values.

A String is an object:

```java
String name = "Java";
```

Behind the scenes:

```
name
 |
 v
+----------------+
| String object  |
|                |
| "Java"         |
+----------------+
```

The variable does not contain the text directly.

It contains a reference to an object.

---

# 2. Why is String a Class?

A common beginner question:

> Why didn't Java create String as a primitive type like int or char?

Example:

Why not:

```java
string name = "Java";
```

like:

```java
int age = 20;
```

The reason is that text requires behavior.

A primitive value only stores data.

Example:

```java
int number = 10;
```

The number itself does not have operations.

But text needs many operations:

```java
name.length();

name.toUpperCase();

name.substring();

name.replace();
```

These operations belong naturally to an object.

A String object contains:

## Data

The characters:

```
Java
```

## Behavior

Operations:

```
length()
replace()
substring()
contains()
```

This is the basic principle of Object-Oriented Programming:

> Objects combine data and behavior.

---

# 3. String as an Object

Let's compare primitive types and objects.

## Primitive

Example:

```java
int age = 30;
```

Memory:

```
age
 |
 v
30
```

The variable directly stores the value.

---

## Object

Example:

```java
String language = "Java";
```

Memory conceptually:

```
language
     |
     v
+-------------+
| String      |
|-------------|
| J a v a     |
+-------------+
```

The variable stores a reference.

---

# 4. Internal Representation of Strings

A String is internally stored as characters.

Conceptually:

```text
String: "Java"

Index:

0 1 2 3
J a v a
```

Each character has a position.

Example:

```java
String word = "Java";

System.out.println(word.charAt(0));
```

Output:

```
J
```

because index `0` contains:

```
J
```

---

Modern Java versions internally optimize String storage.

Historically:

```
char[]
```

was used:

```
[
 'J',
 'a',
 'v',
 'a'
]
```

Modern Java can use a compact representation depending on the characters:

* Latin characters may use less memory
* Other Unicode characters may require more space

The important idea:

A String internally stores encoded character data.

---

# 5. The Most Important Concept: String Immutability

Now we reach the central concept of this module.

## What does immutable mean?

Immutable means:

> An object cannot be changed after it is created.

Once a String exists, its content is fixed forever.

Example:

```java
String name = "Java";
```

The String object contains:

```
Java
```

You cannot transform that same object into:

```
JAVA
```

---

Many beginners expect:

```java
String name = "Java";

name.toUpperCase();

System.out.println(name);
```

Output:

```
Java
```

Why?

Because:

```java
name.toUpperCase();
```

does NOT modify the original object.

It creates a new String.

Conceptually:

```
Before:

name
 |
 v
"Java"


After toUpperCase():

name
 |
 v
"Java"


New object:

"JAVA"
```

The method returns the new object.

Correct:

```java
String name = "Java";

name = name.toUpperCase();

System.out.println(name);
```

Now:

```
JAVA
```

---

# 6. Why Did Java Make Strings Immutable?

This design choice provides several advantages.

---

# Reason 1 — Security

Strings are everywhere in Java:

Examples:

* usernames
* passwords
* database URLs
* file paths
* network addresses

Imagine Strings could change.

Example:

```java
String url = "https://bank.com";
```

A system checks:

```
Is this a trusted address?
```

Then another part of the program changes it:

```
https://evil.com
```

The original validation would no longer be reliable.

Immutable objects cannot silently change.

---

# Reason 2 — String Pool Optimization

Java reuses identical Strings.

Example:

```java
String a = "Java";
String b = "Java";
```

Java can safely do:

```
a ----\
       ---> "Java"
b ----/
```

Because nobody can modify:

```
"Java"
```

If Strings were mutable:

```java
a.changeTo("Python");
```

then:

```
a ----\
       ---> "Python"
b ----/
```

The second variable would unexpectedly change.

Immutability makes sharing safe.

---

# Reason 3 — Thread Safety

Multiple threads can safely access the same String.

Example:

```
Thread A
    |
    v
 "Java"


Thread B
    |
    v
 "Java"
```

Nobody can modify it.

No synchronization is needed.

---

# Reason 4 — Hashing Performance

Strings are frequently used as keys:

Example:

```java
Map<String, Integer> users;
```

Internally, Java calculates a hash:

```
"Java" -> 123456
```

Because Strings never change, the hash remains valid.

If Strings changed:

```
"Java"
   |
   v
"Python"
```

the hash would become incorrect.

---

# 7. Memory Implications

Because Strings are immutable:

Every modification creates a new object.

Example:

```java
String text = "Hello";

text = text + " World";
```

Conceptually:

First:

```
"Hello"
```

Then:

```
"Hello World"
```

The original remains.

Memory:

```
Before:

"Hello"


After:

"Hello"

"Hello World"
```

The old object may later be removed by the Garbage Collector.

---

This is fine for small operations.

Example:

```java
String name = "Java";
```

No problem.

---

But imagine:

```java
String result = "";

for(int i = 0; i < 10000; i++){
    result += i;
}
```

This creates thousands of temporary Strings.

Example:

```
""
"0"
"01"
"012"
"0123"
...
```

This is inefficient.

Later we will learn:

```java
StringBuilder
```

which solves this problem.

---

# 8. Common Beginner Mistakes

---

## Mistake 1 — Thinking methods modify Strings

Wrong:

```java
String text = "java";

text.toUpperCase();

System.out.println(text);
```

Result:

```
java
```

Correct:

```java
text = text.toUpperCase();
```

---

## Mistake 2 — Comparing Strings with ==

Wrong:

```java
if(name == "Java")
```

Why?

Because `==` compares references.

It asks:

> Are these the same object?

Not:

> Do these contain the same text?

Correct:

```java
if(name.equals("Java"))
```

We will study this deeply in the comparison chapter.

---

## Mistake 3 — Excessive concatenation

Avoid:

```java
String text = "";

text += "A";
text += "B";
text += "C";
```

For many operations use:

```java
StringBuilder
```

---

# 9. Practical Demonstration

Create:

```
src/
 └── Main.java
```

Code:

```java
public class Main {

    public static void main(String[] args) {

        String language = "Java";

        System.out.println(language);

        language.toUpperCase();

        System.out.println(language);

        language = language.toUpperCase();

        System.out.println(language);
    }
}
```

Output:

```
Java
Java
JAVA
```

---

# What Happened?

First:

```java
language = "Java";
```

Memory:

```
language
 |
 v
Java
```

---

Then:

```java
language.toUpperCase();
```

Created:

```
JAVA
```

but nobody received it.

The object was discarded.

---

Finally:

```java
language = language.toUpperCase();
```

The reference changed:

Before:

```
language
 |
 v
Java
```

After:

```
language
 |
 v
JAVA
```

---

# Chapter Summary

Today we learned:

✅ String is a class
✅ Strings are objects
✅ Strings store text data
✅ Objects contain data and behavior
✅ Strings are immutable
✅ Methods create new Strings instead of changing existing ones
✅ Immutability improves security, memory sharing, and thread safety
✅ Excessive String modification can impact performance

---

# Key Mental Model

Remember this:

```
A String is not a box containing editable text.

A String is an object containing fixed text.

Any "change" creates another String.
```

---

# ✔️ Next Step

Proceed to:

# Chapter 02 — Creating Strings and the String Pool

Next we will learn:

* String literals
* `new String()`
* Heap memory
* String Pool
* How Java reuses Strings
* Why one way of creating Strings is usually preferred over the other.
