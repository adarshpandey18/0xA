_Architectural blueprints for building adaptable, scalable, and maintainable software._

---
## **S — Single Responsibility Principle (SRP)**

> **A class should have only one reason to change.**

>  **Function ≠ Responsibility**  
> Multiple methods are fine **if they all serve the same responsibility**.

![[class-with-multiple-responsibility.png | center]]

### **Why do we need SRP?**

1. **Tight Coupling**  
    All functions share the same attributes. If one function alters shared state, it can unintentionally break others.
    
2. **Unnecessary Testing Overhead**  
    A small change in one function forces retesting of unrelated features.
    
3. **Poor Reusability**  
    You cannot reuse a class partially without pulling in unwanted behavior.
    
4. **Merge Conflicts**  
    Multiple developers modifying the same class leads to frequent conflicts.
      
5. **Harder Debugging**  
When something breaks, it’s unclear _which responsibility_ caused the issue.

### **Violation Example (SRP Broken)**

```java
public class User {
    private String name;
    private String email;
    private String password;
 
    public User(String name, String email, String password) {
        this.name = name;
        this.email = email;
        this.password = hashPassword(password);
    }
 
    private String hashPassword(String pass) {
        return Integer.toHexString(pass.hashCode());
    }
 
    public User saveToDatabase() {
        this.password = hashPassword(this.password);
        System.out.println("Saving user to database: " + this.name);
        return this;
    }
 
    public void sendWelcomeEmail() {
        System.out.println("Sending welcome email to: " + this.email);
    }
 
    public void log(String msg) {
        System.out.println("LOG: " + msg);
    }
}
```

**Problems:**

- Handles **data**, **security**, **database**, **email**, and **logging**
    
- Multiple reasons to change → violates SRP
    
### **SRP-Compliant Solution**

#### **User.java** (Data Only)

```java
public class User {
    private String name;
    private String email;
    private String password;
 
    public User(String name, String email, String password) {
        this.name = name;
        this.email = email;
        this.password = password;
    }
 
    public String getName() { return name; }
    public String getEmail() { return email; }
    public String getPassword() { return password; }
 
    public void setPassword(String hashedPassword) {
        this.password = hashedPassword;
    }
}
```

#### **UserRepository.java** (Persistence)

```java
public class UserRepository {
    public void save(User user) {
        System.out.println("Saving user to database: " + user.getName());
    }
}
```

#### **EmailService.java**

```java
public class EmailService {
    public void sendWelcomeEmail(String email) {
        System.out.println("Sending welcome email to: " + email);
    }
}
```

#### **LoggerService.java**

```java
public class LoggerService {
    public void log(String message) {
        System.out.println("LOG: " + message);
    }
}
```

#### **UserService.java** (Orchestration Layer)

```java
public class UserService {
    private UserRepository repository = new UserRepository();
    private EmailService emailService = new EmailService();
    private LoggerService logger = new LoggerService();
 
    public void registerUser(String name, String email, String password) {
        String hashed = Integer.toHexString(password.hashCode());
        User user = new User(name, email, hashed);
 
        repository.save(user);
        emailService.sendWelcomeEmail(user.getEmail());
        logger.log("New user registered: " + user.getName());
    }
}
```

### **Benefits of SRP**

- Easier to understand
    
- Easier to test
    
- Better readability
    
- High maintainability
    
- Cleaner Git history
    

---

## **O — Open/Closed Principle (OCP)**

> **Software entities should be open for extension but closed for modification.**

- **Open for Extension:** Add new behavior
    
- **Closed for Modification:** Don’t touch tested, working code

### **Why do we need OCP?**

1. Risk of breaking existing code
    
2. Tightly coupled conditional logic
    
3. Poor scalability
    
4. Merge conflicts when multiple devs add features
    

5. Encourages **polymorphism instead of conditionals**

### **Violation Example (OCP Broken)**

```java
public class Payment {
    public void pay(PaymentType paymentType){
        if(paymentType == PaymentType.PAYPAL){
            System.out.println("Paying through PayPal");
        } else if(paymentType == PaymentType.PAYTM){
            System.out.println("Paying through Paytm");
        } else if(paymentType == PaymentType.GOOGLEPAY){
            System.out.println("Paying through Google Pay");
        }
    }
}
```

 Every new payment → modify this class
 
### **OCP-Compliant Design**

#### **PaymentMethod.java**

```java
interface PaymentMethod {
    void pay();
}
```

#### **Concrete Implementations**

```java
class PaypalPayment implements PaymentMethod {
    public void pay() {
        System.out.println("Paying through PayPal");
    }
}
```

```java
class GooglePayPayment implements PaymentMethod {
    public void pay() {
        System.out.println("Paying through Google Pay");
    }
}
```

#### **Payment.java**

```java
public class Payment {
    private final PaymentMethod paymentMethod;
 
    public Payment(PaymentMethod paymentMethod) {
        this.paymentMethod = paymentMethod;
    }
 
    public void pay() {
        paymentMethod.pay();
    }
}
```

### **Benefits of OCP**

- Easy extensibility
    
- No side effects
    
- Cleaner code
    
- Uses abstraction & polymorphism
    

---

## **L — Liskov Substitution Principle (LSP)**

> **Subtypes must be substitutable for their base types without altering correctness.**

**Correctness means:**

- No unexpected behavior
    
- No broken assumptions
    
- No new exceptions
    

**In simple terms:**  
If a parent works somewhere, the child **must also work there without issues**.

![[liskov-substituion-principle-violation.e06e64c2.webp | center]]

![[liskov-substituion-principle.271e3233.webp | center]]

LSP is often violated when:

- Child removes functionality
    
- Child throws new exceptions
    
- Child changes expected behavior
    

### **Benefits of LSP**

- Predictable behavior
    
- Reliable inheritance
    
- Strong polymorphism
    
- Fewer runtime bugs
    

---

## **I — Interface Segregation Principle (ISP)**

> **Classes should not be forced to depend on methods they do not use.**

>  Fix: Split large interfaces into smaller, role-based interfaces


### **Violation Example**

```java
interface RestaurantWorker {
    void cook();
    void serve();
    void washDishes();
}
```

Each role is forced to implement unrelated methods → 

### **ISP-Compliant Design**

```java
interface ChefDuties {
    void cook();
}
```

```java
interface WaiterDuties {
    void serve();
}
```

```java
interface DishwasherDuties {
    void washDishes();
}
```

Each class implements **only what it needs**.

### **Benefits of ISP**

- Focused interfaces
    
- Cleaner implementations
    
- Better flexibility
    
- Reduced coupling
    

---

## **D — Dependency Inversion Principle (DIP)**

> **High-level modules should not depend on low-level modules.  
> Both should depend on abstractions.**


### **Violation Example**

```java
public class UserService {
    SQLRepository repository = new SQLRepository();
 
    public void get(String id) {
        repository.get(id);
    }
}
```

-  Tightly coupled to SQL  

-  Hard to switch databases

-  Hard to test

### **DIP-Compliant Design**

```java
public interface IRepository {
    void get(String id);
}
```

```java
public class SQLRepository implements IRepository {
    public void get(String id) {
        System.out.println("Fetched from SQL DB");
    }
}
```

```java
public class MongoRepository implements IRepository {
    public void get(String id) {
        System.out.println("Fetched from Mongo DB");
    }
}
```

```java
public class UserService {
    private IRepository repository;
 
    public UserService(IRepository repository) {
        this.repository = repository;
    }
 
    public void get(String id) {
        repository.get(id);
    }
}
```

---

### **Benefits of DIP**

- Loose coupling
    
- Easy testing (mock/fake repos)
    
- Flexible architecture
    
- Clean dependency graph
    

---

## **S.O.L.I.D Summary Table**

| Principle | Core Idea                              |
| --------- | -------------------------------------- |
| SRP       | One class = One responsibility         |
| OCP       | Extend behavior without modifying code |
| LSP       | Child must fully substitute parent     |
| ISP       | Don’t force unused methods             |
| DIP       | Depend on abstractions, not concretes  |

---