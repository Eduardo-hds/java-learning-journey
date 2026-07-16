# Chapter 33 — Exercise 3: Unique Word Counter (Part 2)

In the previous chapter, we created a basic word counter using:

```java
Set<String>
```

with:

```java
HashSet<String>
```

We learned:

* A Set prevents duplicates.
* HashSet provides fast operations.
* Ordering is not guaranteed.

Now we will make the application closer to a real text analyzer.

We will add:

* Text normalization.
* Removing punctuation.
* Case handling.
* Comparing different Set implementations.

---

# Current Problem

Input:

```text
Java java JAVA, is powerful!
```

Our current program sees:

```text
Java
java
JAVA,
is
powerful!
```

The result:

```text
5 unique words
```

But logically:

```text
Java
java
JAVA
```

are the same word.

And:

```text
powerful!
powerful
```

should also be equal.

---

# Step 1 — Normalize Text

Before storing words, we should clean them.

The process:

```text
Original text

↓

Lowercase

↓

Remove punctuation

↓

Split words

↓

Store in Set
```

---

# Convert to Lowercase

Example:

```java id="t7m2q8"
String word = "JAVA";
```

Apply:

```java id="m4x9p1"
word.toLowerCase();
```

Result:

```text id="k8q3v5"
java
```

---

# Why Do This?

Without normalization:

```text
Java
java
JAVA
```

are different strings.

Because:

```java id="w5m8q2"
"Java".equals("java")
```

returns:

```text id="r3x7n9"
false
```

---

# Step 2 — Remove Punctuation

Example:

Input:

```text id="v8m2q5"
Hello!
```

We want:

```text id="p6x9m3"
hello
```

---

Using:

```java id="n4q8m1"
replaceAll()
```

Example:

```java
word.replaceAll("[^a-z]", "");
```

---

Meaning:

```text
[^a-z]
```

means:

> Remove anything that is not a letter.

---

# Step 3 — Improve processText()

Update:

```java id="x5m9q2"
public void processText(String text){

    String[] wordsArray =
            text.split(" ");


    for(String word : wordsArray){

        String cleanWord =
                word
                .toLowerCase()
                .replaceAll("[^a-z]", "");


        if(!cleanWord.isEmpty()){

            words.add(cleanWord);

        }

    }

}
```

---

# Example

Input:

```text id="q7m3x9"
Java Java, JAVA! Collections
```

Processing:

```text id="k2m8v5"
java
java
java
collections
```

HashSet:

```text id="m9x4q1"
java
collections
```

---

# Step 4 — Comparing Set Implementations

Now we have:

```text id="w8m3p6"
Set
 |
 +-- HashSet
 |
 +-- LinkedHashSet
 |
 +-- TreeSet
```

They all store unique values.

The difference:

> How they organize data.

---

# HashSet

Current:

```java id="z4m8q2"
Set<String> words =
        new HashSet<>();
```

---

Characteristics:

## Ordering

No guaranteed order.

Example:

Input:

```text
java
collection
framework
```

Output:

```text
framework
java
collection
```

Possible.

---

## Performance

Average:

```text id="c7m2x9"
add()       O(1)
contains()  O(1)
remove()    O(1)
```

---

## When to Use

Use when:

* You only care about existence.
* You need speed.
* Order does not matter.

Example:

```text
Check blocked usernames.
```

---

# LinkedHashSet

Change:

```java id="p5x8m3"
Set<String> words =
        new LinkedHashSet<>();
```

---

Internal idea:

It combines:

```text id="h4q9m2"
Hash table
+
Linked list
```

---

Result:

Maintains insertion order.

Input:

```text id="x6m3q8"
java
collection
framework
```

Output:

```text id="v2q7m9"
java
collection
framework
```

---

Performance:

Average:

```text id="z8m4x1"
O(1)
```

---

Extra memory:

Because it stores ordering information.

---

# When to Use LinkedHashSet

When you need:

* Unique elements.
* Original insertion order.

Example:

Recently viewed items:

```text id="q5m8x2"
Movie
Book
Game
```

---

# TreeSet

Change:

```java id="m7x3q9"
Set<String> words =
        new TreeSet<>();
```

---

Internal structure:

Usually:

```text id="a8m4q7"
Red-Black Tree
```

---

Unlike HashSet:

It sorts elements.

Input:

```text id="r5x9m2"
java
collection
framework
```

Output:

```text id="v3q8m6"
collection
framework
java
```

---

Performance:

```text id="s7m2q5"
add()       O(log n)
contains()  O(log n)
remove()    O(log n)
```

---

# Why Slower?

Because TreeSet maintains ordering.

Every insertion requires positioning the element correctly.

---

# Comparison Table

| Feature                   | HashSet    | LinkedHashSet      | TreeSet |
| ------------------------- | ---------- | ------------------ | ------- |
| Unique values             | Yes        | Yes                | Yes     |
| Maintains insertion order | No         | Yes                | No      |
| Sorted                    | No         | No                 | Yes     |
| Performance               | Fastest    | Fast               | Slower  |
| Internal structure        | Hash table | Hash + Linked list | Tree    |

---

# Choosing The Correct Set

Question:

## "Do I need sorting?"

Yes:

```text
TreeSet
```

---

## "Do I need insertion order?"

Yes:

```text
LinkedHashSet
```

---

## "Do I only need uniqueness?"

Yes:

```text
HashSet
```

---

# Step 5 — Modify Application To Compare

Create:

```java
Set<String> hashWords =
        new HashSet<>();

Set<String> linkedWords =
        new LinkedHashSet<>();

Set<String> treeWords =
        new TreeSet<>();
```

Add:

```text
java
collection
framework
```

---

Results:

HashSet:

```text
framework
java
collection
```

---

LinkedHashSet:

```text
java
collection
framework
```

---

TreeSet:

```text
collection
framework
java
```

---

# Important Collection Design Principle

Do not choose collections because:

> "This one is more advanced."

Choose because:

> "This behavior matches the problem."

---

# Word Counter Final Design

For this application:

## Basic Counter

```java
HashSet<String>
```

Best.

Reason:

* No duplicates.
* Fast.
* No ordering needed.

---

## Dictionary Application

Maybe:

```java
TreeSet<String>
```

because words should be alphabetical.

---

## Reading History

Maybe:

```java
LinkedHashSet<String>
```

because order matters.

---

# Exercise Task

Modify the word counter:

Implement:

1. Lowercase conversion.
2. Remove punctuation.
3. Test:

Input:

```text
Java, JAVA java Collection Framework!
```

Expected unique words:

```text
java
collection
framework
```

Then test replacing:

```java
HashSet
```

with:

```java
LinkedHashSet
```

and:

```java
TreeSet
```

Observe the difference.

---

# ✔️ Next Step

In **Chapter 34 — Exercise 4: Task Queue System (Part 1)** we will start learning:

* `Queue`
* FIFO behavior
* `PriorityQueue`
* Processing tasks in order

We will build a task processing simulator.
