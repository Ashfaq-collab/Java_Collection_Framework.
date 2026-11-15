# Java Collection Framework: List Interface --- Study Notes

## 1. Java Collection Framework (JCF)

The Java Collection Framework is a set of interfaces and classes used to
store and manipulate groups of objects.

-   Arrays have a fixed size.
-   Collections can grow and shrink dynamically.
-   `List` is one of the main interfaces in the framework.

## 2. List Interface

`List` is an interface that extends `Collection`.

### Main characteristics

1.  Maintains insertion order.
2.  Allows duplicate elements.
3.  Supports index-based access.
4.  Allows elements to be added, updated and removed.
5.  Null support depends on the implementation.

Example:

``` java
List<String> names = new ArrayList<>();
names.add("Arun");
names.add("Bala");
names.add("Arun");

System.out.println(names); // [Arun, Bala, Arun]
```

### List hierarchy

``` text
Iterable
   |
Collection
   |
List
   |
   +-- ArrayList
   +-- LinkedList
   +-- Vector
          |
          +-- Stack
```

-   `List` is an interface.
-   `ArrayList`, `LinkedList` and `Vector` are classes.
-   `Stack` is a class that extends `Vector`.

## 3. Common List Methods

These methods are available across List implementations.

  Method                Purpose
  --------------------- ----------------------------------------------
  `add(e)`              Adds an element at the end
  `add(index, e)`       Inserts an element at a specific index
  `get(index)`          Returns the element at an index
  `set(index, e)`       Replaces the element at an index
  `remove(index)`       Removes the element at an index
  `remove(object)`      Removes the first matching element
  `size()`              Returns the number of elements
  `isEmpty()`           Checks whether the list is empty
  `contains(e)`         Checks whether an element exists
  `indexOf(e)`          Returns the first matching index
  `lastIndexOf(e)`      Returns the last matching index
  `clear()`             Removes all elements
  `toArray()`           Converts the list to an array
  `iterator()`          Returns an Iterator
  `listIterator()`      Returns a ListIterator
  `subList(from, to)`   Returns a view of a range; `to` is exclusive

### Important: `add()` vs `set()`

``` java
list.add(2, 100); // Inserts 100 at index 2; following elements shift.
list.set(2, 100); // Replaces the existing element at index 2.
```

### Important: `remove()` with Integer lists

``` java
List<Integer> numbers = new ArrayList<>(List.of(10, 20, 30));

numbers.remove(1);                    // Removes the element at index 1 (20).
numbers.remove(Integer.valueOf(10)); // Removes the value 10.
```

## 4. ArrayList

`ArrayList` is a resizable-array implementation of `List`.

``` java
ArrayList<Integer> numbers = new ArrayList<>();
```

### Key points

-   Maintains insertion order.
-   Allows duplicates and null values.
-   Provides fast index-based access.
-   Inserting or removing near the beginning or middle requires shifting
    elements.
-   It is not synchronized by default.

### Important methods

  Method                   Purpose
  ------------------------ -----------------------------------------
  `add(e)`                 Adds an element
  `add(index, e)`          Inserts at an index
  `get(index)`             Reads an element
  `set(index, e)`          Updates an element
  `remove(index)`          Removes by index
  `remove(object)`         Removes by value
  `ensureCapacity(n)`      Requests capacity of at least `n`
  `trimToSize()`           Trims capacity to current size
  `clone()`                Creates a shallow copy
  `removeIf(predicate)`    Removes elements matching a condition
  `replaceAll(operator)`   Replaces each element using an operator
  `sort(comparator)`       Sorts the list

`removeIf()`, `replaceAll()` and `sort()` are also available through
inherited interfaces/default methods; they are not exclusive to
ArrayList.

### Example

``` java
ArrayList<Integer> numbers =
    new ArrayList<>(List.of(10, 20, 30, 40));

numbers.sort(Comparator.reverseOrder());
System.out.println(numbers); // [40, 30, 20, 10]

numbers.removeIf(n -> n > 20);
System.out.println(numbers); // [20, 10]

numbers.replaceAll(n -> n * 2);
System.out.println(numbers); // [40, 20]

numbers.ensureCapacity(100);
numbers.trimToSize();
```

### ArrayList time complexity

  Operation                      Typical complexity
  ---------------------------- --------------------
  Access by index                              O(1)
  Update by index                              O(1)
  Add at end                         Amortized O(1)
  Insert at beginning/middle                   O(n)
  Remove at beginning/middle                   O(n)
  Search by value                              O(n)

Use ArrayList as the usual default when you need a general-purpose List
and frequent index-based reads.

## 5. LinkedList

`LinkedList` is implemented as a doubly linked list. Each node stores
data and links to the previous and next nodes.

``` java
LinkedList<Integer> numbers = new LinkedList<>();
```

### Key points

-   Maintains insertion order and allows duplicates.
-   Implements both `List` and `Deque`.
-   Supports operations at both ends.
-   Access by index requires traversal.
-   Uses additional memory for node links.

### Important methods

  Method                        Purpose
  ----------------------------- -------------------------------------------
  `addFirst(e)`                 Adds at the beginning
  `addLast(e)`                  Adds at the end
  `getFirst()`                  Gets the first element
  `getLast()`                   Gets the last element
  `removeFirst()`               Removes the first element
  `removeLast()`                Removes the last element
  `peek()` / `peekFirst()`      Reads the first element without removing
  `peekLast()`                  Reads the last element without removing
  `poll()` / `pollFirst()`      Retrieves and removes the first element
  `pollLast()`                  Retrieves and removes the last element
  `offer(e)` / `offerLast(e)`   Adds at the end
  `offerFirst(e)`               Adds at the beginning
  `push(e)`                     Adds at the front (stack-style operation)
  `pop()`                       Removes and returns the first element

### Example

``` java
LinkedList<Integer> numbers = new LinkedList<>();

numbers.add(20);
numbers.add(30);
numbers.addFirst(10);
numbers.addLast(40);

System.out.println(numbers);          // [10, 20, 30, 40]
System.out.println(numbers.getFirst()); // 10
System.out.println(numbers.getLast());  // 40

numbers.removeFirst();
numbers.removeLast();

System.out.println(numbers);          // [20, 30]
```

### `peek()`, `poll()` and `remove()`

  Method       Retrieves first element   Removes it   If empty
  ------------ ------------------------- ------------ ---------------------
  `peek()`     Yes                       No           Returns `null`
  `poll()`     Yes                       Yes          Returns `null`
  `remove()`   Yes                       Yes          Throws an exception

### LinkedList time complexity

  Operation                             Typical complexity
  ------------------------------- ------------------------
  Access by index                                     O(n)
  Search by value                                     O(n)
  Add/remove at either end                            O(1)
  Insert/remove at a known node                       O(1)
  Insert/remove at an index         O(n), due to traversal

Use LinkedList when deque-style operations at the ends are useful. It is
not automatically faster than ArrayList for arbitrary insertions or
removals.

## 6. Vector

`Vector` is a legacy, resizable-array class. Its methods are
synchronized.

``` java
Vector<Integer> values = new Vector<>();
```

### Key points

-   Maintains insertion order and allows duplicates.
-   Uses a resizable array.
-   Its methods are synchronized.
-   Usually has more synchronization overhead than ArrayList.
-   A newly created empty Vector has a default capacity of 10.

### Important methods

  Method                     Purpose
  -------------------------- ------------------------------------
  `addElement(e)`            Adds an element
  `elementAt(index)`         Gets an element at an index
  `setElementAt(e, index)`   Replaces an element
  `removeElement(e)`         Removes the first matching element
  `removeElementAt(index)`   Removes by index
  `removeAllElements()`      Removes all elements
  `firstElement()`           Gets the first element
  `lastElement()`            Gets the last element
  `elements()`               Returns an Enumeration
  `capacity()`               Returns current capacity
  `ensureCapacity(n)`        Ensures minimum capacity
  `trimToSize()`             Trims capacity to current size
  `setSize(n)`               Changes the logical size

### Example

``` java
Vector<Integer> values = new Vector<>();

values.addElement(10);
values.addElement(20);
values.addElement(30);

System.out.println(values.elementAt(1)); // 20

values.setElementAt(50, 1);

System.out.println(values.firstElement()); // 10
System.out.println(values.lastElement());  // 30
System.out.println(values.capacity());     // Usually 10 initially

values.removeElement(30);
System.out.println(values);                // [10, 50]
```

Note: `size()` is the number of stored elements; `capacity()` is the
amount of allocated storage. They are not the same.

## 7. Stack

`Stack` extends `Vector` and represents a Last In, First Out (LIFO)
structure.

The last element pushed is the first one popped.

``` java
Stack<Integer> stack = new Stack<>();
```

### Important methods

  -----------------------------------------------------------------------
  Method                              Purpose
  ----------------------------------- -----------------------------------
  `push(e)`                           Pushes an element onto the top

  `pop()`                             Removes and returns the top element

  `peek()`                            Returns the top element without
                                      removing it

  `empty()`                           Checks whether the stack is empty

  `search(e)`                         Returns the 1-based position from
                                      the top; `-1` if absent
  -----------------------------------------------------------------------

### Example

``` java
Stack<Integer> stack = new Stack<>();

stack.push(10);
stack.push(20);
stack.push(30);

System.out.println(stack);        // [10, 20, 30]
System.out.println(stack.peek()); // 30
System.out.println(stack.pop());  // 30
System.out.println(stack.empty());// false
System.out.println(stack.search(10)); // 2
```

After popping 30, 20 is at position 1 and 10 is at position 2.

For modern Java stack/deque use cases, `ArrayDeque` is generally
preferred over the legacy Stack class.

## 8. Comparison: ArrayList vs LinkedList vs Vector vs Stack

  --------------------------------------------------------------------------
  Feature        ArrayList      LinkedList     Vector         Stack
  -------------- -------------- -------------- -------------- --------------
  Underlying     Resizable      Doubly linked  Resizable      Inherits
  structure      array          list           array          Vector's array

  Maintains      Yes            Yes            Yes            Yes
  order                                                       

  Allows         Yes            Yes            Yes            Yes
  duplicates                                                  

  Synchronized   No             No             Yes            Inherited
  methods                                                     synchronized
                                                              Vector methods

  Fast index     Yes, O(1)      No, O(n)       Yes, O(1)      Yes, O(1)
  access                                                      

  Special        Index-based    Deque          Legacy         LIFO
  strength       access         operations     synchronized   operations
                                               list           
  --------------------------------------------------------------------------

### Which should you choose?

-   **ArrayList:** General-purpose List; frequent reads by index.
-   **LinkedList:** Operations at the beginning/end or deque behavior.
-   **Vector:** Mainly for understanding legacy Java code.
-   **Stack:** Learn its LIFO methods for interviews; prefer ArrayDeque
    in modern code.

## 9. Different Ways to Iterate Through a List

Use this sample list:

``` java
List<Integer> list = new ArrayList<>(
    Arrays.asList(10, 20, 30, 40, 50)
);
```

### 1. Normal for loop

``` java
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}
```

Best when you need the index or want to iterate backwards.

Backward traversal:

``` java
for (int i = list.size() - 1; i >= 0; i--) {
    System.out.println(list.get(i));
}
```

### 2. Enhanced for loop

``` java
for (int value : list) {
    System.out.println(value);
}
```

Best for simple read-only traversal.

### 3. Iterator

``` java
Iterator<Integer> it = list.iterator();

while (it.hasNext()) {
    System.out.println(it.next());
}
```

Important methods:

-   `hasNext()` --- checks whether another element exists.
-   `next()` --- returns the next element.
-   `remove()` --- safely removes the last element returned by this
    iterator.

Safe removal example:

``` java
Iterator<Integer> it = list.iterator();

while (it.hasNext()) {
    int value = it.next();

    if (value == 30) {
        it.remove();
    }
}
```

### 4. ListIterator

ListIterator supports forward and backward traversal and can modify the
list during traversal.

Forward:

``` java
ListIterator<Integer> it = list.listIterator();

while (it.hasNext()) {
    System.out.println(it.next());
}
```

Backward:

``` java
ListIterator<Integer> it = list.listIterator(list.size());

while (it.hasPrevious()) {
    System.out.println(it.previous());
}
```

Important methods:

-   `hasNext()`, `next()`
-   `hasPrevious()`, `previous()`
-   `nextIndex()`, `previousIndex()`
-   `add(e)`, `set(e)`, `remove()`

### 5. `forEach()` with a lambda

``` java
list.forEach(value -> System.out.println(value));
```

Method-reference version:

``` java
list.forEach(System.out::println);
```

### 6. Stream API

``` java
list.stream()
    .forEach(System.out::println);
```

Filtering example:

``` java
list.stream()
    .filter(value -> value % 2 == 0)
    .forEach(System.out::println);
```

### 7. Parallel Stream

``` java
list.parallelStream()
    .forEach(System.out::println);
```

Parallel processing does not guarantee encounter order with `forEach()`.

To preserve encounter order:

``` java
list.parallelStream()
    .forEachOrdered(System.out::println);
```

Use parallel streams only when parallel processing is appropriate and
beneficial.

### 8. Enumeration (legacy)

Enumeration is available for legacy classes such as Vector; it is not a
general List traversal method.

``` java
Vector<Integer> vector = new Vector<>(
    Arrays.asList(10, 20, 30)
);

Enumeration<Integer> e = vector.elements();

while (e.hasMoreElements()) {
    System.out.println(e.nextElement());
}
```

Important methods:

-   `hasMoreElements()`
-   `nextElement()`

### Iteration method comparison

  -------------------------------------------------------------------------------
  Method            Direction         Index access      Safe removal through
                                                        iterator API
  ----------------- ----------------- ----------------- -------------------------
  Normal for loop   Forward or        Yes               Not applicable; manage
                    backward                            indexes carefully

  Enhanced for      Forward           No                No direct safe-removal
                                                        method

  Iterator          Forward           No                Yes, `iterator.remove()`

  ListIterator      Forward or        Yes, via index    Yes,
                    backward          methods           `listIterator.remove()`

  `forEach()`       Forward encounter No                No direct safe-removal
                    order for an                        method
                    ordered List                        

  Sequential Stream Encounter order   No                Not for structural
                    for ordered                         removal during traversal
                    streams with                        
                    ordered terminal                    
                    operation                           

  Parallel Stream   Not necessarily   No                Not for structural
                    ordered with                        removal during traversal
                    `forEach()`                         

  Enumeration       Forward           No                No
  -------------------------------------------------------------------------------

## 10. Arrays and Lists: Conversion

### Array to List

``` java
String[] arr = {"Java", "Python", "C"};

List<String> list = new ArrayList<>(Arrays.asList(arr));
```

`Arrays.asList(arr)` by itself returns a fixed-size list backed by the
array. Wrapping it in `new ArrayList<>(...)` creates a resizable
ArrayList.

### List to Array

``` java
String[] arr = list.toArray(new String[0]);
```

## 11. Sorting a List

Ascending order:

``` java
Collections.sort(numbers);
```

Descending order:

``` java
Collections.sort(numbers, Collections.reverseOrder());
```

Or:

``` java
numbers.sort(Comparator.reverseOrder());
```

## 12. Generics in Lists

Generics specify the element type a List can hold.

``` java
List<Integer> numbers = new ArrayList<>();
List<String> names = new ArrayList<>();
List<Double> prices = new ArrayList<>();
List<Character> letters = new ArrayList<>();
```

Primitive types cannot be used directly as generic type arguments. Use
wrapper classes such as `Integer`, `Double` and `Character`.

## 13. Common Placement Interview Questions

1.  Is List an interface or a class?
2.  Does List allow duplicate elements?
3.  Does List maintain insertion order?
4.  What is the difference between ArrayList and LinkedList?
5.  What is the difference between `add()` and `set()`?
6.  What is the difference between `remove(1)` and
    `remove(Integer.valueOf(1))`?
7.  What is the difference between `peek()`, `poll()` and `remove()` in
    LinkedList?
8.  What is the difference between Iterator and ListIterator?
9.  How can you safely remove elements while iterating?
10. What is the difference between Vector and ArrayList?
11. Why does Stack follow LIFO?
12. What does Stack's `search()` return?
13. What is the difference between `size()` and `capacity()` in Vector?
14. What is the difference between `forEach()` and Stream's `forEach()`?
15. Does `parallelStream().forEach()` preserve insertion order?

## 14. Coding Problems to Practise

1.  Find the largest and smallest elements in an ArrayList.
2.  Reverse an ArrayList without using `Collections.reverse()`.
3.  Remove duplicate elements from a List.
4.  Find the second-largest element in an ArrayList.
5.  Sort an ArrayList in ascending and descending order.
6.  Count the frequency of each element in a List.
7.  Find the common elements between two Lists.
8.  Remove all even numbers using an Iterator.
9.  Traverse a LinkedList in forward and backward directions.
10. Implement basic stack operations using `Stack`.

## 15. Final Revision Checklist

-   [ ] List interface and its hierarchy
-   [ ] List characteristics: order, duplicates, index access
-   [ ] Common List methods
-   [ ] ArrayList methods and time complexity
-   [ ] LinkedList methods and deque operations
-   [ ] Vector methods, synchronization and capacity
-   [ ] Stack methods and LIFO principle
-   [ ] ArrayList vs LinkedList
-   [ ] Iterator vs ListIterator
-   [ ] All major List iteration techniques
-   [ ] Array/List conversion
-   [ ] Sorting and generics
-   [ ] Practise the coding problems above

### Placement preparation priority

1.  Master common List methods and ArrayList.
2.  Understand ArrayList vs LinkedList and their time complexities.
3.  Practise all iteration techniques, especially Iterator and
    ListIterator.
4.  Learn LinkedList deque methods.
5.  Understand Vector and Stack, including their legacy aspects.
6.  Solve the coding problems without relying on memorized code.
