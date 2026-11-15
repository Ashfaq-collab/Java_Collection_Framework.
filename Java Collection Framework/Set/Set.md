# Java Collection Framework – Set Interface

## 1. What is Set?

- Set is an interface in the Java Collection Framework.
- It is used to store unique elements.
- It does not allow duplicate elements.
- It does not support index-based access.
- Set extends the Collection interface.
- We cannot create an object directly for Set because it is an interface.

```java
Set<Integer> set = new HashSet<>();
```

### Set Hierarchy

```text
Iterable
   |
Collection
   |
  Set
   |
   |-- HashSet
   |
   |-- LinkedHashSet
   |
   |-- SortedSet
          |
      NavigableSet
          |
        TreeSet
```

---

## 2. Types of Set

There are three commonly used Set implementations:

1. HashSet
2. LinkedHashSet
3. TreeSet

### Comparison

| Feature | HashSet | LinkedHashSet | TreeSet |
|---|---|---|---|
| Duplicates | Not allowed | Not allowed | Not allowed |
| Ordering | No guaranteed order | Insertion order | Sorted order |
| Internal structure | HashMap | LinkedHashMap | TreeMap |
| Null values | One null | One null | Not allowed with natural ordering |
| Add complexity | O(1) average | O(1) average | O(log n) |
| Search complexity | O(1) average | O(1) average | O(log n) |
| Remove complexity | O(1) average | O(1) average | O(log n) |
| Synchronized | No | No | No |

---

# 3. HashSet

HashSet is a class that implements the Set interface.

### Characteristics

- Does not allow duplicate elements.
- Does not maintain insertion order.
- Allows one null element.
- Uses HashMap internally.
- Average O(1) time complexity for add, remove and contains.
- Not synchronized by default.

### Example

```java
HashSet<Integer> set = new HashSet<>();

set.add(10);
set.add(20);
set.add(30);
set.add(10);

System.out.println(set);
```

Output (order may vary):

```text
[10, 20, 30]
```

### Internal Working of HashSet

HashSet internally uses HashMap.

Conceptually:

```java
HashMap<E, Object> map;
```

When we execute:

```java
set.add(10);
```

It internally performs an operation similar to:

```java
map.put(10, PRESENT);
```

- Element is stored as a key.
- A dummy object is stored as the value.
- HashMap keys are unique, so duplicate elements are prevented.

### How HashSet Identifies Duplicates

HashSet uses two methods:

1. hashCode()
2. equals()

Working:

1. Calculates the hash code of the element.
2. Finds the appropriate bucket.
3. Checks elements in that bucket.
4. Uses equals() to identify duplicates.
5. If an equal element exists, the new element is not added.

**Important rules:**

- Equal objects must have the same hash code.
- Objects with the same hash code are not necessarily equal.
- Override both equals() and hashCode() when implementing logical equality for custom objects.

### Example

```java
class Student {
    int id;

    Student(int id) {
        this.id = id;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (!(obj instanceof Student)) return false;

        Student s = (Student) obj;
        return this.id == s.id;
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}
```

---

# 4. LinkedHashSet

LinkedHashSet is a class that implements the Set interface.

It is similar to HashSet, but maintains insertion order.

### Characteristics

- Does not allow duplicates.
- Maintains insertion order.
- Allows one null element.
- Uses LinkedHashMap internally.
- Average O(1) time complexity for add, remove and contains.
- Not synchronized by default.

### Example

```java
LinkedHashSet<Integer> set = new LinkedHashSet<>();

set.add(50);
set.add(10);
set.add(30);
set.add(20);
set.add(10);

System.out.println(set);
```

Output:

```text
[50, 10, 30, 20]
```

### Internal Working

LinkedHashSet uses a linked hash map internally.

It combines:

- Hashing for fast searching.
- Doubly linked list for maintaining insertion order.

### Important Use Case

Removing duplicates while preserving insertion order.

```java
ArrayList<Integer> list = new ArrayList<>();

list.add(10);
list.add(20);
list.add(10);
list.add(30);
list.add(20);

LinkedHashSet<Integer> set = new LinkedHashSet<>(list);

System.out.println(set);
```

Output:

```text
[10, 20, 30]
```

---

# 5. TreeSet

TreeSet implements NavigableSet, which extends SortedSet and Set.

It stores unique elements in sorted order.

### Characteristics

- Does not allow duplicates.
- Maintains sorted order.
- Does not allow null with natural ordering.
- Uses TreeMap internally.
- Based on a Red-Black Tree.
- Add, remove and contains take O(log n).
- Not synchronized by default.

### Example

```java
TreeSet<Integer> set = new TreeSet<>();

set.add(50);
set.add(10);
set.add(30);
set.add(20);
set.add(10);

System.out.println(set);
```

Output:

```text
[10, 20, 30, 50]
```

### Internal Working

TreeSet uses TreeMap internally.

TreeMap uses a Red-Black Tree, which is a self-balancing binary search tree.

### Custom Sorting

Descending order:

```java
TreeSet<Integer> set =
    new TreeSet<>(Comparator.reverseOrder());
```

Using lambda:

```java
TreeSet<Integer> set =
    new TreeSet<>((a, b) -> Integer.compare(b, a));
```

### TreeSet with Custom Objects

TreeSet needs a comparison mechanism for custom objects.

We can use:

- Comparable
- Comparator

If the comparison result is 0, TreeSet treats the objects as equivalent and stores only one of them.

---

# 6. Important Methods of HashSet

HashSet mainly uses methods inherited from the Set and Collection interfaces.

| Method | Description |
|---|---|
| add(E e) | Adds an element |
| addAll(Collection c) | Adds all elements |
| remove(Object o) | Removes an element |
| removeAll(Collection c) | Removes matching elements |
| retainAll(Collection c) | Keeps common elements |
| contains(Object o) | Checks element existence |
| containsAll(Collection c) | Checks all elements |
| size() | Returns number of elements |
| isEmpty() | Checks whether empty |
| clear() | Removes all elements |
| iterator() | Returns Iterator |
| toArray() | Converts Set into array |
| forEach() | Iterates using lambda |

---

# 7. Important Methods of LinkedHashSet

LinkedHashSet supports the same commonly used methods as HashSet.

| Method | Description |
|---|---|
| add(E e) | Adds an element |
| addAll(Collection c) | Adds all elements |
| remove(Object o) | Removes an element |
| removeAll(Collection c) | Removes matching elements |
| retainAll(Collection c) | Keeps common elements |
| contains(Object o) | Checks element existence |
| containsAll(Collection c) | Checks all elements |
| size() | Returns number of elements |
| isEmpty() | Checks whether empty |
| clear() | Removes all elements |
| iterator() | Returns Iterator |
| forEach() | Iterates in insertion order |

**Remember:** LinkedHashSet's main advantage is maintaining insertion order.

---

# 8. Important Methods of TreeSet

TreeSet supports common Set methods plus additional navigation and range methods.

### A. Basic Methods

| Method | Description |
|---|---|
| add() | Adds an element |
| addAll() | Adds all elements |
| remove() | Removes an element |
| removeAll() | Removes matching elements |
| retainAll() | Keeps common elements |
| contains() | Checks element existence |
| size() | Returns size |
| isEmpty() | Checks whether empty |
| clear() | Removes all elements |

### B. Navigation Methods

Assume:

```java
TreeSet<Integer> set = new TreeSet<>(
    Arrays.asList(10, 20, 30, 40, 50)
);
```

| Method | Description | Example output |
|---|---|---|
| first() | Smallest element | 10 |
| last() | Largest element | 50 |
| higher(20) | Smallest element strictly greater than 20 | 30 |
| lower(20) | Largest element strictly smaller than 20 | 10 |
| ceiling(25) | Smallest element >= 25 | 30 |
| floor(25) | Largest element <= 25 | 20 |
| pollFirst() | Retrieves and removes smallest element | 10 |
| pollLast() | Retrieves and removes largest element | 50 |
| descendingSet() | Returns reverse-order view | [50, 40, 30, 20, 10] |
| descendingIterator() | Returns reverse iterator | Reverse traversal |

### C. Range Methods

| Method | Description |
|---|---|
| headSet(30) | Elements smaller than 30 |
| tailSet(30) | Elements greater than or equal to 30 |
| subSet(20, 50) | Elements from 20 inclusive to 50 exclusive |

Examples:

```java
set.headSet(30); 
// [10, 20]

set.tailSet(30);
// [30, 40, 50]

set.subSet(20, 50);
// [20, 30, 40]
```

Specify inclusive/exclusive boundaries:

```java
set.subSet(20, true, 50, true);
```

Output:

```text
[20, 30, 40, 50]
```

---

# 9. Different Ways of Iterating a Set

Consider:

```java
Set<Integer> set = new LinkedHashSet<>(
    Arrays.asList(10, 20, 30, 40)
);
```

### 1. Enhanced For Loop

```java
for (Integer num : set) {
    System.out.println(num);
}
```

- Simple syntax.
- Easy to understand.
- Cannot safely remove elements directly during iteration.

### 2. Iterator

```java
Iterator<Integer> itr = set.iterator();

while (itr.hasNext()) {
    System.out.println(itr.next());
}
```

Important Iterator methods:

| Method | Description |
|---|---|
| hasNext() | Checks whether next element exists |
| next() | Returns next element |
| remove() | Safely removes current element |

Removing elements using Iterator:

```java
Iterator<Integer> itr = set.iterator();

while (itr.hasNext()) {
    int num = itr.next();

    if (num == 20) {
        itr.remove();
    }
}
```

### 3. forEach() with Lambda

```java
set.forEach(num -> {
    System.out.println(num);
});
```

Short version:

```java
set.forEach(num -> System.out.println(num));
```

### 4. Method Reference

```java
set.forEach(System.out::println);
```

This is a shorter form of lambda-based iteration.

### 5. Stream API

```java
set.stream()
   .forEach(num -> System.out.println(num));
```

Filtering even numbers:

```java
set.stream()
   .filter(num -> num % 2 == 0)
   .forEach(System.out::println);
```

### 6. Spliterator

```java
Spliterator<Integer> spliterator = set.spliterator();

spliterator.forEachRemaining(System.out::println);
```

Important methods:

| Method | Description |
|---|---|
| tryAdvance() | Processes one element |
| forEachRemaining() | Processes remaining elements |
| trySplit() | Attempts to split elements |
| estimateSize() | Estimates remaining elements |

### Iteration Comparison

| Method | Java version | Main use |
|---|---|---|
| Enhanced for loop | Java 5 | Simple iteration |
| Iterator | Java 1.2 | Iteration and safe removal |
| forEach() | Java 8 | Lambda iteration |
| Method reference | Java 8 | Shorter syntax |
| Stream API | Java 8 | Filtering and processing |
| Spliterator | Java 8 | Traversal and splitting |

---

# 10. Set Operations

There are three important mathematical operations.

### A. Union

Combines all elements from both Sets without duplicates.

```java
A.addAll(B);
```

### B. Intersection

Finds common elements between two Sets.

```java
A.retainAll(B);
```

### C. Difference

Finds elements present in A but not in B.

```java
A.removeAll(B);
```

### Quick Revision

| Operation | Java method |
|---|---|
| Union | addAll() |
| Intersection | retainAll() |
| Difference | removeAll() |

Note: These operations modify the Set on which the method is called.

---

# 11. Important Concepts

### A. Null Values

| Implementation | Null allowed? |
|---|---|
| HashSet | One null |
| LinkedHashSet | One null |
| TreeSet | No null with natural ordering |

### B. Synchronization

HashSet, LinkedHashSet and TreeSet are not synchronized by default.

Synchronized Set:

```java
Set<Integer> set =
    Collections.synchronizedSet(new HashSet<>());
```

Concurrent Set:

```java
Set<Integer> set =
    ConcurrentHashMap.newKeySet();
```

### C. Fail-Fast Behavior

HashSet and LinkedHashSet iterators are generally fail-fast.

Structural modification outside the iterator while iterating may result in ConcurrentModificationException.

Unsafe:

```java
for (Integer num : set) {
    if (num == 20) {
        set.remove(num);
    }
}
```

Safe:

```java
Iterator<Integer> itr = set.iterator();

while (itr.hasNext()) {
    Integer num = itr.next();

    if (num == 20) {
        itr.remove();
    }
}
```

Fail-fast behavior is best-effort, not guaranteed.

---

# 12. Common Coding Problems Using Set

### Problem 1: Remove Duplicates from an Array

```java
int[] arr = {10, 20, 10, 30, 20, 40};

Set<Integer> set = new LinkedHashSet<>();

for (int num : arr) {
    set.add(num);
}

System.out.println(set);
```

Output:

```text
[10, 20, 30, 40]
```

### Problem 2: Find Duplicate Elements

```java
int[] arr = {10, 20, 30, 10, 40, 20};

Set<Integer> seen = new HashSet<>();
Set<Integer> duplicates = new LinkedHashSet<>();

for (int num : arr) {
    if (!seen.add(num)) {
        duplicates.add(num);
    }
}

System.out.println(duplicates);
```

Output:

```text
[10, 20]
```

### Problem 3: Find Common Elements Between Two Arrays

```java
int[] a = {10, 20, 30, 40};
int[] b = {30, 40, 50, 60};

Set<Integer> set = new HashSet<>();

for (int num : a) {
    set.add(num);
}

for (int num : b) {
    if (set.contains(num)) {
        System.out.println(num);
    }
}
```

Output:

```text
30
40
```

### Problem 4: Check Whether Two Arrays Have the Same Unique Elements

```java
int[] a = {10, 20, 30, 20};
int[] b = {30, 10, 20};

Set<Integer> s1 = new HashSet<>();
Set<Integer> s2 = new HashSet<>();

for (int num : a) {
    s1.add(num);
}

for (int num : b) {
    s2.add(num);
}

System.out.println(s1.equals(s2));
```

Output:

```text
true
```

Note: This checks unique elements, not frequencies.

---

# 13. Important Java Interview Questions

1. What is Set in Java?
2. Why doesn't Set allow duplicates?
3. What is the difference between List and Set?
4. What is the difference between HashSet and LinkedHashSet?
5. What is the difference between HashSet and TreeSet?
6. How does HashSet work internally?
7. How does HashSet identify duplicate objects?
8. What is the relationship between equals() and hashCode()?
9. Can HashSet contain null?
10. Why doesn't TreeSet allow null with natural ordering?
11. What is the internal data structure of TreeSet?
12. How do you sort elements in descending order using TreeSet?
13. What happens when a Comparator returns 0?
14. Can we store custom objects in HashSet?
15. What is the difference between Comparable and Comparator?
16. Is HashSet synchronized?
17. What is fail-fast behavior?
18. How do you remove duplicates from an ArrayList using Set?
19. How do you find common elements between two Sets?
20. What is the difference between SortedSet and NavigableSet?

---

# 14. Final Quick Revision

| Topic | Must Remember |
|---|---|
| Set | Stores unique elements |
| HashSet | No guaranteed order |
| LinkedHashSet | Insertion order |
| TreeSet | Sorted order |
| HashSet internal structure | HashMap |
| LinkedHashSet internal structure | LinkedHashMap |
| TreeSet internal structure | TreeMap |
| HashSet complexity | O(1) average |
| LinkedHashSet complexity | O(1) average |
| TreeSet complexity | O(log n) |
| Duplicate detection in HashSet | hashCode() and equals() |
| TreeSet sorting | Comparable / Comparator |
| Union | addAll() |
| Intersection | retainAll() |
| Difference | removeAll() |

## Placement Preparation Priority

1. Understand HashSet internal working.
2. Learn equals() and hashCode().
3. Understand differences between HashSet, LinkedHashSet and TreeSet.
4. Practise all common Set methods.
5. Master TreeSet navigation methods.
6. Practise all four Set coding problems.
7. Learn the different iteration techniques.

**Most important methods to remember:**

```java
// Common Set methods
add()
addAll()
remove()
removeAll()
retainAll()
contains()
containsAll()
size()
isEmpty()
clear()
iterator()
forEach()

// Special TreeSet methods
first()
last()
higher()
lower()
ceiling()
floor()
pollFirst()
pollLast()
headSet()
tailSet()
subSet()
descendingSet()
descendingIterator()
```

**End of Set Interface Notes.**