# Java Map – Complete Notes

## 1. Introduction to Map

- `Map` is an interface in the Java Collection Framework.
- It stores data in **key-value pairs**.
- Each key must be unique.
- Values can be duplicated.
- One key can map to only one value at a time.
- `Map` does not extend the `Collection` interface.

### Example

```java
Map<Integer, String> map = new HashMap<>();

map.put(101, "Ashfaq");
map.put(102, "Rahul");
map.put(103, "John");
```

### Important Points

| Feature | Description |
|---|---|
| Storage | Key-value pairs |
| Duplicate keys | Not allowed |
| Duplicate values | Allowed |
| Key | Unique |
| Value | Can be duplicated |
| Null support | Depends on implementation |
| Ordering | Depends on implementation |

---

## 2. Map Implementations

The important Map implementations are:

1. HashMap
2. LinkedHashMap
3. TreeMap
4. Hashtable
5. ConcurrentHashMap

### Comparison of Map Implementations

| Feature | HashMap | LinkedHashMap | TreeMap | Hashtable | ConcurrentHashMap |
|---|---|---|---|---|---|
| Ordering | No guarantee | Insertion order | Sorted order | No guarantee | No guarantee |
| Null key | One | One | Generally no* | No | No |
| Null values | Allowed | Allowed | Allowed | No | No |
| Thread-safe | No | No | No | Yes | Yes |
| Internal structure | Hash table | Hash table + linked list | Red-Black tree | Hash table | Concurrent hash table |
| Performance | Average O(1) | Average O(1) | O(log n) | Average O(1) | Average O(1) |
| Introduced | Java 1.2 | Java 1.4 | Java 1.2 | Java 1.0 | Java 1.5 |

*TreeMap can support null keys with a suitable custom Comparator.

---

# 3. HashMap

## Introduction

- HashMap implements the Map interface.
- It stores data in key-value pairs.
- It does not guarantee insertion or sorted order.
- It allows one null key and multiple null values.
- It is not synchronized (not thread-safe).
- Average time complexity for basic operations is O(1), assuming good hash distribution.

### Example

```java
HashMap<Integer, String> map = new HashMap<>();

map.put(101, "Ashfaq");
map.put(102, "Rahul");
map.put(103, "John");

System.out.println(map);
```

## Internal Working of HashMap

HashMap internally uses:

- Array of buckets.
- Linked lists for handling collisions.
- Red-Black trees for certain heavily-collided buckets.

### How put() works

1. Calculate the key's `hashCode()`.
2. Apply a hash-spreading operation.
3. Calculate the bucket index.
4. Check whether the bucket is empty.
5. If empty, insert the entry.
6. If occupied, compare keys using `equals()`.
7. Update the value if the key already exists; otherwise, handle the collision by adding another entry.

### Hash Collision

A hash collision occurs when two different keys map to the same bucket.

### equals() and hashCode() Contract

- If two objects are equal according to `equals()`, they must have the same `hashCode()`.
- Two objects having the same hash code need not be equal.

## HashMap Capacity and Load Factor

| Concept | Default value |
|---|---|
| Initial capacity | 16 |
| Load factor | 0.75 |
| Initial resize threshold | 12 |

Formula:

```text
Threshold = Capacity × Load Factor
```

Example:

```text
16 × 0.75 = 12
```

When the number of entries exceeds the threshold, HashMap resizes its internal table.

In common Java implementations, capacity generally doubles during resizing.

### Treeification

In modern Java implementations:

- Treeification threshold: 8.
- Minimum capacity for treeification: 64.
- Untreeification threshold: 6.

These are implementation details, not guaranteed API specifications.

## HashMap Constructors

```java
HashMap<K, V> map = new HashMap<>();

HashMap<K, V> map = new HashMap<>(20);

HashMap<K, V> map = new HashMap<>(20, 0.75f);

HashMap<K, V> map = new HashMap<>(anotherMap);
```

## Important HashMap Methods

| Method | Purpose |
|---|---|
| `put()` | Adds or updates a key-value pair |
| `putAll()` | Copies all entries from another Map |
| `putIfAbsent()` | Inserts if the key is absent or mapped to null |
| `get()` | Retrieves a value using a key |
| `getOrDefault()` | Returns a default value if no mapping exists |
| `remove(key)` | Removes an entry using its key |
| `remove(key, value)` | Removes only if both key and value match |
| `replace()` | Replaces an existing value |
| `containsKey()` | Checks whether a key exists |
| `containsValue()` | Checks whether a value exists |
| `keySet()` | Returns all keys |
| `values()` | Returns all values |
| `entrySet()` | Returns all key-value entries |
| `size()` | Returns the number of entries |
| `isEmpty()` | Checks whether Map is empty |
| `clear()` | Removes all entries |
| `forEach()` | Iterates through entries |
| `compute()` | Computes a new value for a key |
| `computeIfAbsent()` | Computes a value if absent or mapped to null |
| `computeIfPresent()` | Computes a value if currently mapped to a non-null value |
| `merge()` | Combines a new value with an existing mapping |
| `clone()` | Creates a shallow copy |

### Important Examples

**getOrDefault()**

```java
Map<String, Integer> map = new HashMap<>();

map.put("Java", 10);

System.out.println(map.getOrDefault("Java", 0)); 
// 10

System.out.println(map.getOrDefault("Python", 0));
// 0
```

**putIfAbsent()**

```java
map.putIfAbsent("Java", 20);
map.putIfAbsent("Python", 30);
```

**computeIfAbsent()**

```java
map.computeIfAbsent("C++", key -> 40);
```

**merge()**

```java
Map<String, Integer> map = new HashMap<>();

map.merge("Java", 1, Integer::sum);
map.merge("Java", 1, Integer::sum);

System.out.println(map.get("Java")); // 2
```

### Placement Tip: Frequency Counting

```java
String str = "banana";

Map<Character, Integer> map = new HashMap<>();

for (char ch : str.toCharArray()) {
    map.put(ch, map.getOrDefault(ch, 0) + 1);
}

System.out.println(map);
```

---

# 4. LinkedHashMap

## Introduction

- LinkedHashMap extends HashMap.
- It maintains insertion order by default.
- It allows one null key and multiple null values.
- It is not synchronized.
- It uses a hash table and a doubly linked list.

### Example

```java
LinkedHashMap<Integer, String> map = new LinkedHashMap<>();

map.put(103, "John");
map.put(101, "Ashfaq");
map.put(102, "Rahul");

System.out.println(map);
```

Output:

```text
{103=John, 101=Ashfaq, 102=Rahul}
```

## Insertion Order

LinkedHashMap remembers the order in which entries were inserted.

## Access Order

LinkedHashMap can also maintain access order.

```java
LinkedHashMap<Integer, String> map =
    new LinkedHashMap<>(16, 0.75f, true);
```

Here, `true` enables access-order mode.

When an entry is accessed, it moves towards the most recently accessed position.

## Important LinkedHashMap Methods

LinkedHashMap inherits most methods from HashMap.

| Method | Purpose |
|---|---|
| `put()` | Inserts or updates an entry |
| `get()` | Retrieves a value |
| `getOrDefault()` | Retrieves a value or default |
| `putIfAbsent()` | Inserts if absent or mapped to null |
| `remove()` | Removes an entry |
| `replace()` | Replaces an existing value |
| `containsKey()` | Checks key existence |
| `containsValue()` | Checks value existence |
| `keySet()` | Returns keys |
| `values()` | Returns values |
| `entrySet()` | Returns entries |
| `forEach()` | Iterates through entries |
| `compute()` | Computes a value |
| `computeIfAbsent()` | Computes if absent or mapped to null |
| `computeIfPresent()` | Computes if mapped to a non-null value |
| `merge()` | Combines values |
| `clear()` | Removes all entries |
| `removeEldestEntry()` | Allows automatic removal of the eldest entry |

## Special Method: removeEldestEntry()

This protected method can be overridden to create a bounded Map or an LRU cache.

### LRU Cache Example

```java
LinkedHashMap<Integer, String> map =
    new LinkedHashMap<>(16, 0.75f, true) {

        @Override
        protected boolean removeEldestEntry(
            Map.Entry<Integer, String> eldest) {

            return size() > 3;
        }
    };

map.put(1, "A");
map.put(2, "B");
map.put(3, "C");
map.put(4, "D");

System.out.println(map);
```

The eldest entry is automatically removed when the size exceeds 3.

---

# 5. TreeMap

## Introduction

- TreeMap implements NavigableMap.
- It stores entries in sorted order of keys.
- It uses a Red-Black tree internally.
- It does not generally allow null keys with natural ordering.
- It allows null values.
- Basic operations take O(log n) time.

### Example

```java
TreeMap<Integer, String> map = new TreeMap<>();

map.put(30, "John");
map.put(10, "Ashfaq");
map.put(20, "Rahul");

System.out.println(map);
```

Output:

```text
{10=Ashfaq, 20=Rahul, 30=John}
```

## Red-Black Tree

A Red-Black tree is a self-balancing Binary Search Tree.

Important properties:

1. Every node is either red or black.
2. Root is black.
3. Red nodes cannot have red children.
4. Every path from a node to its descendant null leaves has the same number of black nodes.
5. The tree maintains balance using rotations and recoloring.

## Important TreeMap Methods

### Basic Methods

| Method | Purpose |
|---|---|
| `put()` | Inserts or updates an entry |
| `get()` | Retrieves a value |
| `remove()` | Removes an entry |
| `containsKey()` | Checks key existence |
| `containsValue()` | Checks value existence |
| `firstKey()` | Returns the smallest key |
| `lastKey()` | Returns the largest key |
| `firstEntry()` | Returns the smallest key-value entry |
| `lastEntry()` | Returns the largest key-value entry |

### Navigation Methods

| Method | Purpose |
|---|---|
| `lowerKey(key)` | Greatest key strictly smaller than given key |
| `higherKey(key)` | Smallest key strictly greater than given key |
| `floorKey(key)` | Greatest key less than or equal to given key |
| `ceilingKey(key)` | Smallest key greater than or equal to given key |
| `lowerEntry(key)` | Entry with greatest key strictly smaller |
| `higherEntry(key)` | Entry with smallest key strictly greater |
| `floorEntry(key)` | Entry with greatest key less than or equal |
| `ceilingEntry(key)` | Entry with smallest key greater than or equal |
| `pollFirstEntry()` | Retrieves and removes the smallest entry |
| `pollLastEntry()` | Retrieves and removes the largest entry |

### Example

```java
TreeMap<Integer, String> map = new TreeMap<>();

map.put(10, "A");
map.put(20, "B");
map.put(30, "C");
map.put(40, "D");
map.put(50, "E");

System.out.println(map.lowerKey(30));   // 20
System.out.println(map.higherKey(30));  // 40
System.out.println(map.floorKey(30));   // 30
System.out.println(map.ceilingKey(35)); // 40
```

### Range Methods

| Method | Purpose |
|---|---|
| `subMap()` | Returns a range of entries |
| `headMap()` | Returns entries smaller than a given key |
| `tailMap()` | Returns entries greater than or equal to a given key |
| `descendingMap()` | Returns entries in descending key order |
| `descendingKeySet()` | Returns keys in descending order |

Example:

```java
TreeMap<Integer, String> map = new TreeMap<>();

map.put(10, "A");
map.put(20, "B");
map.put(30, "C");
map.put(40, "D");
map.put(50, "E");

System.out.println(map.subMap(20, 40));
System.out.println(map.headMap(30));
System.out.println(map.tailMap(30));
System.out.println(map.descendingMap());
```

Note: Range methods return backed views of the original Map, not independent copies.

## Custom Comparator

```java
TreeMap<Integer, String> map =
    new TreeMap<>(Comparator.reverseOrder());

map.put(10, "A");
map.put(20, "B");
map.put(30, "C");

System.out.println(map);
```

Output:

```text
{30=C, 20=B, 10=A}
```

---

# 6. Hashtable

## Introduction

- Hashtable is a legacy Map implementation.
- It was introduced in Java 1.0.
- It is synchronized.
- It does not allow null keys or null values.
- It does not guarantee insertion or sorted order.
- Its individual methods are synchronized, but a sequence of multiple operations is not automatically atomic.

### Example

```java
Hashtable<Integer, String> map = new Hashtable<>();

map.put(101, "Ashfaq");
map.put(102, "Rahul");
map.put(103, "John");

System.out.println(map);
```

## Internal Details

| Concept | Default |
|---|---|
| Initial capacity | 11 |
| Load factor | 0.75 |
| Collision handling | Linked list |
| Synchronization | Yes |

In common JDK implementations, resizing uses the formula:

```text
New Capacity = Old Capacity × 2 + 1
```

## Important Hashtable Methods

| Method | Purpose |
|---|---|
| `put()` | Inserts an entry |
| `putAll()` | Copies entries |
| `get()` | Retrieves a value |
| `getOrDefault()` | Retrieves a value or default |
| `putIfAbsent()` | Inserts if absent |
| `remove()` | Removes an entry |
| `replace()` | Replaces a value |
| `containsKey()` | Checks key existence |
| `containsValue()` | Checks value existence |
| `contains()` | Legacy alias of `containsValue()` |
| `keys()` | Returns Enumeration of keys |
| `elements()` | Returns Enumeration of values |
| `keySet()` | Returns keys |
| `values()` | Returns values |
| `entrySet()` | Returns entries |
| `size()` | Returns number of entries |
| `isEmpty()` | Checks whether empty |
| `clear()` | Removes all entries |
| `clone()` | Creates a shallow copy |
| `forEach()` | Iterates through entries |
| `compute()` | Computes a new value |
| `computeIfAbsent()` | Computes if absent |
| `computeIfPresent()` | Computes if present |
| `merge()` | Combines values |

## Enumeration

Hashtable supports legacy Enumeration.

### Iterating Keys

```java
Enumeration<Integer> e = map.keys();

while (e.hasMoreElements()) {
    System.out.println(e.nextElement());
}
```

### Iterating Values

```java
Enumeration<String> e = map.elements();

while (e.hasMoreElements()) {
    System.out.println(e.nextElement());
}
```

### Important Note

For modern concurrent programming, prefer ConcurrentHashMap over Hashtable in most cases.

---

# 7. ConcurrentHashMap

## Introduction

- ConcurrentHashMap is a thread-safe Map implementation.
- It was introduced in Java 1.5.
- It does not allow null keys or null values.
- It does not guarantee ordering.
- It supports concurrent access by multiple threads.
- It generally provides better scalability than Hashtable.

### Example

```java
ConcurrentHashMap<Integer, String> map =
    new ConcurrentHashMap<>();

map.put(101, "Ashfaq");
map.put(102, "Rahul");

System.out.println(map);
```

## Internal Working

### Java 7

- Used Segment-based locking.
- Divided the Map into multiple segments.
- Each segment could be locked independently.

### Java 8 and Later

Uses mechanisms including:

- CAS (Compare-And-Swap).
- Synchronization on individual bins when needed.
- Volatile operations.
- Linked lists and tree bins for collisions.

### CAS

CAS means Compare-And-Swap.

It is an atomic operation that:

1. Checks the current value.
2. Compares it with an expected value.
3. Updates it only if the expected value matches.

## Important ConcurrentHashMap Methods

| Method | Purpose |
|---|---|
| `put()` | Inserts an entry |
| `putIfAbsent()` | Atomically inserts if absent |
| `get()` | Retrieves a value |
| `getOrDefault()` | Retrieves a value or default |
| `remove()` | Removes an entry |
| `remove(key, value)` | Conditionally removes an entry |
| `replace()` | Replaces an existing value |
| `replace(key, old, new)` | Conditionally replaces a value |
| `containsKey()` | Checks key existence |
| `containsValue()` | Checks value existence |
| `keySet()` | Returns keys |
| `values()` | Returns values |
| `entrySet()` | Returns entries |
| `forEach()` | Performs an action for entries |
| `compute()` | Atomically computes a mapping |
| `computeIfAbsent()` | Atomically computes if absent |
| `computeIfPresent()` | Atomically computes if present |
| `merge()` | Atomically combines values |
| `search()` | Searches entries or values |
| `reduce()` | Performs reduction operations |

## Bulk Operations

### search()

```java
ConcurrentHashMap<Integer, String> map =
    new ConcurrentHashMap<>();

map.put(1, "Java");
map.put(2, "Python");
map.put(3, "C++");

String result = map.search(
    1,
    (key, value) -> value.equals("Python") ? value : null
);

System.out.println(result);
```

### reduceValues()

```java
ConcurrentHashMap<Integer, Integer> map =
    new ConcurrentHashMap<>();

map.put(1, 10);
map.put(2, 20);
map.put(3, 30);

int sum = map.reduceValues(
    1,
    Integer::sum
);

System.out.println(sum); // 60
```

### Weakly Consistent Iterators

ConcurrentHashMap iterators:

- Can reflect concurrent modifications.
- Do not represent a guaranteed snapshot.
- Do not throw ConcurrentModificationException merely because another thread modifies the Map.

---

# 8. Different Ways of Iterating a Map

Consider:

```java
Map<Integer, String> map = new HashMap<>();

map.put(101, "Ashfaq");
map.put(102, "Rahul");
map.put(103, "John");
```

## 1. Using entrySet() with Enhanced For Loop

Most recommended when both keys and values are needed.

```java
for (Map.Entry<Integer, String> entry : map.entrySet()) {
    System.out.println(
        entry.getKey() + " : " + entry.getValue()
    );
}
```

Methods:

- `getKey()` returns the key.
- `getValue()` returns the value.

## 2. Using keySet() with Enhanced For Loop

```java
for (Integer key : map.keySet()) {
    System.out.println(key + " : " + map.get(key));
}
```

Use when you want to iterate through keys.

## 3. Using values() with Enhanced For Loop

```java
for (String value : map.values()) {
    System.out.println(value);
}
```

Use when you only need values.

## 4. Using Iterator with entrySet()

```java
Iterator<Map.Entry<Integer, String>> itr =
    map.entrySet().iterator();

while (itr.hasNext()) {
    Map.Entry<Integer, String> entry = itr.next();

    System.out.println(
        entry.getKey() + " : " + entry.getValue()
    );
}
```

### Safe Removal

```java
Iterator<Map.Entry<Integer, String>> itr =
    map.entrySet().iterator();

while (itr.hasNext()) {
    Map.Entry<Integer, String> entry = itr.next();

    if (entry.getKey() == 102) {
        itr.remove();
    }
}
```

Use `itr.remove()` to remove entries safely through the iterator.

## 5. Using forEach() with Lambda

```java
map.forEach((key, value) -> {
    System.out.println(key + " : " + value);
});
```

One-line version:

```java
map.forEach((key, value) ->
    System.out.println(key + " : " + value)
);
```

## 6. Using Iterator with keySet()

```java
Iterator<Integer> itr = map.keySet().iterator();

while (itr.hasNext()) {
    Integer key = itr.next();

    System.out.println(key + " : " + map.get(key));
}
```

## 7. Using Stream API

```java
map.entrySet()
   .stream()
   .forEach(entry ->
       System.out.println(
           entry.getKey() + " : " + entry.getValue()
       )
   );
```

### Filtering with Streams

```java
map.entrySet()
   .stream()
   .filter(entry -> entry.getValue().startsWith("A"))
   .forEach(entry ->
       System.out.println(
           entry.getKey() + " : " + entry.getValue()
       )
   );
```

## 8. Hashtable Using Enumeration

### Keys

```java
Enumeration<Integer> e = hashtable.keys();

while (e.hasMoreElements()) {
    System.out.println(e.nextElement());
}
```

### Values

```java
Enumeration<String> e = hashtable.elements();

while (e.hasMoreElements()) {
    System.out.println(e.nextElement());
}
```

## Iteration Comparison

| Method | Iterates Over | Best Use |
|---|---|---|
| `entrySet()` | Keys and values | Both key and value |
| `keySet()` | Keys | Only keys |
| `values()` | Values | Only values |
| Iterator + `entrySet()` | Keys and values | Safe removal |
| `forEach()` | Keys and values | Short syntax |
| Iterator + `keySet()` | Keys | Key-based iteration |
| Stream API | Entries | Filtering and processing |
| Enumeration | Keys or values | Legacy Hashtable |

---

# 9. Important Map Methods – Quick Revision

| Method | Description |
|---|---|
| `put()` | Add or update |
| `putAll()` | Copy entries |
| `putIfAbsent()` | Insert if absent |
| `get()` | Get value |
| `getOrDefault()` | Get value or default |
| `remove()` | Remove entry |
| `replace()` | Replace value |
| `containsKey()` | Check key |
| `containsValue()` | Check value |
| `keySet()` | Get all keys |
| `values()` | Get all values |
| `entrySet()` | Get all entries |
| `forEach()` | Iterate |
| `compute()` | Recalculate value |
| `computeIfAbsent()` | Calculate if absent |
| `computeIfPresent()` | Calculate if present |
| `merge()` | Merge values |
| `clear()` | Remove all entries |
| `size()` | Get Map size |

## Special TreeMap Methods

```java
firstKey()
lastKey()
lowerKey()
higherKey()
floorKey()
ceilingKey()
pollFirstEntry()
pollLastEntry()
subMap()
headMap()
tailMap()
descendingMap()
```

---

# 10. Important Interview Differences

## HashMap vs LinkedHashMap

| HashMap | LinkedHashMap |
|---|---|
| No ordering guarantee | Maintains insertion order by default |
| Uses hash table | Uses hash table + linked list |
| Slightly less overhead | Slightly more overhead |
| Average O(1) | Average O(1) |

## HashMap vs TreeMap

| HashMap | TreeMap |
|---|---|
| No ordering guarantee | Sorted keys |
| Hash table | Red-Black tree |
| Average O(1) | O(log n) |
| Allows one null key | Generally does not allow null keys with natural ordering |

## HashMap vs Hashtable

| HashMap | Hashtable |
|---|---|
| Not synchronized | Synchronized methods |
| Allows null key | Does not allow null key |
| Allows null values | Does not allow null values |
| Modern implementation | Legacy implementation |

## Hashtable vs ConcurrentHashMap

| Hashtable | ConcurrentHashMap |
|---|---|
| Synchronizes individual methods | Uses finer-grained concurrency mechanisms |
| Less scalable under contention | Generally more scalable |
| Does not allow nulls | Does not allow nulls |
| Legacy | Modern concurrent Map |

## LinkedHashMap vs TreeMap

| LinkedHashMap | TreeMap |
|---|---|
| Maintains insertion order by default | Maintains sorted key order |
| Hash table + linked list | Red-Black tree |
| Average O(1) | O(log n) |

---

# 11. Placement Preparation – Must Remember

### Most Important Concepts

1. What is Map?
2. Why does Map not extend Collection?
3. Difference between key and value.
4. HashMap internal working.
5. Hash collision.
6. equals() and hashCode() contract.
7. HashMap capacity and load factor.
8. Difference between HashMap and LinkedHashMap.
9. Difference between HashMap and TreeMap.
10. Difference between HashMap and Hashtable.
11. Difference between Hashtable and ConcurrentHashMap.
12. What is a Red-Black tree?
13. What is CAS?
14. How does ConcurrentHashMap work?
15. Different ways of iterating a Map.

### Must-Practice Methods

**Common Map methods:**

```java
put()
get()
getOrDefault()
putIfAbsent()
remove()
containsKey()
containsValue()
keySet()
values()
entrySet()
forEach()
computeIfAbsent()
merge()
```

**TreeMap methods:**

```java
firstKey()
lastKey()
lowerKey()
higherKey()
floorKey()
ceilingKey()
```

**LinkedHashMap:**

```java
removeEldestEntry()
```

**ConcurrentHashMap:**

```java
putIfAbsent()
computeIfAbsent()
compute()
merge()
search()
reduce()
```

---

# 12. Final Revision Summary

| Implementation | Main Point to Remember |
|---|---|
| HashMap | Fast lookup using hashing |
| LinkedHashMap | Maintains insertion/access order |
| TreeMap | Maintains sorted key order |
| Hashtable | Legacy synchronized Map |
| ConcurrentHashMap | Thread-safe concurrent Map |

### My Placement Recommendation

For service-based company interviews and coding rounds, prioritize:

1. HashMap – internal working and frequency counting.
2. LinkedHashMap – insertion order and LRU cache basics.
3. TreeMap – sorted keys and navigation methods.
4. Hashtable – differences from HashMap.
5. ConcurrentHashMap – thread safety and differences from Hashtable.

**Remember:** HashMap, LinkedHashMap, and TreeMap are especially important to understand and practice for Java placement preparation.