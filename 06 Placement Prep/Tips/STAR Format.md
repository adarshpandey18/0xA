# :LiStars: STAR
The **STAR** format helps you to organize your answers to behavioral questions. This is most applicable to questions that require you to *recount past experiences* or *behavior*.

- ##  **Situation**: 
	Share details about the situation that gave rise to the task
	
- ## **Task**: 
	Explain what you needed to achieve or the problems you had to solve; focus on the
    - #### Scope
    - #### Severity
    - #### Specific benchmarks/outcomes required
    
- ## **Action**: 
	Explain what you did to meet your objectives, describing options you had and how you made decisions
	
- ## **Results**: 
	Describe the outcome of your actions and what you learnt

---
## **SWE Example (STAR Format)**

### **Question**:

_"Tell me about a time you had to deal with a significant bug in a production system. What did you do?"_

### **S – Situation**
During my internship at a fin-tech startup, I was part of a backend team responsible for processing user transactions. One day, we received multiple customer complaints that transfers were failing intermittently.

### **T – Task**
My task was to investigate and resolve the issue quickly to avoid financial loss and restore customer trust. The issue was critical—affecting 10% of daily transactions, which translated to thousands of dollars stuck in limbo.

### **A – Action**
I started by analyzing the logs and traced the problem to a race condition in our transaction queue handler, caused by a recent update that hadn’t been thoroughly tested for concurrency. I proposed a fix using mutex locks to prevent overlapping processes. I wrote test cases to reproduce the issue and verify the fix locally. Then, I rolled it out to staging for further QA before deploying it to production under supervision.

### **R – Result**
The fix resolved the issue—transaction failure rates dropped to 0%. I also helped implement a regression test for concurrent transaction processing to avoid similar bugs in the future. From this, I learned the importance of concurrency testing and having safeguards in CI/CD pipelines.

---

##  **General Example (STAR Format)**

### **Question**:

_"Describe a time when you had to work with a difficult team member."_


### **S – Situation**

In a university group project, one member was often unresponsive and submitted low-quality work close to deadlines.

### **T – Task**
As the team lead, I needed to ensure that all members contributed equally and we delivered a functional web app for our final grade.

### **A – Action**
I scheduled a one-on-one with the team member to understand their challenges. It turned out they were overwhelmed with multiple deadlines. I helped them re-prioritize their tasks and reassigned them a smaller but still meaningful feature. I also introduced weekly check-ins to monitor progress.

### **R – Result**
The team member’s participation improved significantly, and we completed the project on time with an A grade. I learned that empathy and proactive communication are key to resolving team conflicts.

---