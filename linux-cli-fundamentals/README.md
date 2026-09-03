## Lab Exercises: Linux & Network Fundamentals

### 1. File Management & Access Control
* **Directory Operations:** Built workspace structures (`mkdir`, `touch`) and handled file migrations using wildcards (`mv *.log`).
* **Access Control:** Applied Least Privilege via `chmod` (enforcing read-only policies and setting user-only executable rights), and managed file cleanup (`rm`).

### 2. Log Analysis & Text Processing
* **Pattern Searching:** Audited log files using `grep` (extracted `"ERROR"` events, performed case-insensitive queries for `"user"`, and counted `"admin"` occurrences).
* **Data Formatting:** Processed output using `sort` and `uniq` to eliminate duplicates and structure log entries.

### 3. System Monitoring & Process Management
* **Process Auditing:** Analyzed active processes (`ps aux`), filtered running services, and monitored live system metrics using `top`.
* **Process Control:** Exercised process termination via `kill`.
* **Resource Inspection:** Audited disk capacity (`df -h`, `du -sh`), memory usage (`free -m`), and uptime/load averages (`uptime`).

### 4. Network Diagnostics & Socket Inspection
* **Virtual Networking:** Configured VM network interface to **Bridged Mode** for direct routing and real IP assignment.
* **IP Configuration:** Inspected network interfaces and routing tables using `ip a` and `ip route`.
* **Path Tracing:** Verified ICMP reachability (`ping`) and mapped routing hops (`traceroute 8.8.8.8`).
* **Socket Auditing:** Identified open listening ports (`netstat -tulnp`) and performed HTTP requests via `curl`.
