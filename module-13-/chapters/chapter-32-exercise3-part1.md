# Chapter 32 — Exercise 3: Unique Word Counter (Part 1)

So far in this module, we studied:

* `List` → ordered collections with duplicates allowed.
* `Map` → key/value relationships.
* `Set` → collections where uniqueness matters.

Now we will build an application where duplicates are the problem.

The goal:

> Read a text and count how many unique words exist.

This is a perfect scenario for `Set`.

---

# Exercise Objective

Create a console application that:

* Receives a text.
* Separates words.
* Stores only unique words.
* Displays the number of unique words.
* Displays the unique words.

---

# Example

Input:

```text
Java is powerful and Java is popular
```

---

Words:

```text
Java
is
powerful
and
Java
is
popular
```

---

Unique words:

```text
Java
is
powerful
and
popular
```

---

Result:

```text
Total unique words: 5
```

---

# Why Use Set?

Let's analyze.

---

# Using List

Example:

```java
List<String> words;
```

Stores:

```text id="x5m8q2"
[
Java,
is,
powerful,
and,
Java,
is,
popular
]
```

Duplicates remain.

We would need:

```text id="m7q3p9"
Manual duplicate checking
```

---

# Using Set

Example:

```java
Set<String> words;
```

Stores:

```text id="q8m4x1"
[
Java,
is,
powerful,
and,
popular
]
```

Duplicates disappear automatically.

---

# Set Principle

A Set represents:

> A collection of unique elements.

---

# Set Implementations

Java provides:

```text id="w3m9p5"
Set
 |
 +-- HashSet
 |
 +-- LinkedHashSet
 |
 +-- TreeSet
```

---

For this exercise:

We start with:

```java id="k6x2m8"
HashSet
```

---

# Why HashSet?

Because we only need:

* Uniqueness.
* Fast insertion.
* Fast checking.

We do NOT need:

* Sorting.
* Insertion order.

---

# HashSet Characteristics

Internal structure:

```text id="v4q9m2"
Hash Table
```

---

Operations:

| Operation  | Complexity   |
| ---------- | ------------ |
| add()      | O(1) average |
| contains() | O(1) average |
| remove()   | O(1) average |

---

# Project Structure

Add:

```text id="p7m3x8"
src/
│
├── Main.java
│
├── model/
│
├── service/
│   └── WordCounterService.java
│
└── util/
```

---

# Step 1 — Create WordCounterService

Location:

```text id="d8q4m1"
service/WordCounterService.java
```

---

Create storage:

```java id="n5x7m2"
private Set<String> words =
        new HashSet<>();
```

---

# Why Interface Type?

Prefer:

```java id="r9m4x6"
Set<String>
```

instead of:

```java id="z3q8p1"
HashSet<String>
```

because we depend on behavior.

Later we can change:

```java
Set<String> words =
        new TreeSet<>();
```

without rewriting the service.

---

# Step 2 — Adding Words

Create:

```java id="c5m8q2"
public void addWord(String word){

    words.add(word);

}
```

---

Example:

```java id="y7q3m9"
addWord("Java");
addWord("Java");
```

---

HashSet:

First:

```text id="m2x8p4"
Java
```

Second:

```text id="h6q9v1"
Already exists
```

Ignored.

---

# How Does HashSet Know It Exists?

This is important.

HashSet uses:

```text id="z8m3q5"
hashCode()
+
equals()
```

---

Example:

Adding:

```java id="v5p2x9"
"Java"
```

Java calculates:

```text id="k7m4q8"
hashCode()
```

Finds possible location.

Then checks:

```java id="n3x9m1"
equals()
```

to confirm.

---

# Step 3 — Processing Text

We need:

Input:

```text id="w6m2q4"
Java is powerful
```

Output:

```text id="f9q3x7"
Java
is
powerful
```

---

Create method:

```java id="s5m8p2"
public void processText(String text){

    String[] wordsArray =
            text.split(" ");


    for(String word : wordsArray){

        words.add(word);

    }

}
```

---

# What Does split() Do?

Example:

```java id="u7m3q9"
"Java is great"
```

becomes:

```text id="a5x8m2"
[
Java,
is,
great
]
```

---

# Step 4 — Display Unique Words

Create:

```java id="q4m9x3"
public void displayWords(){

    for(String word : words){

        System.out.println(word);

    }

}
```

---

# Important Observation

HashSet does NOT guarantee order.

Input:

```text id="p8x2m6"
Java
is
great
```

Output may be:

```text id="v3m7q9"
great
Java
is
```

---

Why?

Because HashSet prioritizes:

```text id="m4x8p2"
Fast access
```

not ordering.

---

# Step 5 — Count Unique Words

Create:

```java id="w5q8m3"
public int countUniqueWords(){

    return words.size();

}
```

---

Example:

Stored:

```text id="k9m2x5"
Java
is
great
```

Result:

```text id="h4q7m1"
3
```

---

# Complete Flow

```text id="r8m3q6"
Main

 |
 v

WordCounterService

 |
 v

HashSet<String>

 |
 v

Unique words
```

---

# Testing

Main:

```java id="x6m9q2"
WordCounterService service =
        new WordCounterService();


service.processText(
    "Java is powerful and Java is popular"
);


service.displayWords();


System.out.println(
    service.countUniqueWords()
);
```

---

Possible output:

```text
Java
is
powerful
and
popular

5
```

---

# Current WordCounterService

Implemented:

```text id="z7m3q1"
WordCounterService

+ processText()
+ addWord()
+ displayWords()
+ countUniqueWords()
```

---

# Concepts Practiced

You used:

✅ Set interface
✅ HashSet
✅ Duplicate prevention
✅ hashCode()
✅ equals()
✅ size()
✅ Text processing

---

# Important Design Lesson

Different collections solve different problems:

Student:

```text id="n5x8m2"
Need ordered storage
→ List
```

Product:

```text id="b4q9m7"
Need lookup by ID
→ Map
```

Words:

```text id="p2x7m5"
Need uniqueness
→ Set
```

---

# Exercise Task

Create:

`WordCounterService`

Implement:

* `processText()`
* `addWord()`
* `countUniqueWords()`
* `displayWords()`

Test with:

```text
Java Java Java Collection Framework
```

Expected:

```text
Unique words: 3
```

---

# ✔️ Next Step

In **Chapter 33 — Exercise 3: Unique Word Counter (Part 2)** we will improve the application by adding:

* Case normalization.
* Removing punctuation.
* Comparing `HashSet`, `LinkedHashSet`, and `TreeSet`.
* Understanding when ordering matters.
