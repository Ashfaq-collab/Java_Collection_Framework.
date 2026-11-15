# Java Queue – Complete Notes
## Java Collection Framework | Placement Preparation

---

# 1. What is Queue?

- Queue is an interface in the Java Collection Framework.
- It follows the **FIFO (First In, First Out)** principle.
- The element inserted first is removed first.
- Insertion generally happens at the rear.
- Removal generally happens at the front.
- Queue belongs to the `java.util` package.

### Example

```java
Queue<Integer> queue = new LinkedList<>();

queue.offer(10);
queue.offer(20);
queue.offer(30);

System.out.println(queue); // [10, 20, 30]

queue.poll();

System.out.println(queue); // [20, 30]
```

### Real-world applications

- Ticket booking systems
- Printer job scheduling
- Customer service systems
- Task scheduling
- Message processing

---

# 2. Queue Interface Hierarchy

Simplified hierarchy:

```text
Iterable
   |
Collection
   |
 Queue (Interface)
   |
   |---- Deque (Interface)
   |       |
   |       |---- LinkedList
   |       |
   |       |---- ArrayDeque
   |
   |---- PriorityQueue (Class)
```

Other important Queue implementations:

- `PriorityBlockingQueue`
- `ConcurrentLinkedQueue`

### Important points

- Queue is an interface, not a class.
- LinkedList implements both List and Deque.
- ArrayDeque implements Deque.
- Deque extends Queue.
- PriorityQueue directly implements Queue.

---

# 3. Creating a Queue

```java
import java.util.*;

Queue<Integer> q1 = new LinkedList<>();

Queue<Integer> q2 = new PriorityQueue<>();

Queue<Integer> q3 = new ArrayDeque<>();
```

---

# 4. Important Queue Methods

Queue has six major methods.

| Method | Description |
|---|---|
| `add(e)` | Inserts an element |
| `offer(e)` | Inserts an element |
| `remove()` | Removes and returns front element |
| `poll()` | Removes and returns front; returns null if empty |
| `element()` | Retrieves front without removing |
| `peek()` | Retrieves front without removing; returns null if empty |

### Difference between add() and offer()

| add() | offer() |
|---|---|
| Inserts an element | Inserts an element |
| Throws exception if insertion fails | Returns false if insertion fails |

### Difference between remove() and poll()

| remove() | poll() |
|---|---|
| Removes front element | Removes front element |
| Throws exception if Queue is empty | Returns null if Queue is empty |

### Difference between element() and peek()

| element() | peek() |
|---|---|
| Retrieves front element | Retrieves front element |
| Does not remove element | Does not remove element |
| Throws exception if empty | Returns null if empty |

### Other Collection methods

| Method | Description |
|---|---|
| `size()` | Returns number of elements |
| `isEmpty()` | Checks whether Queue is empty |
| `contains(e)` | Checks whether element exists |
| `clear()` | Removes all elements |
| `iterator()` | Returns an iterator |
| `toArray()` | Converts Queue into an array |
| `remove(Object o)` | Removes specified element |
| `addAll(c)` | Adds all elements from another collection |
| `removeAll(c)` | Removes matching elements |
| `retainAll(c)` | Retains matching elements |

---

# 5. Types of Queues

## A. Simple Queue

- Follows FIFO.
- Insertion happens at the rear.
- Removal happens at the front.

Example:

```java
Queue<Integer> queue = new LinkedList<>();

queue.offer(10);
queue.offer(20);
queue.offer(30);

queue.poll(); // Removes 10
```

## B. Priority Queue

- Processes elements based on priority.
- Does not follow normal FIFO.
- Uses a binary heap internally.
- Default implementation is a Min Heap.
- Smallest element has the highest priority.

### Min Heap

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();

pq.offer(40);
pq.offer(10);
pq.offer(30);
pq.offer(20);

System.out.println(pq.poll()); // 10
System.out.println(pq.poll()); // 20
System.out.println(pq.poll()); // 30
System.out.println(pq.poll()); // 40
```

### Max Heap

Use `Collections.reverseOrder()`.

```java
PriorityQueue<Integer> pq =
    new PriorityQueue<>(Collections.reverseOrder());

pq.offer(10);
pq.offer(40);
pq.offer(20);
pq.offer(30);

System.out.println(pq.poll()); // 40
System.out.println(pq.poll()); // 30
System.out.println(pq.poll()); // 20
System.out.println(pq.poll()); // 10
```

Important points:

- Duplicate elements are allowed.
- Null elements are not allowed.
- `peek()` takes O(1).
- `offer()` and `poll()` take O(log n).
- Iteration does not guarantee priority order.

## C. Deque (Double Ended Queue)

- Allows insertion and deletion at both ends.
- Can work as a Queue (FIFO).
- Can also work as a Stack (LIFO).

Important methods:

| Method | Description |
|---|---|
| `addFirst(e)` | Inserts at front |
| `addLast(e)` | Inserts at rear |
| `offerFirst(e)` | Offers at front |
| `offerLast(e)` | Offers at rear |
| `removeFirst()` | Removes front |
| `removeLast()` | Removes rear |
| `pollFirst()` | Removes front; returns null if empty |
| `pollLast()` | Removes rear; returns null if empty |
| `getFirst()` | Retrieves front |
| `getLast()` | Retrieves rear |
| `peekFirst()` | Retrieves front; returns null if empty |
| `peekLast()` | Retrieves rear; returns null if empty |

## D. Blocking Queue

- Used in multithreaded programming.
- Supports blocking operations.
- A consumer can wait when the Queue is empty.
- A producer can wait when a bounded Queue is full.

Important implementations:

- `ArrayBlockingQueue`
- `LinkedBlockingQueue`
- `PriorityBlockingQueue`
- `DelayQueue`

---

# 6. Important Methods of Queue Implementations

## A. LinkedList

- Implements List and Deque.
- Uses a doubly linked list internally.
- Can be used as a FIFO Queue.
- Allows duplicate elements.
- Allows null elements.
- Not thread-safe.

### Queue methods

```java
add(e)
offer(e)
remove()
poll()
element()
peek()
```

### Deque methods

```java
addFirst(e)
addLast(e)

offerFirst(e)
offerLast(e)

removeFirst()
removeLast()

pollFirst()
pollLast()

getFirst()
getLast()

peekFirst()
peekLast()
```

### Other important methods

```java
add(index, e)
get(index)
set(index, e)
remove(index)

indexOf(e)
lastIndexOf(e)

contains(e)
size()
clear()
isEmpty()

descendingIterator()
```

### Example

```java
LinkedList<Integer> list = new LinkedList<>();

list.addFirst(10);
list.addLast(20);
list.addFirst(5);

System.out.println(list); // [5, 10, 20]

list.removeFirst();
list.removeLast();

System.out.println(list); // [10]
```

---

## B. PriorityQueue

- Implements Queue.
- Uses a binary heap internally.
- Default ordering is Min Heap.
- Does not follow FIFO.
- Allows duplicate elements.
- Does not allow null.
- Not thread-safe.

### Important methods

```java
add(e)
offer(e)

remove()
poll()

element()
peek()

size()
isEmpty()
contains(e)
clear()

comparator()
removeIf(predicate)
forEach(action)
toArray()
```

### Time complexity

| Operation | Complexity |
|---|---|
| `offer()` | O(log n) |
| `poll()` | O(log n) |
| `peek()` | O(1) |
| `contains()` | O(n) |
| `remove(Object)` | O(n) |

---

## C. ArrayDeque

- Implements Deque.
- Uses a resizable array internally.
- Supports insertion and deletion at both ends.
- Allows duplicate elements.
- Does not allow null.
- Not thread-safe.
- Generally preferred over LinkedList for normal Queue and Stack operations.

### Queue methods

```java
add(e)
offer(e)

remove()
poll()

element()
peek()
```

### Deque methods

```java
addFirst(e)
addLast(e)

offerFirst(e)
offerLast(e)

removeFirst()
removeLast()

pollFirst()
pollLast()

getFirst()
getLast()

peekFirst()
peekLast()
```

### Stack methods

```java
push(e)
pop()
peek()
```

### Other methods

```java
size()
isEmpty()
contains(e)
clear()

removeFirstOccurrence(e)
removeLastOccurrence(e)

descendingIterator()
iterator()
toArray()
```

### Example: Using ArrayDeque as Stack

```java
ArrayDeque<Integer> stack = new ArrayDeque<>();

stack.push(10);
stack.push(20);
stack.push(30);

System.out.println(stack.peek()); // 30

stack.pop();

System.out.println(stack); // [20, 10]
```

---

## D. PriorityBlockingQueue

- Implements BlockingQueue.
- Thread-safe.
- Uses priority ordering.
- Default ordering is Min Heap.
- Allows duplicate elements.
- Does not allow null.
- Logically unbounded.
- `take()` waits if the Queue is empty.

### Important methods

```java
add(e)
offer(e)
put(e)

take()
poll()
poll(time, unit)

peek()
remove()
element()

size()
isEmpty()
contains(e)
clear()

remainingCapacity()
drainTo(collection)
comparator()
```

### Important blocking methods

**put()**

```java
pq.put(100);
```

Inserts an element. It does not wait for capacity because PriorityBlockingQueue is logically unbounded.

**take()**

```java
int value = pq.take();
```

Removes the highest-priority element. Waits if the Queue is empty.

**poll(time, unit)**

```java
Integer value = pq.poll(5, TimeUnit.SECONDS);
```

Waits for an element up to the specified time and returns null if none becomes available.

**drainTo()**

```java
PriorityBlockingQueue<Integer> pq =
    new PriorityBlockingQueue<>();

pq.offer(10);
pq.offer(20);
pq.offer(30);

List<Integer> list = new ArrayList<>();

pq.drainTo(list);
```

Transfers elements to another collection in priority order.

---

## E. ConcurrentLinkedQueue

- Implements Queue.
- Thread-safe.
- Uses linked nodes internally.
- Follows FIFO.
- Uses non-blocking operations.
- Allows duplicate elements.
- Does not allow null.
- Its iterator is weakly consistent.

### Important methods

```java
add(e)
offer(e)

poll()
peek()

remove()
element()

size()
isEmpty()
contains(e)
clear()

remove(Object o)
addAll(collection)

iterator()
forEach(action)
removeIf(predicate)
toArray()
```

### Important points

- Multiple threads can safely access the Queue.
- `offer()`, `poll()`, and `peek()` are non-blocking.
- `size()` takes O(n) time.
- Iterator does not throw ConcurrentModificationException merely because another thread modifies the Queue.
- Concurrent modifications may or may not be reflected in iteration.

---

# 7. Comparison of All Five Implementations

| Feature | LinkedList | PriorityQueue | ArrayDeque | PriorityBlockingQueue | ConcurrentLinkedQueue |
|---|---|---|---|---|---|
| Ordering | FIFO | Priority | FIFO | Priority | FIFO |
| Internal structure | Doubly linked list | Binary heap | Resizable array | Binary heap | Linked nodes |
| Thread-safe | No | No | No | Yes | Yes |
| Duplicates | Yes | Yes | Yes | Yes | Yes |
| Null | Yes | No | No | No | No |
| Blocking | No | No | No | Yes, `take()` | No |
| Priority-based | No | Yes | No | Yes | No |

### Which implementation should you use?

- **LinkedList:** When you need both List and Queue functionality.
- **PriorityQueue:** When elements must be processed according to priority.
- **ArrayDeque:** For efficient normal Queue and Stack operations.
- **PriorityBlockingQueue:** For concurrent priority-based processing.
- **ConcurrentLinkedQueue:** For concurrent FIFO processing without blocking operations.

---

# 8. Time Complexity

| Operation | LinkedList | PriorityQueue | ArrayDeque |
|---|---|---|---|
| Insert at rear | O(1) | O(log n) | Amortized O(1) |
| Remove front | O(1) | O(log n) | Amortized O(1) |
| Peek | O(1) | O(1) | O(1) |
| Search | O(n) | O(n) | O(n) |
| Size | O(1) | O(1) | O(1) |

---

# 9. Different Ways of Iterating Queue

Consider:

```java
Queue<Integer> queue = new LinkedList<>();

queue.offer(10);
queue.offer(20);
queue.offer(30);
queue.offer(40);
queue.offer(50);
```

## Method 1: For-each Loop

```java
for (Integer num : queue) {
    System.out.println(num);
}
```

- Simple and easy.
- Does not remove elements.

## Method 2: Iterator

```java
Iterator<Integer> itr = queue.iterator();

while (itr.hasNext()) {
    System.out.println(itr.next());
}
```

Important Iterator methods:

| Method | Description |
|---|---|
| `hasNext()` | Checks whether another element exists |
| `next()` | Returns next element |
| `remove()` | Removes last returned element |

### Removing elements using Iterator

```java
Iterator<Integer> itr = queue.iterator();

while (itr.hasNext()) {
    Integer num = itr.next();

    if (num == 30) {
        itr.remove();
    }
}
```

## Method 3: forEach()

```java
queue.forEach(num -> System.out.println(num));
```

Using method reference:

```java
queue.forEach(System.out::println);
```

- Introduced in Java 8.
- Does not remove elements.

## Method 4: Stream API

```java
queue.stream()
     .forEach(System.out::println);
```

### Using filter()

```java
queue.stream()
     .filter(num -> num > 20)
     .forEach(System.out::println);
```

Output:

```text
30
40
50
```

## Method 5: while Loop with poll()

```java
while (!queue.isEmpty()) {
    System.out.println(queue.poll());
}
```

- Retrieves and removes elements.
- Empties the Queue.

## Method 6: Spliterator

```java
Spliterator<Integer> spl = queue.spliterator();

spl.forEachRemaining(System.out::println);
```

- Supports traversal.
- Can also support parallel processing.

### Iteration comparison

| Method | Removes elements? |
|---|---|
| For-each | No |
| Iterator | No, unless `itr.remove()` |
| forEach() | No |
| Stream API | No |
| while + poll() | Yes |
| Spliterator | No |

### Important iteration points

1. For-each is the simplest iteration method.
2. Iterator supports controlled traversal.
3. Iterator's `remove()` can remove elements during traversal.
4. Stream API supports filtering and processing.
5. `poll()` removes elements.
6. PriorityQueue iterator does not guarantee priority order.
7. LinkedList, ArrayDeque and ConcurrentLinkedQueue iterate in FIFO traversal order.

---

# 10. Important Interview Questions

1. What is Queue in Java?
2. What is FIFO?
3. Is Queue an interface or a class?
4. What are the implementations of Queue?
5. Difference between `add()` and `offer()`?
6. Difference between `remove()` and `poll()`?
7. Difference between `element()` and `peek()`?
8. What is PriorityQueue?
9. Does PriorityQueue follow FIFO?
10. What is the difference between Min Heap and Max Heap?
11. How do you create a Max Heap using PriorityQueue?
12. What is Deque?
13. Difference between Queue and Deque?
14. Difference between LinkedList and ArrayDeque?
15. Why is ArrayDeque preferred over Stack?
16. What is BlockingQueue?
17. Difference between PriorityQueue and PriorityBlockingQueue?
18. Difference between ConcurrentLinkedQueue and LinkedList?
19. What is the purpose of `take()`?
20. What is the purpose of `drainTo()`?
21. What is a weakly consistent iterator?
22. Which Queue implementations are thread-safe?
23. Which Queue implementations allow null?
24. What are the different ways to iterate through Queue?
25. Does PriorityQueue iterator guarantee sorted order?

---

# 11. Important Placement Revision Points

1. Queue follows FIFO.
2. Queue is an interface.
3. LinkedList and ArrayDeque implement Deque.
4. Deque extends Queue.
5. PriorityQueue uses a binary heap.
6. Default PriorityQueue is a Min Heap.
7. `Collections.reverseOrder()` creates a Max Heap.
8. PriorityQueue does not follow FIFO.
9. ArrayDeque supports both Queue and Stack operations.
10. ArrayDeque does not allow null.
11. LinkedList allows null.
12. PriorityBlockingQueue is thread-safe and priority-based.
13. PriorityBlockingQueue is logically unbounded.
14. `take()` waits when PriorityBlockingQueue is empty.
15. ConcurrentLinkedQueue is thread-safe and FIFO.
16. ConcurrentLinkedQueue uses non-blocking operations.
17. `poll()` returns null when the Queue is empty.
18. `remove()` throws an exception when the Queue is empty.
19. `peek()` retrieves without removing.
20. `while + poll()` empties the Queue.
21. PriorityQueue iteration does not guarantee priority order.

---

# 12. What to Study First for Service-Based Company Placements

| Priority | Topic |
|---|---|
| 1 | Queue fundamentals and FIFO |
| 2 | Six important Queue methods |
| 3 | LinkedList Queue methods |
| 4 | PriorityQueue and Min/Max Heap |
| 5 | ArrayDeque and Stack operations |
| 6 | Different ways of iterating Queue |
| 7 | PriorityBlockingQueue basics |
| 8 | ConcurrentLinkedQueue basics |
| 9 | Time complexity |
| 10 | Interview questions |

**Final recommendation:** Master LinkedList, PriorityQueue, and ArrayDeque first. Understand the purpose and important methods of PriorityBlockingQueue and ConcurrentLinkedQueue. Practice the six main Queue methods until you can explain their differences without referring to notes.

These topics provide a solid foundation for Java Collection Framework interviews at service-based companies.