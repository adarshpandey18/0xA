![[clean-architecture-flow.png]]

## **3 Main Components of Clean Architecture**

### **3. Data Layer**
This layer works _behind the scenes_ and handles **data management**, including communication with external systems like APIs and databases.

- **Repositories**  
    Repositories act like _storehouses_ or _gatekeepers_ that fetch and manage data from different sources (e.g., remote APIs or local databases).  
    They serve the **Domain Layer** by providing the necessary data, but they don’t contain any business logic themselves.
    

---

### **2. Domain Layer**

This is the **core** of the application. It contains the **business logic** and rules, independent of any external technology or framework.

- **Use Cases**  
    Use cases define specific **actions or operations** that the application can perform (e.g., "log in user", "fetch product list").  
    They orchestrate how data flows between the **Entities** and the **Data Layer**.
    
- **Entities**  
    These are the core **business models** or **rules**—the "unchanging truths" of the system.  
    They are not concerned with how data is fetched or displayed.
	
> `Repositories` are present in both `Domain` & `Data` layer in `Domain` layer it contains the functions that are needed to be present in `Data` layer so it will going to be and `interface` 

---

### **1. Presentation Layer**

This is what the **user interacts with**—UI elements and interface logic.

- **Widgets/UI Components**  
    Represent the visible parts of the app like buttons, forms, lists, etc.
    
- **State Management**  
    Listens to user interactions and data changes. It works as the communication bridge between UI and the underlying layers, ensuring the app reacts appropriately to different events or states.
    

---

## Folder Structure
### Feature First Approach
it organizes functionality based on feature of app that organizes based on feature.
> If you decide to remove the feature from the app you can delete the folder and it wont cause many errors.

- Features
	- Authentication
		- presentation
			- pages
			- widgets
			- bloc / state maanger
		- domain
		- data
- core (contains all the resources that are shared among all the features)
	- theme
	- error
	- secrets
	- 