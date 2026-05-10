# Java Data Structures — Quick Reference

---

## 1. Array
A fixed-size, indexed collection of elements of the same type.
```java
int[] arr = {10, 20, 30, 40};
arr[2] = 99;                   // update index 2
System.out.println(arr[2]);    // 99
```

---

## 2. ArrayList
A resizable array backed by a dynamic list from `java.util`.
```java
ArrayList<String> list = new ArrayList<>();
list.add("Alice");
list.add("Bob");
list.remove("Alice");          // ["Bob"]
```

---

## 3. LinkedList
A doubly-linked list where each node holds a value and pointers to its neighbors.
```java
LinkedList<Integer> ll = new LinkedList<>();
ll.addFirst(1);
ll.addLast(2);
ll.removeFirst();              // [2]
```

---

## 4. Stack
A LIFO (Last-In, First-Out) structure — the last element pushed is the first popped.
```java
Stack<Integer> stack = new Stack<>();
stack.push(1); stack.push(2); stack.push(3);
System.out.println(stack.pop());   // 3
System.out.println(stack.peek());  // 2 (no removal)
```

---

## 5. Queue
A FIFO (First-In, First-Out) structure — elements are added at the rear and removed from the front.
```java
Queue<String> queue = new LinkedList<>();
queue.offer("first"); queue.offer("second");
System.out.println(queue.poll());  // "first"
System.out.println(queue.peek());  // "second"
```

---

## 6. Deque (Double-Ended Queue)
A queue that allows insertion and removal from **both** ends.
```java
Deque<Integer> deque = new ArrayDeque<>();
deque.addFirst(1); deque.addLast(2); deque.addFirst(0);
System.out.println(deque.pollFirst()); // 0
System.out.println(deque.pollLast());  // 2
```

---

## 7. PriorityQueue
A queue that always dequeues the **smallest** (or highest-priority) element first.
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(50); pq.offer(10); pq.offer(30);
System.out.println(pq.poll()); // 10 (min first)
System.out.println(pq.poll()); // 30
```

---

## 8. HashMap
A key-value store using hashing — O(1) average lookup, no guaranteed order.
```java
HashMap<String, Integer> map = new HashMap<>();
map.put("apple", 3); map.put("banana", 5);
System.out.println(map.get("apple"));      // 3
System.out.println(map.containsKey("banana")); // true
```

---

## 9. LinkedHashMap
A `HashMap` that preserves **insertion order** when iterating.
```java
LinkedHashMap<String, Integer> lhm = new LinkedHashMap<>();
lhm.put("one", 1); lhm.put("two", 2); lhm.put("three", 3);
lhm.forEach((k, v) -> System.out.print(k + " ")); // one two three
```

---

## 10. TreeMap
A sorted map that keeps keys in **natural ascending order** (backed by a Red-Black tree).
```java
TreeMap<String, Integer> tm = new TreeMap<>();
tm.put("banana", 2); tm.put("apple", 1); tm.put("cherry", 3);
System.out.println(tm.firstKey()); // "apple"
System.out.println(tm.lastKey());  // "cherry"
```

---

## 11. HashSet
An unordered collection of **unique** elements — duplicates are silently ignored.
```java
HashSet<String> set = new HashSet<>();
set.add("cat"); set.add("dog"); set.add("cat"); // duplicate ignored
System.out.println(set.size());        // 2
System.out.println(set.contains("dog")); // true
```

---

## 12. LinkedHashSet
A `HashSet` that remembers **insertion order** when iterating.
```java
LinkedHashSet<String> lhs = new LinkedHashSet<>();
lhs.add("z"); lhs.add("a"); lhs.add("m");
lhs.forEach(System.out::println); // z, a, m (in order added)
```

---

## 13. TreeSet
A sorted set that keeps elements in **natural ascending order** with no duplicates.
```java
TreeSet<Integer> ts = new TreeSet<>();
ts.add(5); ts.add(1); ts.add(3);
System.out.println(ts.first()); // 1
System.out.println(ts);         // [1, 3, 5]
```

---

## 14. 2D Array (Matrix)
A grid of elements accessed by two indices: row and column.
```java
int[][] matrix = {{1, 2}, {3, 4}, {5, 6}};
System.out.println(matrix[1][0]); // 3 (row 1, col 0)
matrix[2][1] = 99;
System.out.println(matrix[2][1]); // 99
```

---

## 15. String as Array of Characters
A `String` can be treated as a sequence of characters accessible by index.
```java
String s = "hello";
char[] chars = s.toCharArray();
System.out.println(chars[1]);           // 'e'
System.out.println(new String(chars));  // "hello"
```

---

## 16. BitSet
A compact array of bits (booleans) useful for memory-efficient flag storage.
```java
BitSet bs = new BitSet(8);
bs.set(1); bs.set(4); bs.set(7);
System.out.println(bs);          // {1, 4, 7}
System.out.println(bs.get(4));   // true
```

---

## 17. ArrayDeque (as Stack replacement)
A faster, modern alternative to `Stack` — can be used as both a stack and a queue.
```java
ArrayDeque<Integer> ads = new ArrayDeque<>();
ads.push(10); ads.push(20); ads.push(30);
System.out.println(ads.pop());   // 30 (LIFO)
System.out.println(ads.peek());  // 20
```

---

## 18. Collections Utility Methods
`Collections` provides helper algorithms that work on any `Collection`.
```java
List<Integer> nums = new ArrayList<>(Arrays.asList(3, 1, 4, 1, 5));
Collections.sort(nums);
System.out.println(Collections.max(nums)); // 5
Collections.reverse(nums);
System.out.println(nums); // [5, 4, 3, 1, 1]
```

---

## 19. Arrays Utility Methods
`Arrays` provides helpers for sorting, searching, and printing arrays.
```java
int[] arr = {5, 2, 8, 1};
Arrays.sort(arr);
System.out.println(Arrays.binarySearch(arr, 8)); // 3
System.out.println(Arrays.toString(arr));         // [1, 2, 5, 8]
```

---

## 20. Iterator
A universal cursor to traverse any `Collection` without exposing its internal structure.
```java
List<String> items = new ArrayList<>(Arrays.asList("a", "b", "c"));
Iterator<String> it = items.iterator();
while (it.hasNext()) System.out.print(it.next() + " "); // a b c
```

---

> **Tip:** When choosing a structure, ask yourself:
> - Need **fast lookup by key**? → `HashMap`
> - Need **sorted order**? → `TreeMap` / `TreeSet`
> - Need **LIFO**? → `ArrayDeque` (as stack)
> - Need **FIFO**? → `LinkedList` / `ArrayDeque` (as queue)
> - Need **priority ordering**? → `PriorityQueue`
> - Need **unique elements**? → `HashSet` / `TreeSet`