## 2 Tier Architecture

![[2-tier-architecture.png|center|400]]

In a 2-Tier or *Client-Server Architecture*, the client sends requests or **runs queries through the interface**, which are forwarded to the database system. The database processes the request and returns the result.  
### Advantages
- **Easy to maintain** due to a limited number of authorized clients and restricted data access.
### Disadvantages
- **Scalability:** Handling a large number of clients can be challenging.  
- **Security:** Since clients interact directly with the database, security risks are higher.

---
## 3 Tier Architecture

![[3-tier-architecture.png|center|400]]

In a 3-Tier Architecture, the **client interacts with the application layer and sends requests or queries to the business layer**, which processes them. 
This **enhances security** as clients do not interact directly with the database. 
The business layer then forwards the queries to the data layer, retrieves the results, processes them into the desired format, and returns them to the user.
