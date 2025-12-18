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
**use Case:** When you need fast random access and iteration
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


## 🔹 Creation

```java
LinkedList<String> list = new LinkedList<>();
```

---

## 🔹 List Methods (Same as ArrayList)

```java
list.add("Element");      // Adds element
list.get(0);              // Gets element at index
list.set(0, "Updated");   // Updates element
list.remove(0);           // Removes by index
list.contains("Element"); // Checks existence
list.size();              // Returns size
list.isEmpty();           // Checks empty
```

---

## 🔹 Additional LinkedList Methods

```java
list.addFirst("First");   // Adds at beginning
list.addLast("Last");     // Adds at end
list.getFirst();          // Returns first element
list.getLast();           // Returns last element
list.removeFirst();       // Removes first
list.removeLast();        // Removes last
list.peek();              // Returns first (null if empty)
list.poll();              // Removes & returns first
list.offer("Element");    // Adds at end
list.push("Element");     // Adds at beginning (stack)
list.pop();               // Removes from beginning (stack)
```

---

## 🔹 Iterator Methods

```java
Iterator<String> it = list.iterator();
ListIterator<String> lit = list.listIterator();
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create LinkedList
        LinkedList<String> list = new LinkedList<>();
        System.out.println("Initial list: " + list);
        // Output: []

        // add
        list.add("Element");
        System.out.println("After add(\"Element\"): " + list);
        // Output: [Element]

        // addFirst
        list.addFirst("First");
        System.out.println("After addFirst(\"First\"): " + list);
        // Output: [First, Element]

        // addLast
        list.addLast("Last");
        System.out.println("After addLast(\"Last\"): " + list);
        // Output: [First, Element, Last]

        // get
        System.out.println("get(0): " + list.get(0));
        // Output: First

        // getFirst & getLast
        System.out.println("getFirst(): " + list.getFirst());
        // Output: First

        System.out.println("getLast(): " + list.getLast());
        // Output: Last

        // removeFirst
        list.removeFirst();
        System.out.println("After removeFirst(): " + list);
        // Output: [Element, Last]

        // removeLast
        list.removeLast();
        System.out.println("After removeLast(): " + list);
        // Output: [Element]

        // offer
        list.offer("A");
        list.offer("B");
        System.out.println("After offer(A), offer(B): " + list);
        // Output: [Element, A, B]

        // peek
        System.out.println("peek(): " + list.peek());
        // Output: Element

        // poll
        System.out.println("poll(): " + list.poll());
        // Output: Element
        System.out.println("After poll(): " + list);
        // Output: [A, B]

        // push (stack operation)
        list.push("Top");
        System.out.println("After push(\"Top\"): " + list);
        // Output: [Top, A, B]

        // pop (stack operation)
        System.out.println("pop(): " + list.pop());
        // Output: Top
        System.out.println("After pop(): " + list);
        // Output: [A, B]

        // Iterator
        System.out.print("Iterator traversal: ");
        Iterator<String> it = list.iterator();
        while(it.hasNext()) {
            System.out.print(it.next() + " ");
        }
        System.out.println();
        // Output: A B

        // ListIterator
        System.out.print("ListIterator traversal: ");
        ListIterator<String> lit = list.listIterator();
        while(lit.hasNext()) {
            System.out.print(lit.next() + " ");
        }
        System.out.println();
        // Output: A B

        // clear
        list.clear();
        System.out.println("After clear(): " + list);
        // Output: []

        // isEmpty
        System.out.println("isEmpty(): " + list.isEmpty());
        // Output: true
    }
}
```

---



**Time Complexity:**
- Add at beginning/end: O(1)
- Add at middle: O(n)
- Get: O(n)
- Remove: O(1) if node is known

---

### Vector

**Use Case:** Thread-safe ArrayList (legacy, prefer Collections.synchronizedList)


## 🔹 Creation

```java
Vector<String> vector = new Vector<>();
```

---

## 🔹 Common Methods (Same as ArrayList)

```java
vector.add("Element");     // Adds element
vector.get(0);             // Gets element
vector.set(0, "Updated");  // Updates element
vector.remove(0);          // Removes by index
vector.contains("Element");// Checks existence
vector.size();             // Returns size
vector.isEmpty();          // Checks empty
vector.clear();            // Removes all elements
```

---

## 🔹 Vector-Specific Methods

```java
vector.capacity();          // Returns current capacity
vector.ensureCapacity(100); // Ensures minimum capacity
vector.elements();          // Returns Enumeration
```

---

## 🔹 Enumeration (Legacy Iterator)

```java
Enumeration<String> e = vector.elements();
while(e.hasMoreElements()) {
    System.out.println(e.nextElement());
}
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create Vector
        Vector<String> vector = new Vector<>();
        System.out.println("Initial vector: " + vector);
        // Output: []

        // add
        vector.add("Element");
        vector.add("Apple");
        vector.add("Banana");
        System.out.println("After adding elements: " + vector);
        // Output: [Element, Apple, Banana]

        // size
        System.out.println("size(): " + vector.size());
        // Output: 3

        // capacity (default = 10)
        System.out.println("capacity(): " + vector.capacity());
        // Output: 10

        // ensureCapacity
        vector.ensureCapacity(100);
        System.out.println("After ensureCapacity(100)");
        System.out.println("capacity(): " + vector.capacity());
        // Output: 100

        // get
        System.out.println("get(1): " + vector.get(1));
        // Output: Apple

        // set
        vector.set(1, "Updated");
        System.out.println("After set(1, \"Updated\"): " + vector);
        // Output: [Element, Updated, Banana]

        // contains
        System.out.println("contains(\"Banana\"): " + vector.contains("Banana"));
        // Output: true

        // remove
        vector.remove("Element");
        System.out.println("After remove(\"Element\"): " + vector);
        // Output: [Updated, Banana]

        // Enumeration
        System.out.print("Enumeration traversal: ");
        Enumeration<String> en = vector.elements();
        while (en.hasMoreElements()) {
            System.out.print(en.nextElement() + " ");
        }
        System.out.println();
        // Output: Updated Banana

        // clear
        vector.clear();
        System.out.println("After clear(): " + vector);
        // Output: []

        // isEmpty
        System.out.println("isEmpty(): " + vector.isEmpty());
        // Output: true
    }
}
```

---




### Stack

**Use Case:** LIFO (Last-In-First-Out) operations



## 🔹 Creation

```java
Stack<String> stack = new Stack<>();
```

---

## 🔹 Stack Methods

```java
stack.push("Element");   // Adds element to top
stack.pop();             // Removes and returns top element
stack.peek();            // Returns top element without removing
stack.empty();           // Checks if stack is empty
stack.search("Element"); // Returns 1-based position from top
```

---

## 🔹 Important Notes

* `search()` returns:

  * `1` → top of stack
  * `-1` → element not found
* `pop()` throws `EmptyStackException` if stack is empty

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create Stack
        Stack<String> stack = new Stack<>();
        System.out.println("Initial stack: " + stack);
        // Output: []

        // push
        stack.push("A");
        stack.push("B");
        stack.push("C");
        System.out.println("After push(A), push(B), push(C): " + stack);
        // Output: [A, B, C]

        // peek
        System.out.println("peek(): " + stack.peek());
        // Output: C

        // pop
        System.out.println("pop(): " + stack.pop());
        // Output: C
        System.out.println("After pop(): " + stack);
        // Output: [A, B]

        // search
        System.out.println("search(\"B\"): " + stack.search("B"));
        // Output: 1

        System.out.println("search(\"A\"): " + stack.search("A"));
        // Output: 2

        System.out.println("search(\"Z\"): " + stack.search("Z"));
        // Output: -1

        // empty
        System.out.println("empty(): " + stack.empty());
        // Output: false

        // pop remaining elements
        stack.pop();
        stack.pop();
        System.out.println("After popping all elements: " + stack);
        // Output: []

        // empty again
        System.out.println("empty(): " + stack.empty());
        // Output: true
    }
}
```

---

## Set Interface

**Characteristics:**
- No duplicate elements
- May or may not maintain order

### HashSet

**Use Case:** When you need fast add/remove/contains operations and don't care about order


## 🔹 Creation

```java
HashSet<String> set = new HashSet<>();
```

---

## 🔹 Common Methods

```java
set.add("Element");        // Adds element (returns false if duplicate)
set.remove("Element");     // Removes element
set.contains("Element");   // Checks existence
set.size();                // Returns number of elements
set.isEmpty();             // Checks if empty
set.clear();               // Removes all elements
```

---

## 🔹 Set Operations

```java
set.addAll(otherSet);      // Union
set.retainAll(otherSet);   // Intersection
set.removeAll(otherSet);   // Difference
```

---

## 🔹 Iteration

```java
for(String s : set) {
    System.out.println(s);
}

set.forEach(System.out::println);
```

---

## 🔹 Convert to Array

```java
String[] array = set.toArray(new String[0]);
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create HashSet
        HashSet<String> set = new HashSet<>();
        System.out.println("Initial set: " + set);
        // Output: []

        // add
        set.add("Apple");
        set.add("Banana");
        set.add("Apple"); // duplicate
        System.out.println("After adding Apple, Banana, Apple: " + set);
        // Output: [Apple, Banana] (order may vary)

        // contains
        System.out.println("contains(\"Apple\"): " + set.contains("Apple"));
        // Output: true

        // remove
        set.remove("Banana");
        System.out.println("After remove(\"Banana\"): " + set);
        // Output: [Apple]

        // size
        System.out.println("size(): " + set.size());
        // Output: 1

        // isEmpty
        System.out.println("isEmpty(): " + set.isEmpty());
        // Output: false

        // Another set
        HashSet<String> otherSet = new HashSet<>();
        otherSet.add("Apple");
        otherSet.add("Cherry");
        System.out.println("otherSet: " + otherSet);
        // Output: [Apple, Cherry]

        // addAll (Union)
        HashSet<String> union = new HashSet<>(set);
        union.addAll(otherSet);
        System.out.println("Union (addAll): " + union);
        // Output: [Apple, Cherry]

        // retainAll (Intersection)
        HashSet<String> intersection = new HashSet<>(set);
        intersection.retainAll(otherSet);
        System.out.println("Intersection (retainAll): " + intersection);
        // Output: [Apple]

        // removeAll (Difference)
        HashSet<String> difference = new HashSet<>(union);
        difference.removeAll(set);
        System.out.println("Difference (removeAll): " + difference);
        // Output: [Cherry]

        // Iteration using for-each
        System.out.print("For-each iteration: ");
        for (String s : union) {
            System.out.print(s + " ");
        }
        System.out.println();
        // Output: Apple Cherry (order may vary)

        // Java 8 forEach
        System.out.print("forEach(): ");
        union.forEach(e -> System.out.print(e + " "));
        System.out.println();
        // Output: Apple Cherry (order may vary)

        // Convert to Array
        String[] array = union.toArray(new String[0]);
        System.out.println("Converted to array: " + Arrays.toString(array));
        // Output: [Apple, Cherry]

        // clear
        union.clear();
        System.out.println("After clear(): " + union);
        // Output: []

        // isEmpty again
        System.out.println("isEmpty(): " + union.isEmpty());
        // Output: true
    }
}
```

---



### LinkedHashSet

**Use Case:** When you need HashSet features with insertion order maintained


## 🔹 Creation

```java
LinkedHashSet<String> set = new LinkedHashSet<>();
```

---

## 🔹 Common Methods (Same as HashSet)

```java
set.add("Element");        // Adds element (false if duplicate)
set.remove("Element");     // Removes element
set.contains("Element");   // Checks existence
set.size();                // Returns size
set.isEmpty();             // Checks empty
set.clear();               // Removes all elements
```

---

## 🔹 Set Operations

```java
set.addAll(otherSet);      // Union
set.retainAll(otherSet);   // Intersection
set.removeAll(otherSet);   // Difference
```

---

## 🔹 Iteration (Insertion Order Preserved)

```java
for(String s : set) {
    System.out.println(s);
}

set.forEach(System.out::println);
```

---

## 🔹 Convert to Array

```java
String[] array = set.toArray(new String[0]);
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create LinkedHashSet
        LinkedHashSet<String> set = new LinkedHashSet<>();
        System.out.println("Initial set: " + set);
        // Output: []

        // add
        set.add("Apple");
        set.add("Banana");
        set.add("Cherry");
        set.add("Apple"); // duplicate
        System.out.println("After adding Apple, Banana, Cherry, Apple: " + set);
        // Output: [Apple, Banana, Cherry]

        // contains
        System.out.println("contains(\"Banana\"): " + set.contains("Banana"));
        // Output: true

        // remove
        set.remove("Banana");
        System.out.println("After remove(\"Banana\"): " + set);
        // Output: [Apple, Cherry]

        // size
        System.out.println("size(): " + set.size());
        // Output: 2

        // isEmpty
        System.out.println("isEmpty(): " + set.isEmpty());
        // Output: false

        // Another set
        LinkedHashSet<String> otherSet = new LinkedHashSet<>();
        otherSet.add("Cherry");
        otherSet.add("Date");
        System.out.println("otherSet: " + otherSet);
        // Output: [Cherry, Date]

        // addAll (Union)
        LinkedHashSet<String> union = new LinkedHashSet<>(set);
        union.addAll(otherSet);
        System.out.println("Union (addAll): " + union);
        // Output: [Apple, Cherry, Date]

        // retainAll (Intersection)
        LinkedHashSet<String> intersection = new LinkedHashSet<>(set);
        intersection.retainAll(otherSet);
        System.out.println("Intersection (retainAll): " + intersection);
        // Output: [Cherry]

        // removeAll (Difference)
        LinkedHashSet<String> difference = new LinkedHashSet<>(union);
        difference.removeAll(set);
        System.out.println("Difference (removeAll): " + difference);
        // Output: [Date]

        // Iteration using for-each
        System.out.print("For-each iteration: ");
        for (String s : union) {
            System.out.print(s + " ");
        }
        System.out.println();
        // Output: Apple Cherry Date

        // Java 8 forEach
        System.out.print("forEach(): ");
        union.forEach(e -> System.out.print(e + " "));
        System.out.println();
        // Output: Apple Cherry Date

        // Convert to Array
        String[] array = union.toArray(new String[0]);
        System.out.println("Converted to array: " + Arrays.toString(array));
        // Output: [Apple, Cherry, Date]

        // clear
        union.clear();
        System.out.println("After clear(): " + union);
        // Output: []

        // isEmpty again
        System.out.println("isEmpty(): " + union.isEmpty());
        // Output: true
    }
}
```

---


### TreeSet

**Use Case:** When you need sorted set (natural ordering or custom comparator


## 🔹 Creation

```java
TreeSet<String> set = new TreeSet<>();                          // Natural order
TreeSet<String> customSet = new TreeSet<>(Comparator.reverseOrder()); // Reverse order
```

---

## 🔹 Common Methods (Same as HashSet)

```java
set.add("Element");        // Adds element (false if duplicate)
set.remove("Element");     // Removes element
set.contains("Element");   // Checks existence
set.size();                // Returns size
set.isEmpty();             // Checks empty
set.clear();               // Removes all elements
```

---

## 🔹 Additional SortedSet / NavigableSet Methods

```java
set.first();               // Returns first (lowest) element
set.last();                // Returns last (highest) element
set.headSet("Element");    // Returns elements < element
set.tailSet("Element");    // Returns elements >= element
set.subSet("A", "Z");      // Returns elements in range [A, Z)
set.lower("Element");      // Greatest element < element
set.higher("Element");     // Least element > element
set.floor("Element");      // Greatest element <= element
set.ceiling("Element");    // Least element >= element
set.pollFirst();           // Removes & returns first
set.pollLast();            // Removes & returns last
set.descendingSet();       // Returns reverse order view
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create TreeSet
        TreeSet<String> set = new TreeSet<>();
        System.out.println("Initial TreeSet: " + set);
        // Output: []

        // add
        set.add("Apple");
        set.add("Banana");
        set.add("Cherry");
        set.add("Date");
        System.out.println("After adding elements: " + set);
        // Output: [Apple, Banana, Cherry, Date] (sorted order)

        // first & last
        System.out.println("first(): " + set.first());
        // Output: Apple
        System.out.println("last(): " + set.last());
        // Output: Date

        // headSet
        System.out.println("headSet(\"Cherry\"): " + set.headSet("Cherry"));
        // Output: [Apple, Banana]

        // tailSet
        System.out.println("tailSet(\"Cherry\"): " + set.tailSet("Cherry"));
        // Output: [Cherry, Date]

        // subSet
        System.out.println("subSet(\"Banana\", \"Date\"): " + set.subSet("Banana", "Date"));
        // Output: [Banana, Cherry]

        // lower & higher
        System.out.println("lower(\"Cherry\"): " + set.lower("Cherry"));
        // Output: Banana
        System.out.println("higher(\"Cherry\"): " + set.higher("Cherry"));
        // Output: Date

        // floor & ceiling
        System.out.println("floor(\"Blueberry\"): " + set.floor("Blueberry"));
        // Output: Banana
        System.out.println("ceiling(\"Blueberry\"): " + set.ceiling("Blueberry"));
        // Output: Cherry

        // pollFirst & pollLast
        System.out.println("pollFirst(): " + set.pollFirst());
        // Output: Apple
        System.out.println("After pollFirst(): " + set);
        // Output: [Banana, Cherry, Date]

        System.out.println("pollLast(): " + set.pollLast());
        // Output: Date
        System.out.println("After pollLast(): " + set);
        // Output: [Banana, Cherry]

        // descendingSet
        System.out.println("descendingSet(): " + set.descendingSet());
        // Output: [Cherry, Banana]

        // clear
        set.clear();
        System.out.println("After clear(): " + set);
        // Output: []

        System.out.println("isEmpty(): " + set.isEmpty());
        // Output: true
    }
}
```

---


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

## 🔹 Creation

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();                     // Min-heap
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder()); // Max-heap
```

---

## 🔹 Queue Methods

```java
pq.offer(10);        // Adds element, returns false if fails
pq.add(20);          // Adds element, throws exception if fails
pq.poll();           // Removes & returns head, null if empty
pq.remove();         // Removes & returns head, throws if empty
pq.peek();           // Returns head without removing, null if empty
pq.element();        // Returns head, throws if empty
pq.size();           // Returns number of elements
pq.isEmpty();        // Checks empty
pq.clear();          // Removes all elements
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create PriorityQueue (min-heap)
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        System.out.println("Initial PriorityQueue: " + pq);
        // Output: []

        // offer & add
        pq.offer(30);
        pq.add(10);
        pq.add(20);
        System.out.println("After adding 30, 10, 20: " + pq);
        // Output: [10, 30, 20] (min-heap, head = 10)

        // peek & element
        System.out.println("peek(): " + pq.peek());
        // Output: 10
        System.out.println("element(): " + pq.element());
        // Output: 10

        // poll & remove
        System.out.println("poll(): " + pq.poll());
        // Output: 10
        System.out.println("After poll(): " + pq);
        // Output: [20, 30]

        System.out.println("remove(): " + pq.remove());
        // Output: 20
        System.out.println("After remove(): " + pq);
        // Output: [30]

        // size & isEmpty
        System.out.println("size(): " + pq.size());
        // Output: 1
        System.out.println("isEmpty(): " + pq.isEmpty());
        // Output: false

        // clear
        pq.clear();
        System.out.println("After clear(): " + pq);
        // Output: []
        System.out.println("isEmpty(): " + pq.isEmpty());
        // Output: true

        // Max-heap example
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
        maxHeap.add(50);
        maxHeap.add(10);
        maxHeap.add(30);
        System.out.println("Max-heap elements: " + maxHeap);
        // Output: [50, 10, 30] (head = 50)
        System.out.println("peek(): " + maxHeap.peek());
        // Output: 50
    }
}
```

---

**Time Complexity:**
- Offer/Add: O(log n)
- Poll/Remove: O(log n)
- Peek: O(1)

---

### ArrayDeque

**Use Case:** Double-ended queue, faster than LinkedList for both stack and queue operations


## 🔹 Creation

```java
ArrayDeque<String> deque = new ArrayDeque<>();
```

---

## 🔹 Queue Methods (FIFO)

```java
deque.offer("Element");   // Adds to end
deque.poll();             // Removes from beginning, returns null if empty
deque.peek();             // Views beginning, returns null if empty
```

---

## 🔹 Deque Methods

```java
deque.offerFirst("First");   // Adds to beginning
deque.offerLast("Last");     // Adds to end
deque.pollFirst();           // Removes from beginning
deque.pollLast();            // Removes from end
deque.peekFirst();           // Views beginning
deque.peekLast();            // Views end
```

---

## 🔹 Stack Methods (LIFO)

```java
deque.push("Element");       // Adds to beginning
deque.pop();                 // Removes from beginning
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create ArrayDeque
        ArrayDeque<String> deque = new ArrayDeque<>();
        System.out.println("Initial deque: " + deque);
        // Output: []

        // Queue (FIFO) operations
        deque.offer("A");
        deque.offer("B");
        deque.offer("C");
        System.out.println("After offer(A, B, C): " + deque);
        // Output: [A, B, C]

        System.out.println("peek(): " + deque.peek());
        // Output: A
        System.out.println("poll(): " + deque.poll());
        // Output: A
        System.out.println("After poll(): " + deque);
        // Output: [B, C]

        // Deque operations
        deque.offerFirst("X");
        deque.offerLast("Y");
        System.out.println("After offerFirst(X) and offerLast(Y): " + deque);
        // Output: [X, B, C, Y]

        System.out.println("peekFirst(): " + deque.peekFirst());
        // Output: X
        System.out.println("peekLast(): " + deque.peekLast());
        // Output: Y

        System.out.println("pollFirst(): " + deque.pollFirst());
        // Output: X
        System.out.println("pollLast(): " + deque.pollLast());
        // Output: Y
        System.out.println("After pollFirst & pollLast: " + deque);
        // Output: [B, C]

        // Stack (LIFO) operations
        deque.push("M");
        deque.push("N");
        System.out.println("After push(M, N): " + deque);
        // Output: [N, M, B, C]

        System.out.println("pop(): " + deque.pop());
        // Output: N
        System.out.println("After pop(): " + deque);
        // Output: [M, B, C]

        // Size and isEmpty
        System.out.println("size(): " + deque.size());
        // Output: 3
        System.out.println("isEmpty(): " + deque.isEmpty());
        // Output: false

        // Clear
        deque.clear();
        System.out.println("After clear(): " + deque);
        // Output: []
    }
}
```

---



## Map Interface

**Characteristics:**
- Key-value pairs
- No duplicate keys
- Each key maps to at most one value

### HashMap

**Use Case:** When you need fast key-value lookups and don't care about order


## 🔹 Creation

```java
HashMap<String, Integer> map = new HashMap<>();
```

---

## 🔹 Common Methods

```java
map.put("Key", 100);             // Adds/updates entry
map.get("Key");                  // Returns value (null if not found)
map.getOrDefault("Key", 0);      // Returns value or default
map.remove("Key");               // Removes entry
map.containsKey("Key");          // Checks if key exists
map.containsValue(100);          // Checks if value exists
map.size();                      // Number of entries
map.isEmpty();                   // Checks if empty
map.clear();                      // Removes all entries
```

---

## 🔹 Bulk Operations

```java
map.putAll(otherMap);             // Copies all entries
map.putIfAbsent("Key", 100);      // Only adds if key absent
```

---

## 🔹 Java 8+ Methods

```java
map.computeIfAbsent("Key", k -> 100);          // Computes only if absent
map.computeIfPresent("Key", (k, v) -> v + 1); // Computes only if present
map.compute("Key", (k, v) -> (v == null) ? 1 : v + 1);
map.merge("Key", 1, Integer::sum);            // Merges value with existing
map.replace("Key", 100);                      // Replaces value for key
map.replace("Key", 100, 200);                // Replace only if current value matches
```

---

## 🔹 Iteration

```java
for(String key : map.keySet()) {
    System.out.println(key);                  // Iterates over keys
}

for(Integer value : map.values()) {
    System.out.println(value);                // Iterates over values
}

for(Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue()); // Iterates entries
}

map.forEach((k, v) -> System.out.println(k + ": " + v));           // Java 8+
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create HashMap
        HashMap<String, Integer> map = new HashMap<>();
        System.out.println("Initial map: " + map);
        // Output: {}

        // put
        map.put("A", 10);
        map.put("B", 20);
        map.put("C", 30);
        System.out.println("After put A,B,C: " + map);
        // Output: {A=10, B=20, C=30} (order may vary)

        // get & getOrDefault
        System.out.println("get(\"A\"): " + map.get("A"));
        // Output: 10
        System.out.println("getOrDefault(\"D\", 0): " + map.getOrDefault("D", 0));
        // Output: 0

        // containsKey & containsValue
        System.out.println("containsKey(\"B\"): " + map.containsKey("B"));
        // Output: true
        System.out.println("containsValue(50): " + map.containsValue(50));
        // Output: false

        // remove
        map.remove("C");
        System.out.println("After remove(\"C\"): " + map);
        // Output: {A=10, B=20}

        // size & isEmpty
        System.out.println("size(): " + map.size());
        // Output: 2
        System.out.println("isEmpty(): " + map.isEmpty());
        // Output: false

        // putIfAbsent
        map.putIfAbsent("B", 50);
        map.putIfAbsent("D", 40);
        System.out.println("After putIfAbsent: " + map);
        // Output: {A=10, B=20, D=40}

        // computeIfAbsent
        map.computeIfAbsent("E", k -> 100);
        System.out.println("After computeIfAbsent(\"E\"): " + map);
        // Output: {A=10, B=20, D=40, E=100}

        // computeIfPresent
        map.computeIfPresent("B", (k, v) -> v + 5);
        System.out.println("After computeIfPresent(\"B\"): " + map);
        // Output: {A=10, B=25, D=40, E=100}

        // compute
        map.compute("A", (k, v) -> v * 2);
        System.out.println("After compute(\"A\"): " + map);
        // Output: {A=20, B=25, D=40, E=100}

        // merge
        map.merge("D", 10, Integer::sum);
        System.out.println("After merge(\"D\",10): " + map);
        // Output: {A=20, B=25, D=50, E=100}

        // replace
        map.replace("E", 200);
        map.replace("B", 25, 30);
        System.out.println("After replace operations: " + map);
        // Output: {A=20, B=30, D=50, E=200}

        // Iteration
        System.out.print("Keys: ");
        for(String key : map.keySet()) System.out.print(key + " ");
        System.out.println();
        // Output: Keys: A B D E

        System.out.print("Values: ");
        for(Integer value : map.values()) System.out.print(value + " ");
        System.out.println();
        // Output: Values: 20 30 50 200

        System.out.println("Entries:");
        for(Map.Entry<String,Integer> entry : map.entrySet())
            System.out.println(entry.getKey() + ": " + entry.getValue());
        // Output: A:20 B:30 D:50 E:200

        System.out.println("forEach:");
        map.forEach((k,v) -> System.out.println(k + ": " + v));
        // Output: A:20 B:30 D:50 E:200

        // clear
        map.clear();
        System.out.println("After clear(): " + map);
        // Output: {}
        System.out.println("isEmpty(): " + map.isEmpty());
        // Output: true
    }
}
```

---


**Time Complexity:**
- Put: O(1)
- Get: O(1)
- Remove: O(1)
- ContainsKey: O(1)

---

### LinkedHashMap

**Use Case:** When you need HashMap features with insertion/access order maintained


## 🔹 Creation

```java
// Insertion order (default)
LinkedHashMap<String, Integer> map = new LinkedHashMap<>();

// Access order (true): useful for LRU cache
LinkedHashMap<String, Integer> accessOrderMap = new LinkedHashMap<>(16, 0.75f, true);
```

---

## 🔹 Methods (Same as HashMap)

```java
map.put("Key", 100);              // Adds/updates entry
map.get("Key");                   // Returns value, null if not found
map.getOrDefault("Key", 0);       // Returns value or default
map.remove("Key");                // Removes entry
map.containsKey("Key");           // Checks key existence
map.containsValue(100);           // Checks value existence
map.size();
map.isEmpty();
map.clear();
map.putAll(otherMap);
map.putIfAbsent("Key", 100);     
map.computeIfAbsent("Key", k -> 100);
map.computeIfPresent("Key", (k, v) -> v + 1);
map.compute("Key", (k, v) -> (v == null) ? 1 : v + 1);
map.merge("Key", 1, Integer::sum);
map.replace("Key", 100);
map.replace("Key", 100, 200);

// Iteration
for(String key : map.keySet()) System.out.println(key);
for(Integer value : map.values()) System.out.println(value);
for(Map.Entry<String, Integer> entry : map.entrySet())
    System.out.println(entry.getKey() + ": " + entry.getValue());
map.forEach((k, v) -> System.out.println(k + ": " + v));
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create LinkedHashMap (insertion order)
        LinkedHashMap<String, Integer> map = new LinkedHashMap<>();
        map.put("A", 10);
        map.put("B", 20);
        map.put("C", 30);
        System.out.println("Initial map: " + map);
        // Output: {A=10, B=20, C=30} (insertion order)

        // Accessing an element does NOT change order in default map
        map.get("B");
        System.out.println("After get(\"B\"): " + map);
        // Output: {A=10, B=20, C=30}

        // Using access-order map (LRU)
        LinkedHashMap<String, Integer> lruMap = new LinkedHashMap<>(16, 0.75f, true);
        lruMap.put("X", 100);
        lruMap.put("Y", 200);
        lruMap.put("Z", 300);
        System.out.println("Access-order map: " + lruMap);
        // Output: {X=100, Y=200, Z=300}

        // Access element to move it to end
        lruMap.get("Y");
        System.out.println("After get(\"Y\"): " + lruMap);
        // Output: {X=100, Z=300, Y=200} (Y moved to end)

        // Iteration
        System.out.println("Keys:");
        for(String key : map.keySet()) System.out.print(key + " ");
        System.out.println();
        // Output: Keys: A B C

        System.out.println("Values:");
        for(Integer val : map.values()) System.out.print(val + " ");
        System.out.println();
        // Output: Values: 10 20 30

        System.out.println("Entries:");
        for(Map.Entry<String,Integer> entry : map.entrySet())
            System.out.println(entry.getKey() + ": " + entry.getValue());
        // Output: 
        // A: 10
        // B: 20
        // C: 30

        // Clear
        map.clear();
        System.out.println("After clear(): " + map);
        // Output: {}
    }
}
```

---

### TreeMap

**Use Case:** When you need sorted map (by keys)


## 🔹 Creation

```java
// Natural order (ascending)
TreeMap<String, Integer> map = new TreeMap<>();

// Reverse order
TreeMap<String, Integer> reverseMap = new TreeMap<>(Comparator.reverseOrder());
```

---

## 🔹 Map Methods (Same as HashMap)

```java
map.put("Key", 100);             // Adds/updates entry
map.get("Key");                  // Returns value, null if not found
map.getOrDefault("Key", 0);      // Returns value or default
map.remove("Key");               // Removes entry
map.containsKey("Key");          // Checks key existence
map.containsValue(100);          // Checks value existence
map.size();
map.isEmpty();
map.clear();
map.putAll(otherMap);
map.putIfAbsent("Key", 100);     
map.computeIfAbsent("Key", k -> 100);
map.computeIfPresent("Key", (k, v) -> v + 1);
map.compute("Key", (k, v) -> (v == null) ? 1 : v + 1);
map.merge("Key", 1, Integer::sum);
map.replace("Key", 100);
map.replace("Key", 100, 200);
```

---

## 🔹 NavigableMap Methods

```java
map.firstKey();                  // Returns first (lowest) key
map.lastKey();                   // Returns last (highest) key
map.firstEntry();                // Returns first entry
map.lastEntry();                 // Returns last entry
map.lowerKey("Key");             // Greatest key < given key
map.higherKey("Key");            // Least key > given key
map.floorKey("Key");             // Greatest key <= given key
map.ceilingKey("Key");           // Least key >= given key
map.pollFirstEntry();            // Removes & returns first entry
map.pollLastEntry();             // Removes & returns last entry
map.headMap("Key");              // Returns keys < given key
map.tailMap("Key");              // Returns keys >= given key
map.subMap("A", "Z");            // Returns keys in [A, Z)
map.descendingMap();             // Returns reverse order view
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create TreeMap
        TreeMap<String, Integer> map = new TreeMap<>();
        map.put("C", 30);
        map.put("A", 10);
        map.put("B", 20);
        System.out.println("Initial TreeMap: " + map);
        // Output: {A=10, B=20, C=30} (sorted by key)

        // firstKey & lastKey
        System.out.println("firstKey(): " + map.firstKey());
        // Output: A
        System.out.println("lastKey(): " + map.lastKey());
        // Output: C

        // firstEntry & lastEntry
        System.out.println("firstEntry(): " + map.firstEntry());
        // Output: A=10
        System.out.println("lastEntry(): " + map.lastEntry());
        // Output: C=30

        // lowerKey, higherKey, floorKey, ceilingKey
        System.out.println("lowerKey(\"B\"): " + map.lowerKey("B"));
        // Output: A
        System.out.println("higherKey(\"B\"): " + map.higherKey("B"));
        // Output: C
        System.out.println("floorKey(\"B\"): " + map.floorKey("B"));
        // Output: B
        System.out.println("ceilingKey(\"B\"): " + map.ceilingKey("B"));
        // Output: B

        // pollFirstEntry & pollLastEntry
        System.out.println("pollFirstEntry(): " + map.pollFirstEntry());
        // Output: A=10
        System.out.println("pollLastEntry(): " + map.pollLastEntry());
        // Output: C=30
        System.out.println("After polling: " + map);
        // Output: {B=20}

        // headMap, tailMap, subMap
        map.put("A", 10);
        map.put("C", 30);
        System.out.println("map.headMap(\"B\"): " + map.headMap("B"));
        // Output: {A=10}
        System.out.println("map.tailMap(\"B\"): " + map.tailMap("B"));
        // Output: {B=20, C=30}
        System.out.println("map.subMap(\"A\", \"C\"): " + map.subMap("A", "C"));
        // Output: {A=10, B=20}

        // descendingMap
        System.out.println("map.descendingMap(): " + map.descendingMap());
        // Output: {C=30, B=20, A=10}
    }
}
```

---

**Time Complexity:**
- Put: O(log n)
- Get: O(log n)
- Remove: O(log n)

---

### Hashtable

**Use Case:** Legacy thread-safe map (prefer ConcurrentHashMap)


## 🔹 Creation

```java
Hashtable<String, Integer> table = new Hashtable<>();
```

---

## 🔹 Methods (Same as HashMap)

```java
table.put("Key", 100);              // Adds/updates entry
table.get("Key");                   // Returns value, null if not found
table.remove("Key");                // Removes entry
table.containsKey("Key");           // Checks key existence
table.containsValue(100);           // Checks value existence
table.size();
table.isEmpty();
table.clear();
table.putAll(otherTable);
table.putIfAbsent("Key", 100);      // Adds only if key absent

// Iteration
for(String key : table.keySet()) System.out.println(key);
for(Integer value : table.values()) System.out.println(value);
for(Map.Entry<String, Integer> entry : table.entrySet())
    System.out.println(entry.getKey() + ": " + entry.getValue());
table.forEach((k,v) -> System.out.println(k + ": " + v));
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        // Create Hashtable
        Hashtable<String, Integer> table = new Hashtable<>();
        System.out.println("Initial table: " + table);
        // Output: {}

        // put
        table.put("A", 10);
        table.put("B", 20);
        table.put("C", 30);
        System.out.println("After put A,B,C: " + table);
        // Output: {A=10, B=20, C=30} (order not guaranteed)

        // get
        System.out.println("get(\"B\"): " + table.get("B"));
        // Output: 20

        // containsKey & containsValue
        System.out.println("containsKey(\"C\"): " + table.containsKey("C"));
        // Output: true
        System.out.println("containsValue(50): " + table.containsValue(50));
        // Output: false

        // remove
        table.remove("A");
        System.out.println("After remove(\"A\"): " + table);
        // Output: {B=20, C=30}

        // size & isEmpty
        System.out.println("size(): " + table.size());
        // Output: 2
        System.out.println("isEmpty(): " + table.isEmpty());
        // Output: false

        // putIfAbsent
        table.putIfAbsent("B", 50);  // ignored, B exists
        table.putIfAbsent("D", 40);  // added
        System.out.println("After putIfAbsent: " + table);
        // Output: {B=20, C=30, D=40}

        // Iteration
        System.out.println("Keys:");
        for(String key : table.keySet()) System.out.print(key + " ");
        System.out.println();
        // Output: Keys: B C D

        System.out.println("Values:");
        for(Integer value : table.values()) System.out.print(value + " ");
        System.out.println();
        // Output: Values: 20 30 40

        System.out.println("Entries:");
        for(Map.Entry<String,Integer> entry : table.entrySet())
            System.out.println(entry.getKey() + ": " + entry.getValue());
        // Output:
        // B: 20
        // C: 30
        // D: 40

        System.out.println("forEach:");
        table.forEach((k,v) -> System.out.println(k + ": " + v));
        // Output:
        // B: 20
        // C: 30
        // D: 40

        // clear
        table.clear();
        System.out.println("After clear(): " + table);
        // Output: {}
        System.out.println("isEmpty(): " + table.isEmpty());
        // Output: true
    }
}
```


---

## Utility Classes

### Collections Class


### 1️⃣ Sorting

```java
Collections.sort(list);                      // Ascending order
Collections.sort(list, Comparator.reverseOrder());  // Descending order
```

### 2️⃣ Searching

```java
Collections.binarySearch(list, "Element");  // Requires sorted list
```

### 3️⃣ Shuffling

```java
Collections.shuffle(list);                   // Randomizes elements
```

### 4️⃣ Reversing

```java
Collections.reverse(list);                   // Reverses the list
```

### 5️⃣ Filling

```java
Collections.fill(list, "Default");          // Replaces all elements
```

### 6️⃣ Copying

```java
Collections.copy(destList, srcList);        // Copies src to dest
```

### 7️⃣ Min / Max

```java
Collections.min(list);                       // Smallest element
Collections.max(list);                       // Largest element
```

### 8️⃣ Frequency

```java
Collections.frequency(list, "Element");     // Count occurrences
```

### 9️⃣ Disjoint Check

```java
Collections.disjoint(list1, list2);         // True if no common elements
```

---

## 🔹 Synchronization

```java
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Set<String> syncSet = Collections.synchronizedSet(new HashSet<>());
Map<String, Integer> syncMap = Collections.synchronizedMap(new HashMap<>());
```

* Ensures thread-safe access to collections
* Useful in multithreaded programs

---

## 🔹 Unmodifiable Collections

```java
List<String> unmodList = Collections.unmodifiableList(list);
Set<String> unmodSet = Collections.unmodifiableSet(set);
Map<String, Integer> unmodMap = Collections.unmodifiableMap(map);
```

* Throws `UnsupportedOperationException` on modification

---

## 🔹 Empty Collections

```java
Collections.emptyList();
Collections.emptySet();
Collections.emptyMap();
```

* Returns immutable empty collections
* Useful for safe defaults

---

## 🔹 Singleton Collections

```java
Collections.singleton("Element");          // Single object set
Collections.singletonList("Element");      // Single object list
Collections.singletonMap("Key", "Value");  // Single key-value map
```

* Immutable collections with a single element

---

## 🔹 Adding Elements

```java
Collections.addAll(list, "A", "B", "C");   // Adds multiple elements
```

---

## 🔹 Rotating

```java
Collections.rotate(list, 2);               // Rotates elements by n positions
```

---

## 🔹 Replacing

```java
Collections.replaceAll(list, "Old", "New"); // Replaces all occurrences
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        List<String> list = new ArrayList<>();
        Collections.addAll(list, "B", "A", "C", "A");
        System.out.println("Initial list: " + list);
        // Output: [B, A, C, A]

        // Sorting
        Collections.sort(list);
        System.out.println("After sort: " + list);
        // Output: [A, A, B, C]

        Collections.sort(list, Comparator.reverseOrder());
        System.out.println("After reverse sort: " + list);
        // Output: [C, B, A, A]

        // Searching (binary search requires sorted list)
        Collections.sort(list);
        int index = Collections.binarySearch(list, "B");
        System.out.println("Index of B: " + index);
        // Output: 2

        // Shuffling
        Collections.shuffle(list);
        System.out.println("After shuffle: " + list);
        // Output: [A, C, A, B] (example)

        // Reversing
        Collections.reverse(list);
        System.out.println("After reverse: " + list);
        // Output: [B, A, C, A]

        // Filling
        Collections.fill(list, "X");
        System.out.println("After fill: " + list);
        // Output: [X, X, X, X]

        // Frequency
        Collections.addAll(list, "Y", "X", "Z", "X");
        int freq = Collections.frequency(list, "X");
        System.out.println("Frequency of X: " + freq);
        // Output: 3

        // Min / Max
        System.out.println("Min: " + Collections.min(list));
        // Output: X
        System.out.println("Max: " + Collections.max(list));
        // Output: Z

        // Rotating
        Collections.rotate(list, 2);
        System.out.println("After rotate by 2: " + list);
        // Output: [X, X, X, Z, Y, X] (example)

        // Replacing
        Collections.replaceAll(list, "X", "M");
        System.out.println("After replaceAll X -> M: " + list);
        // Output: [M, M, M, Z, Y, M]
    }
}
```



---

### Arrays Class



### 1️⃣ Sorting

```java
Arrays.sort(array);                       // Ascending order
Arrays.sort(array, Comparator.reverseOrder());  // Descending order (Objects)
```

### 2️⃣ Searching

```java
Arrays.binarySearch(array, "Element");   // Requires sorted array
```

### 3️⃣ Copying

```java
int[] copy = Arrays.copyOf(array, newLength);
int[] rangeCopy = Arrays.copyOfRange(array, from, to);
```

### 4️⃣ Filling

```java
Arrays.fill(array, "Default");           // Fills array with value
```

### 5️⃣ Comparing

```java
Arrays.equals(array1, array2);           // True if arrays are equal
Arrays.deepEquals(array1, array2);       // For multidimensional arrays
```

### 6️⃣ Converting

```java
List<String> list = Arrays.asList("A", "B", "C");  // Fixed-size list
```

### 7️⃣ Streaming

```java
Arrays.stream(array).forEach(System.out::println);
```

### 8️⃣ Parallel Sorting

```java
Arrays.parallelSort(array);               // Faster for large arrays
```

### 9️⃣ toString / deepToString

```java
Arrays.toString(array);                   // Converts array to string
Arrays.deepToString(multiArray);         // Converts multi-dimensional array to string
```

---

## 🔹 Complete Example with Step-by-Step Output

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        String[] array = {"B", "A", "C", "A"};
        System.out.println("Initial array: " + Arrays.toString(array));
        // Output: [B, A, C, A]

        // Sorting
        Arrays.sort(array);
        System.out.println("After sort: " + Arrays.toString(array));
        // Output: [A, A, B, C]

        Arrays.sort(array, Comparator.reverseOrder());
        System.out.println("After reverse sort: " + Arrays.toString(array));
        // Output: [C, B, A, A]

        // Searching (binary search requires sorted array)
        Arrays.sort(array);
        int index = Arrays.binarySearch(array, "B");
        System.out.println("Index of B: " + index);
        // Output: 2

        // Copying
        String[] copy = Arrays.copyOf(array, array.length);
        System.out.println("Copy of array: " + Arrays.toString(copy));
        // Output: [A, A, B, C]

        String[] rangeCopy = Arrays.copyOfRange(array, 1, 3);
        System.out.println("Range copy (1,3): " + Arrays.toString(rangeCopy));
        // Output: [A, B]

        // Filling
        Arrays.fill(array, "X");
        System.out.println("After fill: " + Arrays.toString(array));
        // Output: [X, X, X, X]

        // Comparing
        String[] arr1 = {"A", "B"};
        String[] arr2 = {"A", "B"};
        System.out.println("Arrays.equals: " + Arrays.equals(arr1, arr2));
        // Output: true

        String[][] multiArr1 = {{"A","B"}, {"C"}};
        String[][] multiArr2 = {{"A","B"}, {"C"}};
        System.out.println("Arrays.deepEquals: " + Arrays.deepEquals(multiArr1, multiArr2));
        // Output: true

        // Converting to List
        List<String> list = Arrays.asList("A", "B", "C");
        System.out.println("As List: " + list);
        // Output: [A, B, C]

        // Streaming
        System.out.print("Stream: ");
        Arrays.stream(array).forEach(e -> System.out.print(e + " "));
        System.out.println();
        // Output: Stream: X X X X

        // Parallel Sorting
        String[] largeArray = {"Z","Y","X"};
        Arrays.parallelSort(largeArray);
        System.out.println("Parallel sorted: " + Arrays.toString(largeArray));
        // Output: [X, Y, Z]

        // toString / deepToString
        String[][] multiArray = {{"A","B"},{"C","D"}};
        System.out.println("deepToString: " + Arrays.deepToString(multiArray));
        // Output: [[A, B], [C, D]]
    }
}
```



---


## Performance Comparison

| Operation | ArrayList | LinkedList | Vector | Stack | HashSet | LinkedHashSet | TreeSet  | HashMap | LinkedHashMap | TreeMap  | Hashtable | PriorityQueue | ArrayDeque |      |
| --------- | --------- | ---------- | ------ | ----- | ------- | ------------- | -------- | ------- | ------------- | -------- | --------- | ------------- | ---------- | ---- |
| Add       | O(1)*     | O(1)**     | O(1)*  | O(1)  | O(1)    | O(1)          | O(log n) | O(1)    | O(1)          | O(log n) | O(1)      | O(log n)      | O(log n)   | O(1) |
| Remove    | O(n)      | O(1)**     | O(n)   | O(n)  | O(1)    | O(1)          | O(log n) | O(1)    | O(1)          | O(log n) | O(1)      | O(log n)      | O(log n)   | O(1) |
| Get       | O(1)      | O(n)       | O(1)   | O(n)  | N/A     | N/A           | N/A      | O(1)    | O(1)          | O(log n) | O(1)      | O(1)          | O(n)       | O(1) |
| Contains  | O(n)      | O(n)       | O(n)   | O(n)  | O(1)    | O(1)          | O(log n) | O(1)    | O(1)          | O(log n) | O(1)      | O(n)          | O(n)       | O(n) |
| Iteration | Fast      | Fast       | Fast   | Fast  | Fast    | Fast          | Fast     | Fast    | Fast          | Fast     | Fast      | Fast          | Fast       |      |

*Amortized, **if node is known

---

## Choosing the Right Collection

**ArrayList**

* Fast random access
* Iterate more than insert/delete
* Mostly add at the end

**LinkedList**

* Frequent insert/delete at beginning or middle
* Implementing queue or deque
* Random access is rare

**Vector**

* Similar to `ArrayList` but synchronized (legacy)
* Use in multithreaded legacy code

**Stack**

* LIFO operations
* Legacy, use `ArrayDeque` for modern implementation

**HashSet**

* Unique elements
* Order doesn't matter
* Fast add/remove/contains

**LinkedHashSet**

* Unique elements
* Maintains insertion order
* Fast add/remove/contains

**TreeSet**

* Unique elements in sorted order
* Range operations available

**HashMap**

* Key-value pairs
* Order doesn't matter
* Fast lookup

**LinkedHashMap**

* Key-value pairs
* Maintains insertion order
* Fast lookup

**TreeMap**

* Key-value pairs in sorted key order
* Range operations available

**Hashtable**

* Legacy synchronized key-value map
* No null keys/values
* Thread-safe

**PriorityQueue**

* Elements processed by priority
* Implements min/max heap
* Heap-based algorithms

**ArrayDeque**

* Stack or queue operations
* Better performance than `LinkedList`

**Concurrent Collections** (Optional, for multithreading)

* `ConcurrentHashMap`, `CopyOnWriteArrayList`
* Thread-safe without blocking

---

