# Java Streams

## What is a Stream?

- A **Stream** is a pipeline of data through which elements of a collection (or array) can be processed.
    
- Streams allow performing operations such as **filtering, mapping, reducing, sorting, and collecting**.
    
- They enable **bulk processing** of data (functional-style programming).
    
- Streams can be executed in **sequential** or **parallel** mode.
    
- They are **not data structures**; instead, they represent a sequence of elements supporting operations.
    

---

## Stream Workflow

### Flow Diagram

```
Source → Intermediate Operations → Terminal Operation → Result
```

Example:

```
Collection → filter() → map() → sorted() → collect()
```

---

## Example

### Without Stream

```java
List<Integer> salaryList = Arrays.asList(3000, 4100, 9000, 3500);

int count = 0;
for (Integer salary : salaryList) {
    if (salary > 3000) {
        count++;
    }
}
System.out.println("Employees with salary > 3000: " + count);
```

### With Stream

```java
List<Integer> salaryList = Arrays.asList(3000, 4100, 9000, 3500);

long count = salaryList.stream()
                       .filter(salary -> salary > 3000)
                       .count();

System.out.println("Employees with salary > 3000: " + count);
```

---

## Ways to Create a Stream

1. **From Collection**
    

```java
List<Integer> list = Arrays.asList(100, 200, 300);
Stream<Integer> s1 = list.stream();
```

2. **From Array**
    

```java
Integer[] arr = {100, 200, 300};
Stream<Integer> s2 = Arrays.stream(arr);
```

3. **Using Stream.of()**
    

```java
Stream<Integer> s3 = Stream.of(100, 200, 300);
```

4. **Using Stream.builder()**
    

```java
Stream<Integer> s4 = Stream.<Integer>builder()
                           .add(100)
                           .add(200)
                           .add(300)
                           .build();
```

5. **Using Stream.iterate()**
    

```java
Stream<Integer> s5 = Stream.iterate(1000, n -> n + 5000)
                           .limit(5);
```

6. **Using Stream.generate()**
    

```java
Stream<Double> s6 = Stream.generate(Math::random)
                          .limit(5);
```

---

## Intermediate Operations

- **Definition**: Operations that transform one stream into another stream.
    
- They are **lazy** → executed only when a **terminal operation** is called.
    
- Multiple intermediate operations can be chained to form a **pipeline**.
    

### Common Intermediate Operations

1. **filter()** → Select elements based on condition.
    

```java
List<String> names = Stream.of("Hi", "All", "World")
                           .filter(s -> s.length() <= 2)
                           .toList(); // ["Hi"]
```

2. **map()** → Transform each element.
    

```java
List<String> lower = Stream.of("Java", "STREAM")
                           .map(String::toLowerCase)
                           .toList(); // ["java", "stream"]
```

3. **flatMap()** → Flatten nested structures.
    

```java
List<List<String>> list = Arrays.asList(
    Arrays.asList("I", "Love"),
    Arrays.asList("Java", "Streams")
);

List<String> words = list.stream()
                         .flatMap(Collection::stream)
                         .toList(); // ["I", "Love", "Java", "Streams"]
```

4. **distinct()** → Remove duplicates.
    

```java
List<Integer> nums = Arrays.asList(1, 2, 2, 3, 3, 4);
List<Integer> unique = nums.stream().distinct().toList();
// [1, 2, 3, 4]
```

5. **sorted()** → Sort elements.
    

```java
List<Integer> sorted = nums.stream().sorted().toList();
```

6. **peek()** → Debug values while processing.
    

```java
List<Integer> doubled = nums.stream()
                            .peek(System.out::println)
                            .map(n -> n * 2)
                            .toList();
```

7. **limit(n)** → Take first `n` elements.
    

```java
Stream<Integer> limited = Stream.of(1, 2, 3, 4, 5).limit(3);
```

8. **skip(n)** → Skip first `n` elements.
    

```java
Stream<Integer> skipped = Stream.of(1, 2, 3, 4, 5).skip(2);
```

9. **mapToInt / mapToLong / mapToDouble** → Convert objects into primitives.
    

```java
int sum = Stream.of(1, 2, 3).mapToInt(Integer::intValue).sum();
```

---

## Terminal Operations

- **Definition**: Operations that produce a result (collection, primitive value, or no value).
    
- A stream is **consumed** after a terminal operation → cannot be reused.
    

### Common Terminal Operations

1. **forEach()** → Iterate and perform an action.
    

```java
Stream.of(1, 2, 3).forEach(System.out::println);
```

2. **toArray()** → Collect elements into an array.
    

```java
Integer[] arr = Stream.of(1, 2, 3).toArray(Integer[]::new);
```

3. **reduce()** → Reduce elements to a single result.
    

```java
int sum = Stream.of(1, 2, 3, 4).reduce(0, Integer::sum);
```

4. **collect()** → Collect elements into a collection.
    

```java
List<Integer> even = Stream.of(1, 2, 3, 4, 5)
                           .filter(n -> n % 2 == 0)
                           .toList(); // [2, 4]
```

5. **min() / max()**
    

```java
Optional<Integer> minVal = Stream.of(3, 1, 4).min(Integer::compare);
```

6. **anyMatch / allMatch / noneMatch** → Check conditions.
    

```java
boolean allEven = Stream.of(2, 4, 6).allMatch(n -> n % 2 == 0);
```

7. **findFirst / findAny**
    

```java
Optional<Integer> first = Stream.of(1, 2, 3).findFirst();
```

---

## Laziness of Intermediate Ops

- Intermediate operations are **lazy**.
    
- Execution occurs **only when a terminal operation is invoked**.
    

Example:

```java
List<Integer> nums = Arrays.asList(2, 5, 10);

Stream<Integer> s = nums.stream()
                        .filter(n -> n > 3)
                        .peek(System.out::println);

System.out.println("No output yet!");

s.count(); // Triggers execution
```

Output:

```
No output yet!
5
10
```

---

## Parallel Streams

- Streams can be executed in **parallel** for faster processing on multi-core processors.
    
- Use `parallelStream()` or `stream().parallel()`.
    
- Internally uses **ForkJoinPool** and **Spliterator**.
    

Example:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
int sum = numbers.parallelStream()
                 .reduce(0, Integer::sum);
```

### When to use?

- Best for **large datasets**.
    
- Avoid for **small datasets** (overhead cost > benefit).
    
- Ensure **thread-safety** when using mutable shared state.
    

---

## Characteristics of Streams

- **Does not store data** → Works with existing collections/arrays.
    
- **Functional in nature** → Declarative (what to do, not how).
    
- **Lazy evaluation** → Intermediate ops are executed only when terminal ops are called.
    
- **Parallelizable** → Can be split for concurrent execution.
    

---

## Difference Between Collections and Streams

|Feature|Collections|Streams|
|---|---|---|
|Storage|Stores data|Does not store, processes data|
|Nature|Eager|Lazy|
|Reuse|Reusable|Consumed once|
|Traversal|External iteration|Internal iteration|
|Parallel Processing|Manual|Built-in|

---
