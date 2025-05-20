**Functional Dependency (FD):**  
A functional dependency is a constraint between two sets of attributes in a relation. It is denoted as:  
**X → Y**, which means:

- X determines Y
- Y is functionally dependent on X
- X is the **determinant**, and Y is the **dependent** attribute(s)

### Properties of Functional Dependencies:

1. **Reflexivity**  
    If Y is a subset of X, then:  
    **X → Y**
    
2. **Augmentation**  
    If **X → Y**, then:  
    **XZ → YZ**  
    (Adding the same attributes to both sides preserves the dependency)
    
3. **Transitivity**  
    If **X → Y** and **Y → Z**, then:  
    **X → Z**
    
4. **Union**  
    If **X → Y** and **X → Z**, then:  
    **X → YZ**
    
5. **Decomposition**  
    If **X → YZ**, then:  
    **X → Y** and **X → Z**
    
6. **Pseudotransitivity**  
    If **X → Y** and **WY → Z**, then:  
    **WX → Z**
    
7. **Composition**  
    If **X → Y** and **Z → W**, then:  
    **XZ → YW**

---

