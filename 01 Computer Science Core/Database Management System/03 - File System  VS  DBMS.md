# File System VS DBMS

---
## File System
A file system is the method and data structure that an operating system uses to organize, store, retrieve, and manage data on a storage device like a hard drive, SSD, or USB drive.

## File System VS DBMS

![[Server-getting-accessed-by-mulitple-user.png|center|400]]

- ### Searching 
	- **File System:** For example, if there is 25 GB of data to search, it takes a long time.  
	- **DBMS:** A DBMS makes searching for data easier.  

- ### Attributes
	- **File System:** To find something, we need to know the exact location.
	- **DBMS:** We can use attributes to find data without knowing its exact storage location.

- ### Concurrency  
	- **File System:** If multiple users access a file, inconsistencies may arise due to various operations performed by different users.  
	-  **DBMS:** Multiple users can access the data simultaneously without any issues, ensuring consistency.  

- ### Security  
	-  **File System:** It does not provide access control.  
	- **DBMS:** It provides access control based on roles and predefined rules.  

 - ### Redundancy  
	-  **File System:** Duplicate data can be stored.  
	- **DBMS:** Constraints such as foreign keys and primary keys ensure data uniqueness.

---