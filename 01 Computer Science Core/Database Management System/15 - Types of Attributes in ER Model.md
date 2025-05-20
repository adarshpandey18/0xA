### **1. Single-Valued & Multi-Valued Attributes**

- **Single-Valued Attribute**  
    An attribute that holds **only one value** for each entity instance.  
    **Example**: `StudentRegNo`, `AadharNumber`
    
- **Multi-Valued Attribute**  
    An attribute that can hold **multiple values** for a single entity.  
    **Example**: `mobileNo`, `emailAddresses`  
    **Notation**: Represented using a **double oval** in ER diagrams.
	![[multi-valued-attribute-annotation.png|center|200]]
    

---

### **2. Simple & Composite Attributes**

- **Simple Attribute**  
    Cannot be divided further into sub-parts.  
    **Example**: `age`, `gender`
    
- **Composite Attribute**  
    Can be **divided into smaller sub-attributes**.  
    **Example**: `name` → `firstName`, `middleName`, `lastName`  
    **Notation**: Main attribute is connected to sub-attributes with lines.
	![[composite-attributes-annotation.png|center|350]]
    

---

### **3. Stored & Derived Attributes**

- **Stored Attribute**  
    The attribute **directly stored** in the database.  
    **Example**: `dateOfBirth` (DOB)
    
- **Derived Attribute**  
    The attribute that is **calculated from stored attributes**.  
    **Example**: `age` (derived from DOB and current date)  
    **Notation**: Represented using a **dashed (dotted) oval**.
	![[derived-attribute-annotation.png|center|200]]
    
    

---

### **4. Key & Non-Key Attributes** _(Important)_

- **Key Attribute**  
    Uniquely identifies each entity instance.  
    **Example**: `rollNo`, `empID`
    
- **Non-Key Attribute**  
    Does **not uniquely identify** an entity.  
    **Example**: `name`, `address`
    

> Key attributes are used to enforce uniqueness in entities.

---

### **5. Required & Optional Attributes**

- **Required Attribute**  
    Must have a **non-null value**; cannot be left empty.  
    **Example**: `email` in user login
    
- **Optional Attribute**  
    **May be left null** or empty.  
    **Example**: `middleName`, `alternateContactNumber`
    

---

### **Summary Table**

|Type|Description|Example|ER Notation|
|---|---|---|---|
|Single-Valued|One value per entity|StudentRegNo|Single oval|
|Multi-Valued|Multiple values per entity|mobileNo|**Double oval**|
|Simple|Cannot be subdivided|age|Oval|
|Composite|Can be subdivided|name → firstName, etc.|Oval with sub-ovals|
|Stored|Directly stored|dob|Oval|
|Derived|Calculated from other attributes|age|**Dashed oval**|
|Key Attribute|Uniquely identifies entity|rollNo|Underlined oval|
|Non-Key Attribute|Does not uniquely identify|address|Oval|
|Required Attribute|Cannot be null|email|Not specially shown|
|Optional Attribute|Can be null|alternatePhone|Not specially shown|

---
