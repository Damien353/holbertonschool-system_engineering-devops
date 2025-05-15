## Task 2

I designed a web infrastructure with three web servers protected by three firewalls, and a load balancer serving the website over HTTPS using an SSL certificate. Each web server has a monitoring client (such as SumoLogic) to collect metrics and logs. Monitoring is used to track system load, detect errors, and trigger alerts in case of issues. I’m aware of the limitations of this design, including SSL termination at the load balancer, reliance on a single MySQL server for writes, and the fact that all components run on the same servers, which impacts scalability and resilience.

## Whiteboard


## Explanation

- The 3 Firewalls

Firewall 1 (External):

Filters and protects incoming traffic from the internet. It blocks malicious IPs, unwanted protocols, and unauthorized access attempts.

Firewall 2 (Web Tier):

Sits between the load balancer and the web servers. Ensures only traffic coming from the load balancer reaches the web servers.

Firewall 3 (Database Tier):

Protects the database. Only traffic from authorized web servers should be allowed to connect to the database.

Why are firewalls used?

To reduce the attack surface and enforce network segmentation, minimizing the risk in case one part of the system is compromised.

- HTTPS and SSL Certificate

The website www.foobar.com must use HTTPS, which means all traffic between the user's browser and your infrastructure is encrypted.

An SSL/TLS certificate is installed on the load balancer to enable this encryption.

Why HTTPS?

Ensures data privacy and integrity.

Protects against man-in-the-middle (MITM) attacks.

Increases user trust, and is often required for compliance and SEO.

- Monitoring Clients (One per Web Server)

Each web server must have a monitoring agent installed.

What is monitoring used for?

To track the health of the servers and applications.

To detect issues such as downtime, high memory usage, or CPU spikes.

To create alerts when performance or availability degrades.

How does the monitoring tool collect data?

A lightweight agent runs on each web server.

It collects logs, metrics (CPU, memory, request rate), and system status.

The data is sent to a central monitoring platform (e.g., Sumologic, Datadog, Prometheus, etc.).

- How to Monitor QPS (Queries Per Second)

Add metrics collection to the web application to count HTTP requests per second.

Use monitoring tools (like Prometheus or SumoLogic) to:

Export and store the QPS metric.

Visualize it on a dashboard.

Set up alerts for abnormal spikes or drops.

- Issues with the Infrastructure

SSL Termination at Load Balancer

If SSL is terminated at the load balancer, traffic between the load balancer and the web servers is sent in plain text.

That means if the internal network is compromised, an attacker could intercept unencrypted data.

Best practice: Use end-to-end encryption, re-encrypt traffic between the load balancer and the web servers.

- Single MySQL Server for Writes

If only one MySQL server is responsible for all writes, it becomes a single point of failure.

If it crashes, no data can be written and the entire system may go down.

There's also no write scalability.

Solutions:

Set up MySQL replication with a failover mechanism

Use clustering or multi-master architecture carefully

- All Servers Have All Components (Web, App, DB)

Having each server run everything (web, app, database) is inefficient and risky.

No clear separation of roles → Harder to maintain, scale, and secure.

If one part fails or uses too many resources, it can affect all services on that server.

Best practice:

Separate responsibilities: run web servers, application servers, and database servers on different machines or containers.

Makes the system easier to scale, secure, and troubleshoot.