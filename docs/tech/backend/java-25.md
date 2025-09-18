Java 25 is a Long-Term Support (LTS) release and has been made generally available on 16 September 2025.

Here are some features

## Flexible Constructor Bodies

Allows code before the super(...) or this(...) call in constructors.

Enables validation or computations before delegation to the superclass constructor.

#### Before

```java
public class Elephant extends Animal {

    public Elephant(String name) {
        super(validate(name));
    }

    private static String validate(String name) {
        if (name == null) {
            throw new IllegalArgumentException();
        }
        return name;
    }
}
```

#### After

```java
public class Elephant extends Animal {

    public Elephant(String name) {
        if (name == null) {
            throw new IllegalArgumentException();
        }
        super(name);
    }
}
```

## Primitive Types in Patterns

Pattern matching can handle primitive types in switch and instanceof statements.

### `instanceof`

#### Before

```java
Object o = 42;

if (o instanceof Integer i) {   // autoboxed to Integer
    System.out.println("Integer with value: " + i);
} else {
    System.out.println("Not an Integer");
}
```

You could not write if (o instanceof int i).

The only option was to rely on wrapper classes (Integer, Double, etc.), because instanceof only worked with reference types.

#### After

Now, `instanceof` supports primitive patterns:

```java
Object o = 42;
if (o instanceof int i) {   // primitive pattern
    System.out.println("Primitive int with value: " + i);
} else {
    System.out.println("Not an int");
}
```

### `switch`

#### Before

If you had a primitive like `int x = 42;`, and passed it as Object o = x;, then autoboxing turned it into an Integer, and the pattern case Integer i matched.

You could not directly write case int i or use primitive patterns in switch.

```java
public String test(Object obj) {
    return switch (obj) {
        case String s -> "String: " + s;
        case Integer i -> "Integer: " + i;
        default -> "Other: " + obj;
    };
}
```

#### After

You can now use patterns like `int`, `long`, `double`, etc. directly

```java
public String test(Object obj) {
    return switch (obj) {
        case int i    -> "int: " + i;
        case long l   -> "long: " + l;
        case double d -> "double: " + d;
        default       -> "Other: " + obj;
    };
}
```

## Compact Source Files and Instance Main Methods

### Before

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

### After

```java
void main() {
    System.out.println("Hello, world!");
}
```

No need for public class, public static void main, etc. → easier for small programs, teaching, scripting.

## Module import

### Before

```java
import java.util.List;
import java.util.Map;
import java.util.HashMap;

public class Example {
    public static void main(String[] args) {
        List<String> list = List.of("a", "b");
        Map<String, Integer> map = new HashMap<>();
    }
}

```

### After

```java
import module java.util;

void main() {
    var list = List.of("a", "b");
    var map  = new HashMap<String, Integer>();
}
```

Instead of importing every class or package, you can pull in the whole module (java.util in this case).

Cleaner for quick apps and educational snippets.

## Scoped Values

Scoped values are a lightweight and safe alternative to thread-locals.

### Before

```java
static final ThreadLocal<String> USER = new ThreadLocal<>();

public static void main(String[] args) {
    USER.set("John");
    doWork();
    USER.remove();
}

static void doWork() {
    System.out.println("Working as " + USER.get());
}
```

Issues: manual set/remove, risk of memory leaks, not structured.

### After

```java
import java.lang.ScopedValue;

public class Example {
    static final ScopedValue<String> USER = ScopedValue.newInstance();

    public static void main(String[] args) {
        ScopedValue.where(USER, "Alice").run(() -> {
            doWork();
        });
    }

    static void doWork() {
        System.out.println("Working as " + USER.get());
    }
}
```

Benefits:

- No risk of accidental value leakage across threads.
- Automatically bound to the structured scope.
- Plays nicely with virtual threads.

## Other

- Compact Object Headers : the header size is reduced -> more efficient memory usage
- GC / Startup / Profiling : Previous versions required extra flags and tools for performance tuning and observability. Java 25 improves this with faster startup times
- Crypto Updates : modernized cryptography libraries
