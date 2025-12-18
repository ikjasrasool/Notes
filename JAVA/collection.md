# Java Collections Framework - Complete Guide

## Table of Contents
1. [Overview](#overview)
2. [Collection Hierarchy](#collection-hierarchy)
3. [List Interface](#list-interface)
4. [Set Interface](#set-interface)
5. [Queue Interface](#queue-interface)
6. [Map Interface](#map-interface)
7. [Utility Classes](#utility-classes)

---

## Overview

The Java Collections Framework provides a unified architecture for storing and manipulating groups of objects. It includes interfaces, implementations, and algorithms.

**Key Benefits:**
- Reduces programming effort
- Increases performance
- Provides interoperability between unrelated APIs
- Reduces effort to learn APIs

---

## Collection Hierarchy

```
Collection (Interface)
├── List (Interface)
│   ├── ArrayList
│   ├── LinkedList
│   ├── Vector
│   └── Stack
├── Set (Interface)
│   ├── HashSet
│   ├── LinkedHashSet
│   └── SortedSet (Interface)
│       └── TreeSet
└── Queue (Interface)
    ├── PriorityQueue
    ├── Deque (Interface)
    │   ├── ArrayDeque
    │   └── LinkedList

Map (Interface) - Separate Hierarchy
├── HashMap
├── LinkedHashMap
├── Hashtable
├── TreeMap
└── WeakHashMap
```

---

## List Interface

**Characteristics:**
- Ordered collection (maintains insertion order)
- Allows duplicate elements
- Index-based access

### ArrayList

## 🔹 Creation

```java
ArrayList<String> list = new ArrayList<>();
ArrayList<String> listWithCapacity = new ArrayList<>(100);
```

---

## 🔹 Common Methods

```java
list.add("Element");              // Adds element at the end
list.add(0, "First");             // Adds element at index
list.get(0);                      // Returns element at index
list.set(0, "Updated");           // Updates element at index
list.remove(0);                   // Removes element by index
list.remove("Element");           // Removes element by value
list.contains("Element");         // Checks existence
list.indexOf("Element");          // Returns first index
list.lastIndexOf("Element");      // Returns last index
list.size();                      // Returns number of elements
list.isEmpty();                   // Checks if list is empty
list.clear();                     // Removes all elements
list.toArray();                   // Converts list to array
list.addAll(otherList);           // Adds all elements from another list
list.removeAll(otherList);        // Removes matching elements
list.retainAll(otherList);        // Keeps only matching elements
list.subList(0, 5);               // Returns a sublist view
```

---

## 🔹 Java 8+ Methods

```java
list.forEach(e -> System.out.println(e));  // Iteration
list.replaceAll(e -> e.toUpperCase());     // Replace all elements
list.removeIf(e -> e.startsWith("A"));     // Conditional removal
list.sort(Comparator.naturalOrder());      // Sorting
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create ArrayList
        ArrayList<String> list = new ArrayList<>();
        System.out.println("Initial list: " + list);
        // Output: []

        // Add elements
        list.add("Element");
        System.out.println("After add(\"Element\"): " + list);
        // Output: [Element]

        list.add(0, "First");
        System.out.println("After add(0, \"First\"): " + list);
        // Output: [First, Element]

        // Get element
        System.out.println("get(0): " + list.get(0));
        // Output: First

        // Set element
        list.set(0, "Updated");
        System.out.println("After set(0, \"Updated\"): " + list);
        // Output: [Updated, Element]

        // Remove by index
        list.remove(0);
        System.out.println("After remove(0): " + list);
        // Output: [Element]

        // Remove by object
        list.remove("Element");
        System.out.println("After remove(\"Element\"): " + list);
        // Output: []

        // Add more elements
        list.add("Apple");
        list.add("Banana");
        list.add("Apple");
        System.out.println("After adding Apple, Banana, Apple: " + list);
        // Output: [Apple, Banana, Apple]

        // Contains
        System.out.println("contains(\"Apple\"): " + list.contains("Apple"));
        // Output: true

        // IndexOf & LastIndexOf
        System.out.println("indexOf(\"Apple\"): " + list.indexOf("Apple"));
        // Output: 0

        System.out.println("lastIndexOf(\"Apple\"): " + list.lastIndexOf("Apple"));
        // Output: 2

        // Size
        System.out.println("size(): " + list.size());
        // Output: 3

        // isEmpty
        System.out.println("isEmpty(): " + list.isEmpty());
        // Output: false

        // toArray
        Object[] arr = list.toArray();
        System.out.println("toArray(): " + Arrays.toString(arr));
        // Output: [Apple, Banana, Apple]

        // Another list
        ArrayList<String> otherList = new ArrayList<>();
        otherList.add("Banana");
        otherList.add("Cherry");
        System.out.println("otherList: " + otherList);
        // Output: [Banana, Cherry]

        // addAll
        list.addAll(otherList);
        System.out.println("After addAll(otherList): " + list);
        // Output: [Apple, Banana, Apple, Banana, Cherry]

        // removeAll
        list.removeAll(otherList);
        System.out.println("After removeAll(otherList): " + list);
        // Output: [Apple, Apple]

        // retainAll
        list.add("Banana");
        list.add("Cherry");
        System.out.println("Before retainAll(otherList): " + list);
        // Output: [Apple, Apple, Banana, Cherry]

        list.retainAll(otherList);
        System.out.println("After retainAll(otherList): " + list);
        // Output: [Banana, Cherry]

        // subList
        list.clear();
        list.add("A");
        list.add("B");
        list.add("C");
        list.add("D");
        list.add("E");
        System.out.println("New list: " + list);
        // Output: [A, B, C, D, E]

        List<String> sub = list.subList(1, 4);
        System.out.println("subList(1,4): " + sub);
        // Output: [B, C, D]

        // Java 8 forEach
        System.out.print("forEach(): ");
        list.forEach(e -> System.out.print(e + " "));
        System.out.println();
        // Output: A B C D E

        // replaceAll
        list.replaceAll(e -> e.toLowerCase());
        System.out.println("After replaceAll(toLowerCase): " + list);
        // Output: [a, b, c, d, e]

        // removeIf
        list.removeIf(e -> e.equals("c"));
        System.out.println("After removeIf(e == \"c\"): " + list);
        // Output: [a, b, d, e]

        // sort
        list.sort(Comparator.naturalOrder());
        System.out.println("After sort(): " + list);
        // Output: [a, b, d, e]

        // clear
        list.clear();
        System.out.println("After clear(): " + list);
        // Output: []

        System.out.println("isEmpty(): " + list.isEmpty());
        // Output: true
    }
}
```

---

**Time Complexity:**
- Add: O(1) amortized
- Get: O(1)
- Remove: O(n)
- Search: O(n)

---

### LinkedList

**Use Case:** When you need frequent insertions/deletions at beginning or middle

```java
// Creation
LinkedList<String> list = new LinkedList<>();

// List Methods (same as ArrayList)
list.add("Element");
list.get(0);

// Additional LinkedList Methods
list.addFirst("First");           // Adds at beginning
list.addLast("Last");             // Adds at end
list.getFirst();                   // Returns first element
list.getLast();                    // Returns last element
list.removeFirst();                // Removes first
list.removeLast();                 // Removes last
list.peek();                       // Returns first (null if empty)
list.poll();                       // Removes and returns first
list.offer("Element");            // Adds to end
list.push("Element");             // Adds at beginning (stack)
list.pop();                        // Removes from beginning (stack)

// Iterator
Iterator<String> it = list.iterator();
while(it.hasNext()) {
    System.out.println(it.next());
}

ListIterator<String> lit = list.listIterator();
while(lit.hasNext()) {
    System.out.println(lit.next());
}
```

**Time Complexity:**
- Add at beginning/end: O(1)
- Add at middle: O(n)
- Get: O(n)
- Remove: O(1) if node is known

---

### Vector

**Use Case:** Thread-safe ArrayList (legacy, prefer Collections.synchronizedList)

```java
Vector<String> vector = new Vector<>();

// Same methods as ArrayList, but synchronized
vector.add("Element");
vector.capacity();                 // Returns capacity
vector.ensureCapacity(100);       // Ensures minimum capacity
vector.elements();                 // Returns enumeration
```

---

### Stack

**Use Case:** LIFO (Last-In-First-Out) operations

```java
Stack<String> stack = new Stack<>();

stack.push("Element");            // Adds to top
stack.pop();                       // Removes and returns top
stack.peek();                      // Returns top without removing
stack.empty();                     // Checks if empty
stack.search("Element");          // Returns position from top
```

---

## Set Interface

**Characteristics:**
- No duplicate elements
- May or may not maintain order

### HashSet

**Use Case:** When you need fast add/remove/contains operations and don't care about order

```java
HashSet<String> set = new HashSet<>();

// Common Methods
set.add("Element");               // Returns false if duplicate
set.remove("Element");            // Removes element
set.contains("Element");          // Checks existence
set.size();                        // Returns size
set.isEmpty();                     // Checks if empty
set.clear();                       // Removes all
set.addAll(otherSet);             // Union
set.retainAll(otherSet);          // Intersection
set.removeAll(otherSet);          // Difference

// Iteration
for(String s : set) {
    System.out.println(s);
}

set.forEach(System.out::println);

// Convert to Array
String[] array = set.toArray(new String[0]);
```

**Time Complexity:**
- Add: O(1)
- Remove: O(1)
- Contains: O(1)

---

### LinkedHashSet

**Use Case:** When you need HashSet features with insertion order maintained

```java
LinkedHashSet<String> set = new LinkedHashSet<>();

// Same methods as HashSet
// Maintains insertion order during iteration
```

---

### TreeSet

**Use Case:** When you need sorted set (natural ordering or custom comparator)

```java
TreeSet<String> set = new TreeSet<>();
TreeSet<String> customSet = new TreeSet<>(Comparator.reverseOrder());

// Set Methods (same as HashSet)
set.add("Element");

// Additional SortedSet Methods
set.first();                       // Returns first (lowest)
set.last();                        // Returns last (highest)
set.headSet("Element");           // Returns elements < element
set.tailSet("Element");           // Returns elements >= element
set.subSet("A", "Z");             // Returns range [A, Z)
set.lower("Element");             // Returns greatest element < element
set.higher("Element");            // Returns least element > element
set.floor("Element");             // Returns greatest element <= element
set.ceiling("Element");           // Returns least element >= element
set.pollFirst();                  // Removes and returns first
set.pollLast();                   // Removes and returns last
set.descendingSet();              // Returns reverse order view
```

**Time Complexity:**
- Add: O(log n)
- Remove: O(log n)
- Contains: O(log n)

---

## Queue Interface

**Characteristics:**
- FIFO (First-In-First-Out) by default
- Designed for holding elements before processing

### PriorityQueue

**Use Case:** When you need elements processed in priority order (natural or custom)

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());

// Queue Methods
pq.offer(10);                     // Adds element, returns false if fails
pq.add(20);                       // Adds element, throws exception if fails
pq.poll();                        // Removes and returns head, null if empty
pq.remove();                      // Removes and returns head, throws if empty
pq.peek();                        // Returns head without removing, null if empty
pq.element();                     // Returns head, throws if empty
pq.size();
pq.isEmpty();
pq.clear();
```

**Time Complexity:**
- Offer/Add: O(log n)
- Poll/Remove: O(log n)
- Peek: O(1)

---

### ArrayDeque

**Use Case:** Double-ended queue, faster than LinkedList for both stack and queue operations

```java
ArrayDeque<String> deque = new ArrayDeque<>();

// Queue Methods (FIFO)
deque.offer("Element");           // Adds to end
deque.poll();                     // Removes from beginning
deque.peek();                     // Views beginning

// Deque Methods
deque.offerFirst("First");        // Adds to beginning
deque.offerLast("Last");          // Adds to end
deque.pollFirst();                // Removes from beginning
deque.pollLast();                 // Removes from end
deque.peekFirst();                // Views beginning
deque.peekLast();                 // Views end

// Stack Methods (LIFO)
deque.push("Element");            // Adds to beginning
deque.pop();                      // Removes from beginning
```

---

## Map Interface

**Characteristics:**
- Key-value pairs
- No duplicate keys
- Each key maps to at most one value

### HashMap

**Use Case:** When you need fast key-value lookups and don't care about order

```java
HashMap<String, Integer> map = new HashMap<>();

// Common Methods
map.put("Key", 100);              // Adds/updates entry
map.get("Key");                   // Returns value, null if not found
map.getOrDefault("Key", 0);       // Returns value or default
map.remove("Key");                // Removes entry
map.containsKey("Key");           // Checks key existence
map.containsValue(100);           // Checks value existence
map.size();
map.isEmpty();
map.clear();

// Bulk Operations
map.putAll(otherMap);
map.putIfAbsent("Key", 100);     // Only if key absent

// Java 8+ Methods
map.computeIfAbsent("Key", k -> 100);
map.computeIfPresent("Key", (k, v) -> v + 1);
map.compute("Key", (k, v) -> (v == null) ? 1 : v + 1);
map.merge("Key", 1, Integer::sum);
map.replace("Key", 100);
map.replace("Key", 100, 200);    // Only if current value is 100

// Iteration
for(String key : map.keySet()) {
    System.out.println(key);
}

for(Integer value : map.values()) {
    System.out.println(value);
}

for(Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}

map.forEach((k, v) -> System.out.println(k + ": " + v));
```

**Time Complexity:**
- Put: O(1)
- Get: O(1)
- Remove: O(1)
- ContainsKey: O(1)

---

### LinkedHashMap

**Use Case:** When you need HashMap features with insertion/access order maintained

```java
LinkedHashMap<String, Integer> map = new LinkedHashMap<>();
// Insertion order
LinkedHashMap<String, Integer> accessOrderMap = new LinkedHashMap<>(16, 0.75f, true);
// Access order (useful for LRU cache)

// Same methods as HashMap
```

---

### TreeMap

**Use Case:** When you need sorted map (by keys)

```java
TreeMap<String, Integer> map = new TreeMap<>();
TreeMap<String, Integer> reverseMap = new TreeMap<>(Comparator.reverseOrder());

// Map Methods (same as HashMap)
map.put("Key", 100);

// NavigableMap Methods
map.firstKey();                   // Returns first (lowest) key
map.lastKey();                    // Returns last (highest) key
map.firstEntry();                 // Returns first entry
map.lastEntry();                  // Returns last entry
map.lowerKey("Key");              // Returns greatest key < key
map.higherKey("Key");             // Returns least key > key
map.floorKey("Key");              // Returns greatest key <= key
map.ceilingKey("Key");            // Returns least key >= key
map.pollFirstEntry();             // Removes and returns first
map.pollLastEntry();              // Removes and returns last
map.headMap("Key");               // Returns keys < key
map.tailMap("Key");               // Returns keys >= key
map.subMap("A", "Z");             // Returns range [A, Z)
map.descendingMap();              // Returns reverse order view
```

**Time Complexity:**
- Put: O(log n)
- Get: O(log n)
- Remove: O(log n)

---

### Hashtable

**Use Case:** Legacy thread-safe map (prefer ConcurrentHashMap)

```java
Hashtable<String, Integer> table = new Hashtable<>();

// Same methods as HashMap
// Does not allow null keys or values
// All methods are synchronized
```

---

## Utility Classes

### Collections Class

```java
// Sorting
Collections.sort(list);
Collections.sort(list, Comparator.reverseOrder());

// Searching (requires sorted list)
Collections.binarySearch(list, "Element");

// Shuffling
Collections.shuffle(list);

// Reversing
Collections.reverse(list);

// Filling
Collections.fill(list, "Default");

// Copying
Collections.copy(destList, srcList);

// Min/Max
Collections.min(list);
Collections.max(list);

// Frequency
Collections.frequency(list, "Element");

// Disjoint Check
Collections.disjoint(list1, list2);

// Synchronization
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Set<String> syncSet = Collections.synchronizedSet(new HashSet<>());
Map<String, Integer> syncMap = Collections.synchronizedMap(new HashMap<>());

// Unmodifiable
List<String> unmodList = Collections.unmodifiableList(list);
Set<String> unmodSet = Collections.unmodifiableSet(set);
Map<String, Integer> unmodMap = Collections.unmodifiableMap(map);

// Empty Collections
Collections.emptyList();
Collections.emptySet();
Collections.emptyMap();

// Singleton Collections
Collections.singleton("Element");
Collections.singletonList("Element");
Collections.singletonMap("Key", "Value");

// Adding Elements
Collections.addAll(list, "A", "B", "C");

// Rotating
Collections.rotate(list, 2);

// Replacing
Collections.replaceAll(list, "Old", "New");
```

---

### Arrays Class

```java
// Sorting
Arrays.sort(array);
Arrays.sort(array, Comparator.reverseOrder());

// Searching (requires sorted array)
Arrays.binarySearch(array, "Element");

// Copying
int[] copy = Arrays.copyOf(array, newLength);
int[] rangeCopy = Arrays.copyOfRange(array, from, to);

// Filling
Arrays.fill(array, "Default");

// Comparing
Arrays.equals(array1, array2);
Arrays.deepEquals(array1, array2);  // For multidimensional

// Converting
List<String> list = Arrays.asList("A", "B", "C");

// Streaming
Arrays.stream(array).forEach(System.out::println);

// Parallel Sorting (faster for large arrays)
Arrays.parallelSort(array);

// toString
Arrays.toString(array);
Arrays.deepToString(multiArray);
```

---

## Performance Comparison

| Operation | ArrayList | LinkedList | HashSet | TreeSet | HashMap | TreeMap |
|-----------|-----------|------------|---------|---------|---------|---------|
| Add | O(1)* | O(1) | O(1) | O(log n) | O(1) | O(log n) |
| Remove | O(n) | O(1)** | O(1) | O(log n) | O(1) | O(log n) |
| Get | O(1) | O(n) | N/A | N/A | O(1) | O(log n) |
| Contains | O(n) | O(n) | O(1) | O(log n) | O(1) | O(log n) |
| Iteration | Fast | Fast | Fast | Fast | Fast | Fast |

*Amortized, **if node is known

---

## Choosing the Right Collection

**Use ArrayList when:**
- You need fast random access
- You iterate more than you insert/delete
- You mostly add at the end

**Use LinkedList when:**
- You frequently insert/delete at beginning or middle
- You implement a queue or deque
- Random access is rare

**Use HashSet when:**
- You need unique elements
- Order doesn't matter
- Fast add/remove/contains is critical

**Use TreeSet when:**
- You need unique elements in sorted order
- You need range operations

**Use HashMap when:**
- You need key-value pairs
- Order doesn't matter
- Fast lookup is critical

**Use TreeMap when:**
- You need key-value pairs in sorted key order
- You need range operations on keys

**Use PriorityQueue when:**
- You need elements processed by priority
- You're implementing heap-based algorithms

**Use ArrayDeque when:**
- You need stack or queue operations
- You want better performance than LinkedList



