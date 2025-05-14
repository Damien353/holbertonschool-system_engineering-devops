## Task 1

Infrastructure explanation
When a user types www.foobar.com in their browser, the DNS system resolves the domain name to the IP address of the load balancer. The HAProxy load balancer receives incoming traffic and distributes it to one of the two backend servers based on a round-robin algorithm.

Each backend server runs a web server (Nginx) that handles incoming HTTP requests and forwards them to the application server, which processes business logic using the application files. If the application needs to read or write data, it connects to the MySQL database.

In this setup, Server 1 contains the Primary database node, and Server 2 contains a Replica node. The Primary node handles all write operations (INSERT, UPDATE, DELETE), while the Replica node gets updates from the Primary via replication and can be used for read-only operations or failover.

## Whiteboard



## Explanation

- Why each element is added
Load Balancer (HAProxy): Distributes traffic across multiple servers, avoids overloading a single node.

Multiple Servers: Improves reliability, allows traffic distribution, and enables scaling.

Primary-Replica DB: Increases data availability and read performance, enables database failover.

- Load Balancer Mode & Algorithm
We use a round-robin distribution algorithm, which sends each new connection to the next available server in order. This ensures even traffic distribution across all servers.

This is an Active-Active setup, meaning both backend servers are serving requests simultaneously. In contrast, an Active-Passive setup has one active server and one standby server that only takes over if the first fails.

- Primary vs Replica Node (Database)
The Primary node can handle both reads and writes.

The Replica node can only handle reads, and it syncs changes from the Primary.
This allows the application to scale read traffic and have a fallback in case of failure.

## Issues with this setup
SPOF (Single Point of Failure):

The load balancer itself is a SPOF. If it fails, no traffic reaches the backend.

Security:

No HTTPS (data is not encrypted in transit)

No firewall (all ports may be exposed)

No Monitoring:

We cannot detect failures or performance issues in real time without tools like Prometheus, Grafana, etc.
