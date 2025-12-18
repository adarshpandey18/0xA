# Mockito

## Introduction

**Mockito** is a popular Java testing framework used for creating mock objects.  
It helps isolate the code under test by replacing real dependencies with simulated ones.

- **Why use Mockito?**
    
    - To avoid using real services (like databases, APIs, etc.) during unit testing.
        
    - To make unit tests **faster**, **independent**, and **easier to maintain**.
        
    - To test behavior in multiple scenarios without writing numerous stub classes.
        

---

## Basic Example Without Mockito

```java
package com.demo.mockitotutorial.business;  
  
public class Business {  
    public int calculateSum(int[] data) {  
        int sum = 0;  
        for (int value : data) {  
            sum += value;  
        }  
        return sum;  
    }  
}
```

### Test Class

```java
package com.demo.mockitotutorial.business;  
  
import org.junit.jupiter.api.Test;  
import static org.junit.jupiter.api.Assertions.assertEquals;  
  
public class BusinessTest {  
    @Test  
    public void calculateSum_basic() {  
        Business business = new Business();  
        int actualResult = business.calculateSum(new int[]{1,2,3});  
        int expectedResult = 6;  
        assertEquals(expectedResult, actualResult);  
    }  
  
    @Test  
    public void calculateSum_empty() {  
        Business business = new Business();  
        int actualResult = business.calculateSum(new int[]{});  
        int expectedResult = 0;  
        assertEquals(expectedResult, actualResult);  
    }  
  
    @Test  
    public void calculateSum_singleValue() {  
        Business business = new Business();  
        int actualResult = business.calculateSum(new int[]{3});  
        int expectedResult = 3;  
        assertEquals(expectedResult, actualResult);  
    }  
}
```

- Here, we **hardcode the data values**.
    
- In real-world scenarios, data usually comes from external services (e.g., database, APIs).
    

---

## Introducing a Service Dependency

```java
package com.demo.mockitotutorial.business;  
  
import com.demo.mockitotutorial.Service.SomeService;  
  
public class SomeBusiness {  
    private SomeService someService;  
  
    public void setSomeService(SomeService someService) {  
        this.someService = someService;  
    }  
      
    public int calculateSum(int[] data) {  
        int sum = 0;  
        for (int value : data) {  
            sum += value;  
        }  
        return sum;  
    }  
  
    public int calculateSumService() {  
        int[] data = someService.retrieveData();  
        int sum = 0;  
        for (int value : data) {  
            sum += value;  
        }  
        return sum;  
    }  
}
```

### Service Interface

```java
package com.demo.mockitotutorial.Service;  
  
public interface SomeService {  
    int[] retrieveData();  
}
```

---

## Using Stubs (Old Way)

If we directly test `SomeBusiness.calculateSumService()`, it throws **NullPointerException**, because no service is injected.

We create **stub classes** to simulate service behavior.

```java
class SomeServiceStubBasic implements SomeService {  
    @Override  
    public int[] retrieveData() {  
        return new int[]{1,2,3};  
    }  
}  
  
public class SomeBusinessStubTest {  
    @Test  
    public void testSomeBusiness_basic() {  
        SomeBusiness someBusiness = new SomeBusiness();  
        someBusiness.setSomeService(new SomeServiceStubBasic());  
        int actual = someBusiness.calculateSumService();  
        int expected = 6;  
        assertEquals(expected, actual);  
    }  
}
```

### Problem with Stubs

- For **every new scenario**, a new stub class is needed (empty array, single element, etc.).
    
- Not **feasible** and **not maintainable**.
    
- If the `SomeService` interface changes, **all stub classes must be updated**.
    

---

## Using Mockito

Mockito solves these problems by dynamically creating mock objects.

```java
import static org.mockito.Mockito.mock;  
import static org.mockito.Mockito.when;  

public class SomeBusinessMockTest {  
    SomeService someServiceMock = mock(SomeService.class);  
    SomeBusiness someBusiness = new SomeBusiness();  
  
    @BeforeEach  
    void setUp() {  
        someBusiness.setSomeService(someServiceMock);  
    }  
  
    @Test  
    public void testSomeBusiness_basic() {  
        when(someServiceMock.retrieveData()).thenReturn(new int[]{1,2,3});  
        int actual = someBusiness.calculateSumService();  
        assertEquals(6, actual);  
    }  
}
```

---

## Mockito Annotations

Instead of `mock()` manually, we can use annotations:

```java
@ExtendWith(MockitoExtension.class)  
public class SomeBusinessMockTest {  

    @Mock  
    SomeService someServiceMock;  

    @InjectMocks  
    SomeBusiness someBusiness;  

    @Test  
    public void testSomeBusiness_basic() {  
        when(someServiceMock.retrieveData()).thenReturn(new int[]{1,2,3});  
        assertEquals(6, someBusiness.calculateSumService());  
    }  
}
```

### Common Annotations

- `@Mock` → Creates a mock object.
    
- `@InjectMocks` → Injects mocks into the class under test.
    
- `@ExtendWith(MockitoExtension.class)` → Enables Mockito in JUnit 5.
    
- `@RunWith(MockitoJUnitRunner.class)` → Used for JUnit 4.
    

---

## Returning Multiple Values

```java
when(mock.size()).thenReturn(5).thenReturn(10);  
```

- First call to `size()` → returns `5`.
    
- Second call → returns `10`.
    

---

## Return with Generic Parameters

```java
@Test  
public void testReturnWithAnyParameters() {  
    List mock = mock(List.class);  
    when(mock.get(anyInt())).thenReturn("Pass");  
    assertEquals("Pass", mock.get(1));  
    assertEquals("Pass", mock.get(2));  
}
```

- Works with `anyInt()`, `anyBoolean()`, etc.
    

---

## Verification

We can verify method calls instead of return values.

```java
verify(mock).add("Something");  
```

Useful when we want to check whether a method was called with correct arguments.

---

## Argument Capturing

```java
@Test  
public void testArgumentCaptor() {  
    List mock = mock(List.class);  
    mock.add("Something");  
  
    ArgumentCaptor<String> captor = ArgumentCaptor.forClass(String.class);  
    verify(mock).add(captor.capture());  
    assertEquals("Something", captor.getValue());  
}
```

### Multiple Arguments

```java
verify(mock, times(2)).add(captor.capture());  
List<String> captured = captor.getAllValues();  
assertEquals("Something", captured.get(0));  
assertEquals("Something2", captured.get(1));  
```

---

## Spying

Unlike mocks, **spies retain original behavior** unless explicitly stubbed.

```java
@Test  
public void spying() {  
    ArrayList mock = spy(new ArrayList<>());  
    System.out.println(mock.size()); // 0  
    mock.add("something");  
    mock.add("something2");  
    System.out.println(mock.get(0)); // something  
    when(mock.size()).thenReturn(5);  
    System.out.println(mock.size());  // 5  
}
```

---

## MockMvc for Testing Controllers

```java
@WebMvcTest(HelloWorldController.class)  
public class HelloWorldControllerTest {  

    @Autowired  
    private MockMvc mockMvc;  

    @Test  
    public void helloWorld_basic() throws Exception {  
        RequestBuilder requestBuilder = MockMvcRequestBuilders  
                .get("/greet")  
                .accept(MediaType.APPLICATION_JSON);  
  
        MvcResult mvcResult = mockMvc.perform(requestBuilder).andReturn();  
        String responseBody = mvcResult.getResponse().getContentAsString();  
  
        assertEquals("Hello World", responseBody);  
    }  
}
```

### With Response Matchers

```java
mockMvc.perform(requestBuilder)  
       .andExpect(status().isOk())  
       .andExpect(content().string("Hello World!"));  
```

- `status().isOk()` → checks HTTP status code = 200.
    
- `content().string("...")` → checks response body.

---
## @SpringBootTest

- `@SpringBootTest` loads the full Spring context for integration tests.
    
- Useful when we want to test the **whole application flow**, not just isolated components.
    

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class HelloWorldIntegrationTest {  

    @Autowired  
    private TestRestTemplate restTemplate;  

    @Test  
    public void helloWorld_integrationTest() {  
        String response = this.restTemplate.getForObject("/greet", String.class);  
        assertEquals("Hello World", response);  
    }  
}
```

### Notes

- `webEnvironment` can be:
    
    - `MOCK` → default, uses a mock servlet environment.
        
    - `RANDOM_PORT` → starts server on a random port.
        
    - `DEFINED_PORT` → uses configured port.
        
    - `NONE` → no web environment.
        
- `TestRestTemplate` is used for making HTTP calls in tests.
    

---

## @DataJpaTest

- `@DataJpaTest` is a slice annotation that tests only **JPA components** (repositories).
    
- Loads **in-memory database** (like H2) by default.
    

```java
@DataJpaTest  
public class UserRepositoryTest {  

    @Autowired  
    private UserRepository userRepository;  

    @Test  
    public void testFindByUsername() {  
        User user = new User("adarsh", "password");  
        userRepository.save(user);  

        User found = userRepository.findByUsername("adarsh");  
        assertThat(found.getUsername()).isEqualTo("adarsh");  
    }  
}
```

---

## AssertJ (Fluent Assertions)

AssertJ provides a **fluent API** for writing more readable assertions.

```java
import static org.assertj.core.api.Assertions.assertThat;

@Test
public void testAssertJ() {
    String name = "Mockito";
    assertThat(name)
        .isNotNull()
        .startsWith("Mock")
        .endsWith("ito")
        .hasSize(7);
}
```

---

## Hamcrest Matchers

Hamcrest is another assertion library that makes test conditions more **expressive**.

```java
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.Matchers.*;

@Test
public void testHamcrest() {
    String str = "Mockito";
    assertThat(str, allOf(startsWith("Mock"), endsWith("ito")));
    assertThat(str, is("Mockito"));
    assertThat(7, greaterThan(5));
}
```

---

## JSONPath Testing

Spring provides `jsonPath` to validate JSON responses in **MockMvc tests**.

```java
mockMvc.perform(get("/users/1"))
       .andExpect(status().isOk())
       .andExpect(jsonPath("$.id").value(1))
       .andExpect(jsonPath("$.name").value("Adarsh"));
```

- `$.id` → access `id` field in JSON response.
    
- `$.name` → access `name` field.
    

---

#Testing 