# Stream


- We can consider stream as a pipeline, through which our collection element passes through
- While elements passes through pipelines, it perform various operations like sorting, filtering etc.
- Useful when deals with bulk processing(can do parallel processing)

![[streams-flow.png]]

### Example : 
#### Without using Stream : 
```java
package org.adarsh;  
  
import java.util.ArrayList;  
import java.util.List;  
  
public class Main {  
    public static void main(String[]args) {  
        List<Integer> salaryList = new ArrayList<>();  
        salaryList.add(3000);  
        salaryList.add(4100);  
        salaryList.add(9000);  
        salaryList.add(3500);  
  
        int count = 0;  
        for(Integer salary : salaryList) {  
            if(salary > 3000) {  
                count++;  
            }  
        }  
  
        System.out.println("Total employees with salary > 3000 : " + count);  
    }  
}
```

#### Using Stream : 
```java
package org.adarsh;  
  
import java.util.ArrayList;  
import java.util.List;  
  
public class Main {  
    public static void main(String[]args) {  
        List<Integer> salaryList = new ArrayList<>();  
        salaryList.add(3000);  
        salaryList.add(4100);  
        salaryList.add(9000);  
        salaryList.add(3500);  
  
        long count = salaryList.stream().filter(salary -> salary > 3000).count();  
  
        System.out.println("Total employees with salary > 3000 : " + count);  
    }  
}
```

## Different ways to create stream :

### 1. From Collection
```java
List<Integer> list = Arrays.asList(100,200,300,400);
Stream<Integer> streamFromIntegerList = list.stream();
```
### 2. From Array
```java
Integer[] array = {100,200,300,400,500};
Stream<Integer> streamFromIntegerArray = Arrays.stream(array);
```

### 3. From Static Method
```java
Stream<Integer> streamFromStaticMethod = Stream.of(100,200,300,400.500);
```

### 4. From Stream Builder
```java
Stream.Builder<Integer> streamBuilder = Stream.builder();
streamBuilder.add(100).add(200).add(300);
```

### 5. From Stream Iterate
```java
Stream<Integer> streamFromIterate = Stream.iterate(1000, (Integer, n) -> n + 5000).limit(5);
```

## Different Intermediate Operations
We can chain multiple intermediate operations together to perform more complex processing before applying terminal operation to produce the result.

### 1. filter(Predicate<T> predicate)
- Filter the element
- Example:

```java
Steam<String> nameStream = Stream.of("Hello", "Eeverybody", "How", "Are", "You", "Doing");
Stream<String> filteredStream = nameStream.filter((String name) -> name.length() <=3);
List<String> filteredNameList = filteredStream.collect(Collectors.toList());

```
### 2. map(Function<T, R> mapper)
- used to transform each element
```
Steam<String> nameStream = Stream.of("Hello", "Eeverybody", "How", "Are", "You", "Doing");
Stream<String> filteredStream = nameStream.filter((String name) -> name.toLowerCase());
```

### 3. flatMap(Function<T, Stream<R>> mapper) 
- used to iterate over 
```java
		List<List<String>> sentenceList = Arrays.asList(Arrays.asList("I", "Love", "Java"), Arrays.asList("Concept", "Are", "Clear"))



