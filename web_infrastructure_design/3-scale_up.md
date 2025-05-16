## Task 3

- For Every Additional Element: Why You Are Adding It

1. Additional Server

**Description**:  
An extra server is added to separate application roles instead of using monolithic servers.

**Why It’s Added**:
- **Separation of Concerns**: Isolates each layer (web, app, db) to improve design clarity.
- **Security**: Minimizes the attack surface by limiting what each server is responsible for.
- **Scalability**: Enables independent scaling of specific services (e.g. more web servers without touching the database).
- **Maintainability**: Easier to debug, deploy, and manage when components are modular.

---

2. One Additional Load Balancer (HAProxy Cluster)

**Description**:  
HAProxy is configured in a clustered setup with two nodes (active-passive or active-active).

**Why It’s Added**:
- **High Availability (HA)**: If one load balancer fails, the second takes over to ensure continuity.
- **Redundancy**: Prevents a single point of failure at the network entry point.
- **Resilience**: Improves fault tolerance during network outages or updates.
- **Efficient Traffic Distribution**: Ensures consistent traffic routing under load.

---

3. Split of Components: Web Server, Application Server, Database

**Description**:  
The infrastructure now has distinct servers for the web layer, application layer, and database.

**Why It’s Added**:
- **Security**: Each layer has specific access rules (e.g., only the app server can query the database).
- **Performance Optimization**: Resources are better allocated (e.g., DB gets I/O power, web gets CPU).
- **Scalability**: Allows for horizontal scaling (e.g., more web servers without affecting app/db).
- **Professional Best Practice**: This mirrors real-world production-grade architecture design.
- **Simplified Troubleshooting**: Problems can be diagnosed at the component level.

---

### Summary Table

| Element                          | Why It’s Added                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| 1 Additional Server              | To split roles (web/app/db), improve scalability, security, and manageability  |
| 1 Extra HAProxy Load Balancer   | For high availability, redundancy, and fault tolerance                         |
| Split Web/App/DB Components     | For modular design, security, better performance, and ease of maintenance      |

## Whiteboard

![Schéma projet web infrastructure design task 3 drawio](https://github.com/user-attachments/assets/f5b805fe-7397-4076-8a57-fee45edf643e)
