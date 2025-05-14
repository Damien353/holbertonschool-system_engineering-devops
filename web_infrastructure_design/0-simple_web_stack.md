## Task 0

When a user types www.foobar.com into their browser, the browser makes a request to resolve the domain name. The DNS system translates www.foobar.com to the IP address 8.8.8.8 using an A record for the subdomain www.

The user’s browser then sends an HTTP request to 8.8.8.8. On this server, Nginx acts as the web server: it receives the request and forwards it to the application server (e.g., PHP-FPM). The application logic (contained in the application files) is processed, and if needed, the app queries the MySQL database to fetch or store data.

The response is then sent back through Nginx to the user’s browser.

## Whiteboard



## Questions

- What is a server?
A server is a physical or virtual machine that provides services or functionality to other devices or programs called clients.

- What is the role of the domain name?
A domain name is a human-readable address that maps to the IP address of a server.

- What type of DNS record is "www" in www.foobar.com?
It's an A record that maps the subdomain www to the IP address 8.8.8.8.

- What is the role of the web server (Nginx)?
The web server handles incoming HTTP requests and serves static content or forwards requests to the application server.

- What is the role of the application server?
The application server runs the backend code, processes business logic, and interacts with the database.

- What is the role of the database?
The database stores structured data and allows the application to read or write data efficiently.

- How does the server communicate with the user's computer?
Through the TCP/IP protocol stack, specifically using the HTTP or HTTPS protocol over port 80 or 443.

## Issues with this infrastructure

- SPOF (Single Point of Failure):
If this one server fails, the entire website goes offline.

- Downtime during maintenance:
Deploying new code or restarting the web server can cause temporary unavailability.

- Scalability issues:
The server cannot handle high traffic because all resources (CPU, RAM, etc.) are limited and not distributed.