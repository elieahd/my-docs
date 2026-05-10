# Java Interview Questions & Answers

---

## Basics

**1. What is Java and why is it platform independent?**

- Java compiles your code into **bytecode**, not machine code
- Bytecode runs on any machine that has a JVM installed
- So you write it once, it runs on Windows, Mac, Linux, no changes needed
- That's the famous "Write Once, Run Anywhere" idea

---

**2. Explain the concept of object-oriented programming.**

- You organize your code around **objects** instead of functions
- An object has data (fields) and things it can do (methods)
- Think of a `Car`, it has a brand, a speed, and can accelerate
- OOP has 4 pillars: **encapsulation, inheritance, polymorphism, abstraction**

```java
class Animal {
    String name;

    void speak() {
        System.out.println("...");
    }
}

class Dog extends Animal {
    void speak() {
        System.out.println("Woof!");
    }
}
```

---

**3. What are the main features of Java?**

- Platform independent (thanks to the JVM)
- Strongly typed, the compiler catches type errors early
- Automatic memory management via garbage collection
- Built-in multithreading support
- Rich standard library out of the box
- Security features baked right into the runtime

---

## JVM / JDK

**4. What is the Java Virtual Machine (JVM)?**

- It's the engine that actually runs your Java code
- It takes the bytecode and executes it on your machine
- It also manages memory, runs the garbage collector, and JIT-compiles hot code to native instructions

---

**5. What's the difference between JDK, JRE and JVM?**

- **JVM**, runs the bytecode, that's it
- **JRE**, JVM + the standard Java libraries (enough to run a program)
- **JDK**, JRE + compiler + debugger + dev tools (what you need to build programs)
- Rule of thumb: users need JRE, developers need JDK

---

**6. Explain the Java garbage collection process.**

- Java handles memory for you, you don't free objects manually
- When an object has no more references, it becomes eligible for GC
- The heap is split into generations: Eden → Survivor → Old Gen
- Objects get promoted as they survive more GC cycles
- Modern collectors like G1 and ZGC minimize pause times

```java
// You can hint at it, but never force it
System.gc();
```

---

## OOP

**7. What is a class in Java?**

- A class is a blueprint, it defines what an object looks like and what it can do
- No memory is used until you actually create an object from it

```java
class Car {
    String brand;
    int speed;

    void accelerate() {
        speed += 10;
    }
}
```

---

**8. What is an object in Java?**

- An object is a live instance of a class
- It lives on the heap and has its own copy of the class's fields

```java
Car myCar = new Car();
myCar.brand = "Tesla";
myCar.accelerate();
```

---

**9. What is inheritance in Java?**

- A child class can inherit fields and methods from a parent class
- You use the `extends` keyword
- It avoids copy-pasting code and models "is-a" relationships naturally

```java
class Vehicle {
    int speed;
}

class Car extends Vehicle {
    String brand;
}
// Car gets speed for free from Vehicle
```

---

**10. What is polymorphism in Java?**

- One reference type, many possible behaviors
- At runtime, Java calls the right method based on the actual object
- Compile-time version = method overloading
- Runtime version = method overriding

```java
Animal a = new Dog();
a.

speak(); // calls Dog's speak(), not Animal's
```

---

**11. What is encapsulation in Java?**

- Hide your internal data and only expose what you need to
- Use `private` fields, then control access with getters and setters
- Protects your object from being put in a bad state

```java
class BankAccount {
    private double balance;

    public double getBalance() {
        return balance;
    }

    public void deposit(double amt) {
        balance += amt;
    }
}
```

---

## Core Concepts

**12. What is the difference between == and equals() in Java?**

- `==` checks if two variables point to the **same object** in memory
- `equals()` checks if two objects have the **same content**
- For strings, almost always use `equals()`

```java
String a = new String("hi");
String b = new String("hi");
a ==b       // false, two different objects
a.equals(b)  // true , same characters
```

---

**13. What is the static keyword in Java?**

- `static` means it belongs to the **class**, not to any specific object
- A static field is shared by all instances
- A static method can be called without creating an object

```java
class MathUtils {
    static int square(int n) {
        return n * n;
    }
}
MathUtils.square(5); // no object needed
```

---

**14. What is a constructor and how is it different from a method?**

- A constructor runs automatically when you create an object with `new`
- It has no return type, not even `void`
- A method is called manually and does work on an existing object

```java
class Point {
    int x, y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    } // constructor

    double distance() {
        return Math.sqrt(x * x + y * y);
    } // method
}
```

---

**15. What is method overloading in Java?**

- Same method name, different parameter list
- The compiler picks the right one at compile time
- Useful when you want the same operation to handle different input types

```java
int add(int a, int b) {
    return a + b;
}

double add(double a, double b) {
    return a + b;
}
```

---

**16. What is method overriding in Java?**

- A subclass rewrites a method from its parent with the same signature
- Java calls the subclass version at runtime
- Always use `@Override`, the compiler will catch typos

```java
class Shape {
    double area() {
        return 0;
    }
}

class Circle extends Shape {
    double r;

    @Override
    double area() {
        return Math.PI * r * r;
    }
}
```

---

**17. What is the difference between final, finally and finalize?**

- `final`, locks something down (variable can't change, method can't be overridden, class can't be extended)
- `finally`, the block that always runs after a try/catch, great for cleanup
- `finalize()`, old GC hook on Object, deprecated and unreliable, don't use it

```java
final int MAX = 100;
try {
    riskyOp();
} finally{
    connection.close();
}
```

---

## Abstraction

**18. What is an abstract class in Java?**

- A class you can't instantiate directly
- It can have both abstract methods (no body) and normal methods
- Use it when subclasses share some logic but must implement their own version of certain methods

```java
abstract class Shape {
    abstract double area();                          // subclass must implement

    void print() {
        System.out.println(area());
    }    // shared logic
}
```

---

**19. What is an interface and how is it different from an abstract class?**

- An interface is a pure contract, it just says "implement these methods"
- A class can implement multiple interfaces but extend only one class
- Since Java 8, interfaces can also have `default` and `static` methods

```java
interface Drawable {
    void draw();
}

interface Resizable {
    void resize(double factor);
}

class Icon implements Drawable, Resizable { 
    ...
}
```

---

## Exceptions

**20. What is the difference between checked and unchecked exceptions?**

- **Checked**, the compiler forces you to handle or declare them (e.g. `IOException`)
- **Unchecked**, these are bugs, not expected failures (e.g. `NullPointerException`)
- Checked = things that can go wrong in the real world. Unchecked = programmer mistakes

```java
// Checked, must be handled
void read() throws IOException { ... }

// Unchecked, compiler won't warn you
int[] a = {};
a[0]; // ArrayIndexOutOfBoundsException at runtime
```

---

## Concurrency

**21. What is multithreading and how is it implemented?**

- Running multiple tasks at the same time within the same program
- All threads share the same heap but have their own stack
- Best practice: don't manage threads manually, use an `ExecutorService`

```java
ExecutorService pool = Executors.newFixedThreadPool(4);
pool.submit(() ->System.out.println("running in a thread"));
pool.shutdown();
```

---

**22. What is the purpose of the volatile keyword?**

- Without it, a thread might read a stale cached value of a variable
- `volatile` forces reads/writes to go straight to main memory
- But it doesn't make compound operations (like `count++`) atomic, use `AtomicInteger` for that

```java
private volatile boolean running = true;
// all threads will see the latest value
```

---

**23. What is a Thread and how is it different from a Process?**

- A **process** is an isolated program with its own memory
- A **thread** lives inside a process and shares the heap with other threads
- Threads are lighter and faster to create than processes

```java
Thread t = new Thread(() -> System.out.println("hello"));
t.start();
```

---

**24. What is the difference between synchronized, Lock, and volatile?**

- `synchronized`, simplest way to prevent two threads entering the same block
- `Lock` (ReentrantLock), more flexible: supports timeouts, try-lock, interruptible waits
- `volatile`, only guarantees visibility, not mutual exclusion

```java
Lock lock = new ReentrantLock();
lock.lock();
try{
    /* only one thread here at a time */ 
} finally{
    lock.unlock();
}
```

---

**25. What is a deadlock in Java?**

- Thread A holds lock 1, waits for lock 2
- Thread B holds lock 2, waits for lock 1
- Both wait forever, that's a deadlock
- Fix: always acquire locks in the same order, or use `tryLock()` with a timeout

```java
// Danger, if two threads run these in opposite order
synchronized(lockA){synchronized(lockB){...}}
synchronized(lockB){synchronized(lockA){...}}
```

---

**26. What is the difference between wait() and sleep()?**

- `sleep()` just pauses the thread, it keeps all its locks
- `wait()` releases the lock and suspends until someone calls `notify()`
- `wait()` must be inside a `synchronized` block

```java
synchronized(lock) {
    lock.wait();
}  // releases the lock
Thread.sleep(1000); // holds the lock, just pauses
```

---

**27. What is the difference between Callable and Runnable?**

- `Runnable`, no return value, can't throw checked exceptions
- `Callable`, returns a result via `Future`, can throw exceptions
- Use `Callable` whenever you need to get something back from a task

```java
Future<Integer> f = executor.submit(() -> 42);
int result = f.get(); // waits for the result
```

---

**28. What is the Executor Framework?**

- A cleaner way to run tasks without manually managing threads
- You submit tasks, the framework handles the thread pool
- Gives you `Future` objects to track results

```java
ExecutorService pool = Executors.newFixedThreadPool(4);
Future<String> f = pool.submit(() -> "done");
System.out.println(f.get());
pool.shutdown();
```

---

**29. What is the difference between synchronized methods and synchronized blocks?**

- A synchronized **method** locks the whole object for the duration of the call
- A synchronized **block** lets you lock only a specific resource for a smaller window
- Blocks give you finer control and reduce contention

```java
synchronized void fullLock() { ...}

void partialLock() {
    doUnsafeWork();
    synchronized (this.cache) {
        updateCache();
    } // only this part is locked
}
```

---

## Collections

**30. What is the difference between ArrayList and LinkedList?**

- `ArrayList`, backed by an array. Fast random access, slow inserts in the middle
- `LinkedList`, backed by nodes. Fast inserts/deletes at the ends, slow random access
- Honestly, use `ArrayList` by default, it's faster for most real-world use cases

```java
List<String> arr = new ArrayList<>();  // your default choice
List<String> lnk = new LinkedList<>(); // only if you need queue-like behavior
```

---

**31. What is the difference between Array and ArrayList?**

- Arrays are fixed size, you set the length once and that's it
- Arrays can hold primitives (`int[]`), ArrayList can't
- `ArrayList` grows automatically and has helper methods like `add()`, `remove()`

```java
int[] arr = new int[5];                 // fixed, primitives OK
List<Integer> list = new ArrayList<>(); // flexible, objects only
```

---

**32. What is the Java Collections Framework?**

- A set of ready-made data structures you can use out of the box
- Covers lists, sets, maps, queues, all with consistent interfaces
- You rarely need to build your own data structure in Java because of this

```java
List<String> list = new ArrayList<>();
Set<String> set = new HashSet<>();
Map<String, Integer> map = new TreeMap<>();
```

---

**33. What is the difference between HashMap and Hashtable?**

- `HashMap` is faster, not thread-safe, and allows one `null` key
- `Hashtable` is synchronized and doesn't allow `null` keys at all
- In modern code, use `ConcurrentHashMap` if you need thread safety

```java
Map<String, Integer> map = new HashMap<>();            // fast, not thread-safe
Map<String, Integer> safe = new ConcurrentHashMap<>();  // thread-safe modern choice
```

---

**34. What is the difference between HashSet and TreeSet?**

- `HashSet`, no guaranteed order, but O(1) lookups
- `TreeSet`, always sorted, but O(log n) operations
- Use `TreeSet` when you need the elements in order, otherwise `HashSet` is faster

```java
Set<Integer> h = new HashSet<>(); // fast, unordered
Set<Integer> t = new TreeSet<>(); // sorted, slightly slower
```

---

**35. What is the difference between Comparator and Comparable?**

- `Comparable`, the object defines its own natural sort order (`compareTo`)
- `Comparator`, an external object defines a custom sort order
- Use `Comparator` when you want multiple ways to sort or can't touch the class

```java
// Comparable, sort by GPA inside the class
class Student implements Comparable<Student> {
    public int compareTo(Student o) {
        return this.gpa - o.gpa;
    }
}
// Comparator, sort by name from outside
list.sort(Comparator.comparing(Student::getName));
```

---

## Strings

**36. What is the difference between String, StringBuilder, and StringBuffer?**

- `String`, immutable, every change creates a new object
- `StringBuilder`, mutable and fast, not thread-safe
- `StringBuffer`, mutable and thread-safe, but slower
- In a loop building a string? Always use `StringBuilder`

```java
StringBuilder sb = new StringBuilder();
sb.append("Hello").append(" World");
String result = sb.toString();
```

---

## Design Patterns

**37. What is the singleton design pattern?**

- Ensures only one instance of a class ever exists
- Useful for things like config managers or connection pools
- The tricky part is making it thread-safe, use `volatile` + double-checked locking

```java
class Singleton {
    private static volatile Singleton instance;

    private Singleton() {
    }

    public static Singleton get() {
        if (instance == null)
            synchronized (Singleton.class) {
                if (instance == null) instance = new Singleton();
            }
        return instance;
    }
}
```

---

## Advanced Java

**38. What is reflection in Java?**

- Lets you inspect and call classes, methods, and fields at runtime
- Used heavily in frameworks (Spring, Hibernate) under the hood
- It's powerful but slow and breaks encapsulation, don't abuse it

```java
Class<?> c = Class.forName("java.util.ArrayList");
Method m = c.getMethod("size");
Object result = m.invoke(new ArrayList<>());
```

---

**39. What is the Java Stream API and why is it useful?**

- A cleaner way to work with collections, no more verbose for-loops
- You chain operations: filter, map, reduce, collect
- Can switch to parallel processing with one word: `parallelStream()`

```java
List<Integer> evens = numbers.stream()
        .filter(n -> n % 2 == 0)
        .collect(Collectors.toList());
```

---

**40. What is the Fork/Join Framework?**

- Built for divide-and-conquer problems
- You split a big task into smaller ones (fork), run them in parallel, then combine the results (join)
- Uses work-stealing under the hood so idle threads pick up tasks from busy ones

```java
class SumTask extends RecursiveTask<Long> {
    protected Long compute() {
        if (size <= THRESHOLD) return sequentialSum();
        SumTask left = new SumTask(...);
        left.fork();
        return new SumTask(...).compute() + left.join();
    }
}
```

---

**41. What is the difference between deep copy and shallow copy?**

- **Shallow copy**, copies the object but nested objects are still shared
- **Deep copy**, copies everything, all the way down
- If you change a nested object in a shallow copy, the original is affected too

```java
// Shallow, fast but shares references
Object clone = original.clone();

// Deep, via serialization (truly independent copy)
ObjectOutputStream oos = new ObjectOutputStream(bos);
oos.writeObject(original);
```

---

**42. What are Java Annotations and how are they used?**

- Metadata you attach to classes, methods, or fields with `@`
- Some are processed at compile time (`@Override`, `@SuppressWarnings`)
- Others are read at runtime by frameworks via reflection (`@Entity`, `@GetMapping`)

```java
@interface Retry {
    int times() default 3;
}

@Retry(times = 5)
void callExternalService() { ...}
```

---

**43. What are Generics in Java?**

- Let you write classes and methods that work with any type, safely
- The compiler catches type mismatches, no more random `ClassCastException` at runtime
- The type info is erased at runtime (type erasure), but that's a JVM detail you rarely care about

```java
class Box<T> {
    private T value;
}

Box<String> box = new Box<>(); // compiler enforces String only
```

---

**44. What is the Optional class and why is it useful?**

- A wrapper that forces you to deal with the possibility of a missing value
- Instead of returning `null` and hoping the caller checks, you return `Optional`
- Eliminates a whole category of `NullPointerException` bugs

```java
Optional<String> name = findUser(id).map(User::getName);
name.ifPresentOrElse(n  ->System.out.println("Hello "+n), ()->System.out.println("User not found"));
```
